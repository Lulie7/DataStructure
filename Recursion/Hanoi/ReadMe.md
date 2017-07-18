# 하노이의 탑 (Hanoi)
## 1. 개념 및 제약사항
![hanoi_1](../images/170718_hanoi_1.png)
- 한 막대에 쌓여있는 원판들을 다른 막대로 이동시켜야 한다.
- 제약사항
+ 한 번에 하나의 원판만 이동할 수 있다.
+ 맨 위에 있는 원판만 이동할 수 있다.
+ 크기가 작은 원판 위에 큰 원판이 있을 수 없다.
+ (크기가 큰 원판 위에만 작은 원판을 놓을 수 있다)
+ 중간 막대를 이용할 수 있으나 앞의 3가지 조건을 만족해야 한다.

<br><br>
![hanoi_2](../images/170718_hanoi_2.png)
- 원판이 3개인 하노이의 탑을 옮기는 과정

## 2. 원판의 갯수가 클 경우의 재귀적 접근 방법
![hanoi_3](../images/170718_hanoi_3.png)
![hanoi_4](../images/170718_hanoi_4.png)
![hanoi_5](../images/170718_hanoi_5.png)
![hanoi_6](../images/170718_hanoi_6.png)
```
void hanoi_tower(int n, char from, char to, char temp) {
  if (n == 1) {
    from에서 to로 원판을 옮긴다.
  } else {
    Step-1) from의 맨 밑 원판을 제외한 나머지 원판들을 temp로 옮긴다.
    Step-2) from에 있는 한 개의 원판을 to로 옮긴다.
    Step-3) temp의 원판들을 to로 옮긴다.
  }
}
```
- Step-1)과 Step-3)은 같은 원판 옮기기지만 문제의 범위가 n-1인데다, 호출 될 때마다 범위가 줄어들기 때문에 재귀적 호출로 변경할 수 있다.
- 단, from과 to의 대상이 변경된다는 점에 주의!
```
void hanoi_tower(int n, char from, char to, char temp) {
  if (n == 1) {
    from에서 to로 원판을 옮긴다.
  } else {
    hanoi_tower(n-1, from, to, temp);
    from에 있는 한 개의 원판을 to로 옮긴다.
    hanoi_tower(n-1, temp, from, to);
  }
}
```






# 피보나치 수열 (Fibonacci)
## 1. 기본개념
- fib(n)
+ 0   if n=0
+ 1   if n=1
+ fib(n-1) + fib(n-2)   if n>=2

## 2. 재귀 호출을 이용한 구현
![book](../images/recursion_fibonacci_1.png)
- 피보나치 수열을 재귀 호출로 구현할 경우 성능면에서 매우 비효율적
- 같은 숫자에 대한 피보나치 수열 계산을 중복하여 호출하기 때문이다.
- ex) fib(6)의 값을 계산하기 위해 fib(4)가 두 번 호출, fib(3)은 세 번 호출되므로...
- 시간복잡도가 O(n^2) 이므로 n의 값이 커질수록 매우매우 비효율적

## 3. 반복 호출을 이용한 구현
```
int i = 0, temp = 0, current = 1, last = 0;

for(i = 2; i <= n; i++) {
  temp = current;
  current += last;
  last = temp;
}
```
- 반복 호출을 이용하면 시간복잡도가 O(n)
- 재귀 호출에 비해 수행시간이 매우 짧다는 장점!
- 그러나, 한 눈에 흐름을 파악할 수 없다는 단점!
