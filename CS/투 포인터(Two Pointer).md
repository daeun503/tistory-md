# Two Pointer (투 포인터)

투 포인터는 1차원 배열에서 두 개의 포인터를 이동하며 원하는 값을 얻는 방식이다. 주로 다음과 같이 두 가지 방식 중 하나를 채택한다.

- 1차원 배열 **처음과 끝에 각 포인터**를 두고, 각 포인터가 중앙으로 오는 방식
- 1차원 배열 **처음에 두 포인터**를 두고, 각 포인터가 전진하는 방식

투 포인터와 비슷한 슬라이딩 윈도우가 있다. 슬라이딩 윈도우는 고정 사이즈의 윈도우가 이동하면서 윈도우 내에 있는 데이터를 이용해 문제를 푸는 알고리즘이다. 2개의 네트워크 호스트 간의 패킷 흐름을 제어하기 위한 방법을 지칭하는 네트워크 용어이기도 하다.

투 포인터와 슬라이딩 윈도우는 비슷하지만 다음과 같은 차이가 있기도 하다.

| 이름            | 배열 정렬 여부 | 윈도우 사이즈 | 이동               |
| --------------- | -------------- | ------------- | ------------------ |
| 투 포인터       | 대부분 O       | 가변          | 좌우 포인터 양방향 |
| 슬라이딩 윈도우 | X              | 고정          | 좌 또는 우 단방향  |

<br/>

# 첫 번째 방식

> 첫 번째 방식은 1차원 배열 **처음과 끝에 각 포인터**를 두고, 각 포인터가 중앙으로 오는 방식이다.

 

[[BOJ 3273] 두 수의 합](https://www.acmicpc.net/problem/3273)로 설명하기 위해 문제를 요약하자면 다음과 같다.

- n개의 서로 다른 양의 정수로 이루어진 수열이 있을 때, Ai + Aj = x가 되는 (i, j) 쌍을 구하시오



처음 포인터를 s (start) , 끝 포인터를 e (end) 라고 설정한다. start와 end의 합을 구하며 다음 로직을 반복한다.

- 합이 타겟보다 작으면 start를 오른쪽으로 이동하여 합을 증가시킨다.
- 합이 타겟보다 크면 end를 왼쪽으로 이동하여 합을 감소시킨다.
- 합이 타겟과 같으면 start, end 모두 이동한다. 하나만 이동해선 무조건 타겟과 같을 수 없기 때문.

**배열을 정렬**한 후 진행해야한다. 예제에서 target은 13인데 설명을 위해 14로 변경했다.

![image-20211219031139249](투 포인터(Two Pointer).assets/image-20211219031139249.png)

![image-20211219031202137](투 포인터(Two Pointer).assets/image-20211219031202137.png)



```python
n = int(input())
arr = list(map(int, input().split()))
x = int(input())

# start, end 포인터
s, e = 0, n-1
result = 0
# 정렬
arr.sort()

while s < e:

    # start + end 의 합 pair_sum
    pair_sum = arr[s] + arr[e]

    # 합이 x 이면 +1 // start, end 이동
    if pair_sum == x:
        result += 1
        s += 1
        e -= 1

    # 합이 x 보다 작으면 start를 오른쪽으로
    elif pair_sum < x:
        s += 1

    # 합이 x 보다 크면 end를 왼쪽으로
    else:
        e -= 1

print(result)
```

<br/>

# 두 번째 방식

> 1차원 배열 **처음에 두 포인터**를 두고, 각 포인터가 전진하는 방식

이 방식은 Runner 기법과 유사하기도 하다. Runner 기법에서는 **한 포인터가 다른 포인터보다 앞서게 하여 병합 지점이나 중간 위치, 길이 등을 판별**할 때 유용하게 사용할 수 있다. 각각 Fast Runner, Slow runner라고 부르는데, 대개 fast는 두 칸씩, slow는 한 칸씩 이동한다. 때문에 fast가 끝에 도달했을 때 slow는 중간 지점에 위치하게 된다.

![image-20211219040340395](투 포인터(Two Pointer).assets/image-20211219040340395.png)

Fast runner는 더 빠른 포인터 end, Slow runner는 더 느린 포인터 start에 대응한다.



[[BOJ 2003] 수들의 합2](https://www.acmicpc.net/problem/2003) 으로 설명하기 위해 문제를 요약하자면 다음과 같다.

- N개의 수로 된 수열에서 i ~ j 번째 수의 합이 M이 되는 경우의 수는 몇 개 인가?



 더 느린(시작점) 포인터를 s (start), 더 빠른(끝점) 포인터를 e (end) 라고 설정한다. start와 end의 **구간합**을 구하며 다음 로직을 반복한다.

- 합이 M보다 작으면 end를 오른쪽으로 이동하여 합을 증가시킨다.
- 합이 M보다 크면 start를 오른쪽으로 이동하여 합을 감소시킨다.
- 합이 M과 같으면 start 혹은 end를 오른쪽으로 이동한다.



![image-20211219041512781](투 포인터(Two Pointer).assets/image-20211219041512781.png)

![image-20211219041538901](투 포인터(Two Pointer).assets/image-20211219041538901.png)

![image-20211219041555718](투 포인터(Two Pointer).assets/image-20211219041555718.png)

```python
N, M = map(int, input().split())
arr = list(map(int, input().split()))

s, e, total = 0, 0, 0
result = 0

while 1:
    # total과 M이 같으면 result +1
    if total == M:
        result += 1

    # total이 M보다 같거나 크면 start +1
    if total >= M:
        total -= arr[s]
        s += 1
    # end가 끝인데 위 if에서 안걸렸으면 total < M이란 것이므로 break
    elif e == N:
        break
    # 아직 end가 끝이 아니고 total이 M보다 작으므로 end +1
    else:
        total += arr[e]
        e += 1

print(result)
```

