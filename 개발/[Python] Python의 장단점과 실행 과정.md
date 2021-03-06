# [Python] Python의 장단점과 실행 과정



## Python이란?

>파이썬은 1991년 네덜란드계 프로그래머인 귀도 반 로섬이 발표한 고급 프로그래밍 언어로, 플랫폼에 독립적이며 인터프리터식, 객체지향적, 동적 타이핑 대화형 언어이다.

파이썬의 핵심 철학은 다음과 같다. 핵심 철학에 걸맞게 파이썬은 아주 쉽다! 그래서 여러 대학의 교양 과목이나 비 전공자의 프로그래밍 입문에서 주로 소개되는 언어이다.

- "아름다운 게 추한 것보다 낫다." (Beautiful is better than ugly)
- "명시적인 것이 암시적인 것 보다 낫다." (Explicit is better than implicit)
- "단순함이 복잡함보다 낫다." (Simple is better than complex)
- "복잡함이 난해한 것보다 낫다." (Complex is better than complicated)
- "가독성은 중요하다." (Readability counts)

<br/>

## Python의 장점

1. 간결한 코드, 쉬운 문법, 낮은 러닝 커브 => 높은 생산성
   - 인간의 사고와 유사하여 코드를 작성하기 쉽다. 수도 코드가 곧 파이썬 코드입니다. 
   - 어느 정도 문법과 코드 스타일이 강제되기 때문에 팀원과 코드 스타일에 대해 논할 시간을 줄일 수 있다.
2. 방대한 라이브러리
   - 파이썬은 대부분의 라이브러리가 이미 다른 사용자에 의해 구현되어 있다.
   - 수 십년 동안 다양한 분야의 방대한 라이브러리를 쌓아왔으며 개발 생태계가 활발하다.
3. 플랫폼 독립적
   - 리눅스, 윈도우 등 어떤 플랫폼에서도 동일하게 동작한다.
4. 인터프리터 언어
   - 인터프리터 언어는 원시코드를 기계어로 변환하는 과정 없이 한 줄씩 바로 해석하여 실행하는 언어이다.
   - 파이썬은 인터프리터 언어로 한 줄씩 실행되어 대화식으로 쉽게 사용할 수 있다.
   - 한 줄씩 실행되기 때문에 소스 코드 수정 및 디버깅이 쉽다.
5. 동적 타이핑
   - 변수의 자료형을 지정하지 않고 단순히 선언하는 것만으로도 값을 지정할 수 있다.
   - 선언된 변수의 자료형은 해당 코드가 실행될 때 결정된다.

<br/>

## Python의 단점

1. 느린 속도
   - 다른 언어들보다 느리다. 아래 이유로...
2. 인터프리터 언어
   - 컴파일 언어는 원시코드를 기계어로 변환한 뒤 실행한다. 처음 원시코드를 기계어로 번역하는 데에 오래 걸리지만, 런타임 상황에서는 이미 기계어로 모든 소스 코드가 변환되었기 때문에 더 빠르다.
   - 즉, 인터프리터 언어인 파이썬은 컴파일 언어보다 느리다. 
3. 동적 타이핑
   - 동적 타이핑 덕분에 초보자가 개발하기 쉬우나, 사소하게 잘못된 데이터 타입을 찾을 때 어려울 수 있다.
   - 동적으로 입력된다는 것은 많은 메모리, 충분한 메모리 공간을 확보해놔야 한다는 것이다. 
   - 많은 메모리 사용은 많은 컴퓨팅 시간을 의미한다. 
4. GIL
   - 멀티 스레드를 구현할 때 문제가 된다. 
   - 공유 자원에 접근할 때 하나의 스레드만 접근이 가능하도록 하고 다른 스레드는 락을 걸어버린다.

<br/>

## 파이썬의 실행 과정

파이썬은 해석 프로그램에 따라 아래와 같이 나뉠 수 있다. 

- CPython : C로 작성된 인터프리터.
- Jython : 자바가상머신용 인터프리터. 
- lronPython : .NET 플랫폼용 인터프리터
- PyPy : 파이썬으로 작성된 파이썬 인터프리터



보통 기본적으로 사용하는 Python의 인터프리터는 CPython이기 때문에 이에 대해 설명한다. 

CPython은 C 언어로 구현한 구현체인데, 인터프리터이자 컴파일러이다. 파이썬 파일을 실행하면 런타임 중의 컴파일 과정에서 렉서(lexer, 요소를 하나하나 쪼갬), 파서(parser, 구문분석)를 거쳐서 바이트 코드를 만들어낸다. 해당 바이트 코드가 들어있는 파일이 .pyc이다. 이것을 인터프리터가 실행함으로써 파이썬 파일을 실행할 수 있다.

> Python 코드 → 실행 & 런타임 시작 →  파이썬 컴파일러 → 바이트코드(.pyc) → 파이썬 인터프리터 (VM) →  기계어 →  CPU

어셈블리어는 CPU에 의존적이지만 바이트코드는 VM 위에서 돌아가기 때문에 그렇지 않아서, 어떠한 플랫폼 위에서도 잘 실행되는 것이다.

<br/>

## 참고자료

- [지금 잘나가는 파이썬의 미래를 어둡게 보는 이유](https://techit.kr/view/?no=20200418133036)
- [위키백과 파이썬](https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%9D%B4%EC%8D%AC)
- [강의노트 13. compiler, interpreter](https://wayhome25.github.io/cs/2017/04/13/cs-14/)
- [[Python] 파이썬 동작 방식](https://velog.io/@chldppwls12/python-%EB%8F%99%EC%9E%91-%EB%B0%A9%EC%8B%9D)

