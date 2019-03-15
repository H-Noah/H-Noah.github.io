---
title: "[풀이]백준 풀이(IV/1260)"
permalink: docs/solve(IV)
last_modified_at: 2019-03-15T17:58:49-04:00
excerpt: "BOJ 1260 등 다수의 잡 문제 풀이"
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


## 문제풀이

### DFS와 BFS(1260, DFS, BFS)

> 회고 

- 쓸모 없는 짓을 많이했다... cout 찍는 곳에서 ㅎㅎ...
- DFS의 마지막을 체크하기 위해 한 뻘짓 ^^..   

```c++
bool recheck(){
	int count=0;
	for(int i=0; i<1001; i++){
		//못가는 곳이 몇개인지
		if(check[i]) count++;
	}
	cout <<  "count = "<<count <<endl;
	if(count==0) {
		return false;
	}
	else {
		return true;
	}
}
```

- DFS와 BFS의 차이를 알 수 있는 좋은 문제

```c++
#include <iostream>
#include <vector>
#include <queue>
#include <stack>
#include <algorithm>

using namespace std;
bool check[1001];
bool connection[1001][1001];
int dist[1001];
int n, m, v;

void init(){
	for(int i=0; i<1001; i++) check[i]=false;
}
void dfs(int x){
	cout << x+1 << " ";
	//if(정답을 찾음) 정답을 찾은처리
	if(check[x]) return;
	check[x]=true;

	for(int i=0; i<n; i++){
		if(connection[x][i] && !check[i]){
			dfs(i);
		}
	}
}
void bfs(int v){
	queue<int> q;
	q.push(v);
	check[v] = true;
	dist[v] = 0;
	cout << v+1 << " ";

	while(!q.empty()){
		int x = q.front();
		q.pop();
		//모든 정점에 대해
		for(int y=0; y<n; y++){
			if(!check[y] && connection[x][y]){
				q.push(y);
				check[y] = true;
				dist[y] = dist[x]+1;
				cout << y+1 << " ";
			}
		}
	}
}
int main(){
	cin >> n >> m >> v;
	for(int i=0; i<m; i++){
		int a, b;
		cin >> a >> b;
		connection[a-1][b-1]=true;
		connection[b-1][a-1]=true;
	}
	dfs(v-1);
	cout << endl;
	init();
	bfs(v-1);
}
```

### 연결 요소의 개수(BFS, 11724)

- 방향 없는 그래프가 주어졌을 때, 연결 요소의 개수를 구하는 프로그램을 작성하라
- 정점의 개수 N, 간선의 개수 M `(1<=N<=1000, 0<=M<=N*(N-1)/2)`
- M개의 줄어 주어지는 간선 (u,v) `(u!=v, 1<=u,v<=N)`





### 진법 변환 2(11005)

왜 실패가 떠있는지는 모르지만 일단 try.

- 10진수 N을 받아 B진법으로 바꿔 출력하는 프로그램
- 진법 변환 1을 풀었던 기억이 난다. 자릿수의 합을 진법으로 나누어 나머지를 구했던 것 같다.
- N은 10억보다 작거나 같은 자연수, B는 2~36의 정수이다.

> 번호를 잘못봤다.. 중요한 문제가 아니므로 다음에 풀어보자

```c++



```


### A/B(잡문제, 1008)

```c++
#include <iostream>
#include <iomanip>

using namespace std;

int main(){
	double A,B;
	
	cin>>A;
	cin>>B;
	cout.precision(10);
	cout<< A/B;
	
}
```

### 2017년(잡문제, 1924)

```c++
#include <iostream>

using namespace std;

int main() {
	int m;
	int d = 0;
	cin >> m;
	cin >> d;
	int M[12] = { 31,28,31,30,31,30,31,31,30,31,30,12 };
	if (m < 13 && d < 32) {

		for (int i = 0; i < m - 1; i++) {
			d += M[i];
		}
		d = d % 7;
		switch (d) {
		case 1: cout << "MON"; break;
		case 2: cout << "TUE"; break;
		case 3: cout << "WED"; break;
		case 4: cout << "THU"; break;
		case 5: cout << "FRI"; break;
		case 6: cout << "SAT"; break;
		case 0: cout << "SUN"; break;
		}
	}
	else
	{
		cout << "Error" << endl;
	}
}
```


### 시험성적(잡문제, 9498)

```c++
#include <iostream>

using namespace std;
int main() {
	int i;
	cin >> i;	
	if (89 < i) {
		cout << "A";
	}
	else if (79 < i) {
		cout << "B";
	}

	else if (69 < i ) {
		cout << "C";
	}

	else if (59 < i ) {
		cout << "D";
	}
	else
		cout << "F";	
}
```

### 세 수(잡문제, 10817)

```c++
#include <iostream>
using namespace std;
int main() {
	int a=0,b=0,c=0;
	cin >> a;
	cin >> b;
	cin >> c;
	int temp;
	for (int i = 0; i < 10; i++) {
		if (a > b) {
			temp = b;
			b = a;
			a = temp;
		}
		if (b > c) {
			temp = c;
			c = b;
			b = temp;
		}
		if (a > c) {
			temp = c;
			c = a;
			a = temp;
		}
	}
	cout << b << endl;	
}
```

### 사칙 연산(잡문제, 10869)

```c++
#include <iostream>
#include <iomanip>
using namespace std;

int main(){
	int A,B;
	cin>>A;
	cin>>B;
	cout.precision(10);
	cout<< A+B<<endl;
	cout<< A-B<<endl;
	cout<< A*B<<endl;
	cout<< A/B<<endl;
	cout<< A%B<<endl;	
}
```

### X보다 작은 수(잡문제, 10871)

```c++
#include <iostream>

using namespace std;

int main() {
	int n;
	int x;
	int N[10000];

	cin >> n;
	cin >> x;
	for (int i = 0; i < n; i++) {
		cin >> N[i];
	}
	for (int j = 0; j< n; j++) {
		if (x > N[j])
			cout << N[j] << " ";
	}
}
```

### AxB (잡문제, 10998)

```c++
#include <iostream>
using namespace std;
int main(){
	int A,B;
	cin>>A;
	cin>>B;
	cout<< A*B;
	
}
```


### 열 개씩 끊어 출력하기(잡문제, 11721)

> 회고

하다가 중간에 짜증나서 딴거 풀었었는데 소스비교 한 번 해봐야겠다!


```c++
#include <iostream>
using namespace std;
int main() {
	int cnt = 0;
	char word[10000];
	cin >> word;

	for (int j = 0; j < 100; j++) {
		if (word[j] != '\0') {
			cnt++;
		}
		else
			j = 100;
	}
	char *rst = new char[cnt];
	rst[0] = '\0';
	for (int k = 0; k < cnt; k++) {
		rst[k] = word[k];
	}

	for (int i = 0; i < cnt; i++) {
		if (i % 10 != 0) {
			cout << rst[i];
		}
		else if (i % 10 == 0) {
			if (i != 0) {
				cout << endl;
			}
			cout << rst[i];
		}					
	}
}
```
 



