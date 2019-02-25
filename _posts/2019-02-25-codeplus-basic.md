---
title: "[강의]코드플러스 기초"
permalink: /docs/problem001-picnic
last_modified_at: 2019-02-21T17:58:49-04:00
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - algorithm
  - coding

---

**Note:** 전체목차를 다룰 수 없어 필요하다고 생각하는 부분만 발췌하여 요약합니다.
{: .notice--warning}




## 수학

### 나머지 연산 (mod)

`정답을 N으로 나눈 나머지를 출력하라`는 경우가 있음 = 정답이 너무크다.

int(2^31-1), longlong(2^63-1)을 넘어가는 경우(대략 10^18) 어쩔 수 없이 문자열 혹은 다른 라이브러리를 사용해서 구현해야 한다.

1. (A+B)%C = (A%C + B%C)
2. (A*B)%C = (A%C * B%C)

나눗셈, 뺄셈(음수)에 대해서는 적용되지 않는다.
따라서, 뺼셈의 경우에는 <mark>(a%c - b%c +c)%C</mark>로 먼저 양수로 만들어 준 뒤 모듈라연산을 해야한다.   
나누기의 경우에는 페르마의 소정리 <mark>(a/b^c-2)%c</mark>(a/b는 서로소, c는 소수)를 이용한다..


#### 나머지(10430)

```javascript
#include <iostream>
#include <string>
#include <cstring>


using namespace std;


int main(void)
{
	int A, B, C;

	cin >> A >> B >> C;

	cout << (A+B)%C << endl;
	cout << (A%C + B%C)%C << endl;
	cout << (A*B)%C << endl;
	cout << (A%C * B%C)%C;
}

```


### 최대공약수 (GCD)

정답이 분수형태로 나오는 경우 -> 기약분수로 출력하라. 또는 수학공식을 써야하는 문제에 필요하다.

* 가장 쉬운 방법은 2부터 min(A,B)까지 모든 정수로 나누어 보는 방법 = O(N)

* 유클리드 호제법 = O(logN)
   - GCD(a,b) = GCD(b,r)과 같다. r=0인순간 b가 최대공약수이다.
   - GCD(24,16) = GCD(16,8) = GCD(8,0) = 8 
   - 재귀함수를 이용해서 구현할 수 있다.
   
   ```javascript 
  int gcd(int a, int b){
    if(b==0){
      return a;
    } else{
      return gcd(b, a%b);
    }
  }
   ```

  - 재귀함수를 사용하지 않을 수도 있다.     
   
   ```javascript
  int gcd(int a, int b){
    while(b!=0){
      int r= a%b;
      a= b;
      b= r;
    }
    return a;    
  }
  ```   

  
### 최소공배수 (LCM)

> 편안... A*B/GBD

> 비재귀방법이 안되던데.... 다시 확인할 것


### 최대공약수와 최소공배수(2609,) 1934

```javascript
#include <iostream>
#include <string>
#include <cstring>
using namespace std;

int gcd(int a, int b);

int main(void)
{
	int a, b;
	cin >> a >> b;
	cout << gcd(a,b) << endl<< a*b/gcd(a,b);
}

int gcd(int a, int b) {
	if (b == 0) {
		return a;
	}
	else {
		return gcd(b, a%b);
	}
}

```



```javascript

#include <iostream>
#include <string>
#include <cstring>

using namespace std;

int gcd(int a, int b);

int main(void)
{
	int T;
	cin >> T;
	int a, b;
	for(int i=0; i<T; i++){
		cin >> a >> b;
		cout << a*b/gcd(a,b) << endl;;
	}
}

int gcd(int a, int b) {
	if(b==0) return a;
	int r = a%b;
	a = b;
	b = r;
	gcd(a,b);
}

```

### 소수

* 약수가 1과 자기 자신 밖에 없는 수
* N이 소수가 되려면 2보다 크거나 같고 N-1보다 작거나 같은 자연수로 나누어 떨어지면 안된다.

1. 소수와 관련된 알고리즘= O(N)

```javascript
bool prime(int n){
  if(n<2) return 0;

  for(int i=2; i<=n-1; i++){
    if(n%i ==0){
      return 0;
    }
  }
  return 1; 
}
```

2. 소수와 관련된 알고리즘= O(N)

* N이 소수가 되려면 2부터 크거나 같고, N/2보다 작거나 같은 자연수로 나누어 떨어지면 안된다.
(N의 약수 중에서 가장 큰 것은 N/2보다 작거나 같기 때문)


```javascript
bool prime(int n){
  if(n<2) return 0;

  for(int i=2; i<=n/2; i++){
    if(n%i ==0){
      return 0;
    }
  }
  return 1; 
}
```


3. __[결론]소수와 관련된 알고리즘= O(루트N)__

* N이 소수가 되려면 2보다 크거나 같고 루트N보다 작거나 같은 자연수로 나누어 떨어지면 안된다.
(N이 소수가 아니라면 A*B형태로 나타낼 수 있으며 A>=(루트N), B<=(루트N))



```javascript
bool prime(int n){
  if(n<2) return 0;

  for(int i=2; i*i<=n; i++){
    if(n%i ==0){
      return 0;
    }
  }
  return 1; 
}
```

### 소수(1978)

```javascript
#include <iostream>
#include <string>
#include <cstring>


using namespace std;

bool prime(int a);

int main(void)
{
	int T;
	cin >> T;
	int a;
	int result= 0;
	for(int i=0; i<T; i++){
		cin >> a;
		result += prime(a);
	}
	cout << result;
}

bool prime(int a) {
	if(a<2) return 0;
	for(int i=2; i*i<=a; i++){
		if(a%i == 0) return 0;
	}
	return 1;
}
```

### 에라토스테네스의 체 = O(NloglogN) 

패스


### 골드바흐의 추축

패스

## 브루트포스(1)

### 브루트포스

모든 경우의 수를 다 해보는 것이다. 일반적으로 문제 시간제한을 넘지 않으려면 초당(1~10억)아래의 수만 연산할 수 있다. <mark>실제로는 천만정도가 한계</mark>