https://zerozero7bang.tistory.com/6



# [Vue.js] 코로플레스 맵 만들기

`코로플레스 맵(Choropleth Map)`은 색상 또는 패턴을 사용하여 특정 통계에 대한 **데이터를 사전에 정의된 영역과 관계**시키는 맵 유형이다. 앱을 사용했을 때 어떤 지역에서 사용했는지 확인하여 사용 횟수를 증가시키고, 해당 지역의 사용 횟수를 코로플레스 맵을 이용해 보여주는 작업을 진행했다. 프로젝트에서 코로플레스 맵의 비중이 그리 큰 편이 아니라, 코드에 힘 안 들이고 다른 사람 코드 참고하면서 기능만 수정하고 빨리 넘어갔다.

-   D3로 우리나라 인구밀도 시각화하기 [http://bl.ocks.org/e9t/55699e9fa8c3eb7fe40c](http://bl.ocks.org/e9t/55699e9fa8c3eb7fe40c)
-   서울시 생활 인구 코로플레스맵 시각화[https://story.pxd.co.kr/1408](https://story.pxd.co.kr/1408)
-   D3.js Geo Map on Vue.js(D3.js를 이용하여 지도 그리기)[https://parandol.tistory.com/38](https://parandol.tistory.com/38)
-   d3-scale-chromatic[https://github.com/d3/d3-scale-chromatic](https://github.com/d3/d3-scale-chromatic)
-   southkorea-maps[https://github.com/southkorea/southkorea-maps](https://github.com/southkorea/southkorea-maps)

<br/>

D3.js는 웹브라우저 상에서 동적이고 인터렉티브한 **정보시각화**를 구현하기 위한 자바스크립트 라이브러리이다. Vue에서 사용할 것이니 npm으로 d3 깔고 나서, 일단 알못이니까 Quick start 마냥 [코드](http://bl.ocks.org/e9t/55699e9fa8c3eb7fe40c) 넣고 실행하면 돌아가길 바랐는데 함수를 못 찾는다고 안 된다.

 확인하니 코드는 d3.v3를 사용하고 d3 공식 문서에서는 d3.v7 까지 나와서 npm으로 깐 게 몇 버전인지는 몰라도 상위 버전이라서 안 된다고 한다. v3과 v4이상부터 꽤 차이가 난다는 듯. v3은 모든 게 다 들어있지만 크고, v4는 나눠져있어서 필요한 것만 가져다 쓸 수 있다고 한다. 그 과정에서 사라진 함수나 이름이 바뀐 함수가 꽤 많은 듯. 결론적으로 그냥 코드대로 라이브러리 설치 없이 d3.v3.js import해서 사용했다.

-   d3.js [https://d3js.org/](https://d3js.org/)
-   D3 V4 - What's new? [https://iros.github.io/d3-v4-whats-new/#1](https://iros.github.io/d3-v4-whats-new/#1)

<br/>

GeoJSON은 위치정보를 갖는 점을 기반으로 체계적으로 지형을 표현하기 위해 설계된 개방형 공개 표준 형식이다. JSON인 자바스크립트 Object Notation을 사용한다. TopoJSON 은 GeoJSON의 확장 형식으로 각 영역을 아크(arcs)들의 영역으로 구분하여 표시하는 기능을 제공해주어 연산량을 적게 해준다. GeoJSON보다 80% 가량 **더 크기가 작다**고 하니, 이번에는 크기를 줄이기 위해 TopoJSON을 사용했다.

-   TopoJSON [https://github.com/topojson/topojson](https://github.com/topojson/topojson)

<br/>

<br/>

D3로 우리나라 인구밀도 시각화하기 의 코드를 살펴보자. 해당 코드에서는 TopoJSON파일로 맵을 만들고, **csv에 저장된 값을 이용**해서 코로플레스 맵을 만든다. html/css 부분은 간단하니 제외하고 script만 보자

```vue
<script>
  // 너비, 높이 설정
  var width = 960,
      height = 500;

  // #chart에 svg 추가 & 너비, 높이 속성 값 부여
  var svg = d3.select("#chart").append("svg")
      .attr("width", width)
      .attr("height", height);

  // 맵 중앙 & 확대 축소 스케일
  var projection = d3.geo.mercator()
      .center([128, 36])
      .scale(4000)
      .translate([width/2, height/2]);

  var path = d3.geo.path()
      .projection(projection);

  // 값 0 ~ 1000(domain)을 9단계(range)로 나누기
  var quantize = d3.scale.quantize()
      .domain([0, 1000])
      .range(d3.range(9).map(function(i) { return "p" + i; }));

  var popByName = d3.map();

  // 동기 처리. municipalities-topo-simple.json 이라는 topojson파일을 읽은 후
  // population-edited.csv 를 읽어서, name 값: population 값으로 설정 후 ready 실행 
  queue()
      .defer(d3.json, "municipalities-topo-simple.json")
      .defer(d3.csv, "population-edited.csv", function(d) {
        popByName.set(d.name, +d.population);
      })
      .await(ready);

  function ready(error, data) {
      var features = topojson.feature(data, data.objects["municipalities-geo"]).features;

      // 위에서 csv 파일 읽은 후 저장한 값 popByName: {name1: population1, ...} 으로 저장되어서
      // popByName.get(d.properties.name) 하면 population값이 나온다. 이를 저장
      // 밀도를 구하는 거라 area로 나눠주고 그 값을 반영
      features.forEach(function(d) {
          d.properties.population = popByName.get(d.properties.name);
          d.properties.density = d.properties.population / path.area(d);
          d.properties.quantized = quantize(d.properties.density);
      });


      // 색 입히고 텍스트 설정하고 등등
      svg.selectAll("path")
          .data(features)
          .enter().append("path")
          .attr("class", function(d) { return "municipality " + d.properties.quantized; })
          .attr("d", path)
          .attr("id", function(d) { return d.properties.name; })
          .append("title")
          .text(function(d) { return d.properties.name + ": " + d.properties.population/10000 + "만 명" });

      svg.selectAll("text")
          .data(features.filter(function(d) { return d.properties.name.endsWith("시"); }))
          .enter().append("text")
          .attr("transform", function(d) { return "translate(" + path.centroid(d) + ")"; })
          .attr("dy", ".35em")
          .attr("class", "region-label")
          .text(function(d) { return d.properties.name; });
  }
</script>
```

<br/>

위에서는 csv에 저장된 값을 사용했지만, 나는 **DB에 저장된 값**을 가져와서 보여주어야 했다.

1.  앱 사용 완료 후 현재 주소를 post 요청 보낸다.
2.  back에서 주소를 받고 파싱 후 DB에 저장 (key: 지역 코드, value: 정수 값)
3.  get 요청으로 DB의 값을 받고 코로플레스 맵 시각화 ← 이걸 구현

이제 위 코드를 Vue로 옮겨보자. html은 tmplate에 넣고, style도 style에 넣으면 된다. 간단해서 달라진 부분만 설명. 결과 이미지는 기존 코드랑 똑같고 데이터만 DB에서 받아와서 보여준다. 과정에서 TopoJSON 이 2012 버전이라 **지역 코드가 안 맞는 문제**가 있었다. 또, 나는 시군구 까지만 사용할 건데 T**opoJSON 은 더 깊게 나눠진 문제**도 있었다. 최신 TopoJSON을 찾으려고 했는데 못 찾아서(GeoJSON은 있는 것 같은데 직접 변환할 시간이 없어서) 직접 JSON파일 자체를 수정했다. 지역 코드 DB key를 TopoJSON에서 추출하면 둘 다 안 맞아서 오히려 제대로 되는 현상(?)이 발생하긴 한다.

```vue
// 나머지 script는 index.html에 넣었다.
<script src="https://d3js.org/queue.v1.min.js"></script>
<script>
import { HTTP } from '@/util/http-common';

export default {
  name: '이름 써주기',
  mounted() {
    var width = 380,
        height = 600;

    var svg = d3.select("#chart").append("svg")
        .attr("width", width)
        .attr("height", height);

    var projection = d3.geo.mercator()
        .center([127.8, 36])
        .scale(5000)
        .translate([width/2, height/2]);

    var path = d3.geo.path()
        .projection(projection);

    var quantize = d3.scale.quantize()
        .domain([0, 100])
        .range(d3.range(9).map(function(i) { return "p" + i; }));

    var popByName = d3.map();

    queue()
      .defer(d3.json, "municipalities-topo-simple.json")
      .defer(data_request)
      .await(ready);
  
    // ~/map 으로 axios get요청을 보낸다. data가 {11010: 22, 11080: 32, ... }식으로 온다.
    // 각 값을 popByName에 써주고 callback으로 돌아가서, ready를 실행하면 된다.
    function data_request(callback) {
      HTTP.get(`/map`)
      .then(res => {
        return res.data.data
      })
      .then(datas => {
        datas.forEach((data) => {
          popByName.set(data.code, +data.count)
        })
        callback()
      })
    }

    function ready(error, data) {
      var features = topojson.feature(data, data.objects["municipalities-geo"]).features;

      // 기존 코드에서는 밀도로 했지만 나는 값 자체를 사용할 거라 나누는 부분은 필요없다.
      features.forEach(function(d) {
        d.properties.dataCnt = popByName.get(d.properties.code);
        d.properties.quantized = quantize(d.properties.dataCnt);
      });

      svg.selectAll("path")
        .data(features)
        .enter().append("path")
        .attr("class", function(d) { return "municipality " + d.properties.quantized; })
        .attr("d", path)
        .attr("id", function(d) { return d.properties.name; })
        .append("title")
        .text(function(d) {
          return d.properties.name + " " + d.properties.dataCnt + "개" 
        });
    }
  }
}
</script>
```

<br/>

언젠가 써볼만한 데이터 시각화 툴

-   테이블 형태 [https://datatables.net/](https://datatables.net/)
-   데이터 비주얼 차트 [https://plotdb.com/](https://plotdb.com/)