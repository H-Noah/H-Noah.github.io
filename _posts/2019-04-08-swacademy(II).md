---
title: "[풀이]swacademy 풀이(II/1206 등)"
permalink: docs/swacademy(II)
last_modified_at: 2019-04-08T17:58:49-04:00
excerpt: "SW ACADEMY 1206 등 다수의 잡 문제 풀이"
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

- A형 결과가 발표날 때 까지는 취미겸 SW아카데미 등급을 올려야겠다.
- 전략을 변경한다. (SW Academy 등급올리기 + B형취득)

### View(1206, D3)

- 빌딩 층별로 양쪽에 2칸 이상 다른 건물이 없을 경우 조망권이 있다고 한다.
- 조망권이 확보된 세대의 수를 반환하는 프로그램을 작성하라.
- 가로길이는 1000이하, 높이는 최대 255

- 만약 2차원배열에 직접채워 넣는경우, 모든 경우를 search하는 경우  1000 * 255  * (양쪽2칸 4)= 100만쯤?

- 줄이려면 양쪽2칸을 봤을 때 겹친다면 겹치는 녀석도 조망권 X 처리
- 아무튼 자신의 높이를 기준으로 양옆을 확인해서 max를 구한 뒤 빼면된다.

```c++
#include <iostream>
#include <cmath>
#include <algorithm>
using namespace std;

int T, test_case;
int Answer = 0;
int main(){
	int building[1000];
	for(test_case=1; test_case<11; test_case++){
		Answer =0;
		int n;
		cin >> n;
		for(int i=0; i<n; i++){
			cin >> building[i];
		}

		for(int i=2; i<n-2; i++){
			int l1 = building[i-1];
			int l2 = building[i-2];
			int r1 = building[i+1];
			int r2 = building[i+2];
			int c = building[i];

			int l = max(l1,l2);
			int r = max(r1,r2);
			int maxHeight = max(l,r);
			if(c>maxHeight) Answer += (c-maxHeight);
		}
		cout << "#" << test_case << " " << Answer<< endl;
	}
}
```

> 남의 코드 보기

그냥 내 풀이랑 거의똑같네... 패스


### [RE]최대 상금(1244, D3)

- 퀴즈대회 우승 시 보너스 상금을 획득할 수 있다.
- 우승자는 숫자판 중 2개를 선택해 정해진 횟수만큼 서로의 자리를 교환할 수 있다.
- 숫자판의 오른쪽 끝부터 1원이고 왼쪽으로 갈수록 10의 배수만큼 커진다.
- **중요**: 반드시 횟수만큼 교환이 이루어져야하고 동일한 위치의 교환이 중복되어도 된다. (항상 최대값이 출력되지 않을수도 있음)


- 바꿀 것 2개를 선택한다. 
- n번만큼 반복한다.
01 01 01, 01 01 02, 01 01 03, 01 01 04 ... 등 쭉 가면 너무 경우의 수가 많아지므로 좀 줄여가야 할 것 같다.
- 버블소트랑 비슷한 원리인데...

> 풀이

- 거른다 이문제..
- 기회되면 코드리뷰할 것

```c++
#include <iostream>
#include <cmath>
#include <string>
#include <algorithm>
#include <string.h>
using namespace std;
int T, test_case;
int Answer = 0, n;
char reward[6];
string s;

void calc(int cnt, int now){
	if(cnt==n) {
		Answer= max(Answer, stoi(s));
		return;
	}
	int size = s.size();
	for(int i=now; i<size; i++){
		for(int j=i; j<size; j++){
			if(i==j) continue;
			if(s[i]<=s[j]){
				swap(s[i],s[j]);
				calc(cnt+1, i);
				swap(s[i],s[j]);
			}
		}
	}
}
int main(){
	cin >> T;
	for(test_case=1; test_case<=T; test_case++){
		cin >> s >> n;
		strcpy(reward,s.c_str());
		Answer =0;
		calc(0,0);
		cout << "#" << test_case << " " << Answer<< endl;
	}
}
```


### 격자판의 숫자 이어 붙이기(2819)

- 4*4 격자판 (0~9 입력되어있음)
- 임의의 위치에서 출발, 동서남북으로 총 6칸 이동하며 각 칸에 적혀있는 숫자를 연속해서 적으면 7자리수가된다.
- (번거로움)갔던 자리를 다시 지날 수 있으며 0으로 시작하는 수를 만들 수도 있다.
- 격자판을 벗어나는 이동은 가능하지 않다.

- 풀다보니 DFS가 더 적절하다는 걸 알게됨...
- 왜 이렇게 의지가 안생길까... 잠시 휴식기를 가지자.