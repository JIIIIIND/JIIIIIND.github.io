---
title: "게임에서의 해킹"
date: 2020-01-05 20:33:10 +0900
categories: Learn
---

### 클라이언트 해킹

해커가 많이 쓰는 방법으로 다른 사람의 컴퓨터에 몰래 악성 프로그램을 심는 것

#### 악성 프로그램을 심는 방법

1. 이메일, 스마트폰 문자 메시지를 사용하여 악성 코드가 들어 있는 첨부 파일이나 인터넷 주소 전송
    * 이 프로그램으로 실행되고 있는 프로그램이나 디스크에 있는 내용을 도청하거나 조작
    * 멀웨어, 바이러스가 이에 해당
2. 운영체제나 응용 프로그램 의 결함을 이용해서 악성 프로그램을 전파
3. 사용자가 안일하게 설정한 보안 설정을 역이용해서 뚫고 들어감
    * 이러한 방식은 암호 알고리즘이 소용 없음    
    * 클라이언트 안에서 실행되는 프로그램 메모리 안에는 암호화되기 전 개인 정보가 이미 있기 때문

#### 해결 방법

- 항상 최신 소프트웨어를 유지
- 불필요한 보안 해제 하지 않고
- 알 수 없는 출처의 프로그램을 실행하지 않아야 함

### 서버 컴퓨터 해킹

 서버가 해킹당하면 모든 유저가 다 위험해지기에 더욱 조심해야 함

 클라이언트와 마찬가지로 서버 쪽 운영체제나 응용 프로그램 결함이나 보안 설정의 구멍을 이용하여 해킹하기에 앞서 말한 유지 관리를 해야 함

 추가적으로 서버 고유의 역할인 웹 서버나 DB 서버에서는 클라이언트와 다른 종류의 해킹을 추가로 예방해야 함
 * 대표적으로는 Query Injection이 있으며 다음에 설명함

#### 방화벽

 게임 서버는 일반 유저가 접속할 수 있는 리스닝 포트를 제외하고 모두 방화벽으로 막아야 함

 방화벽은 일종의 네트워크 기기로 여러 종류의 통싱니 오가는 것을 중간에서 감시하거나 불필요한 통신을 차단하는 역할을 함

 DB와 같은 일반 유저가 접속할 일 없는 서버는 일반 유저가 접속조차 할 수 없게 방화벽으로 막는 것이 좋음

### 게임 치트

 클라이언트에서 게임 플레이를 판단하는 것들은 쉽게 해킹을 당할 수 있지만 막는데 너무 집중하면 실시간 멀티플레이어 품질을 떨어뜨릴 수도 있으므로 절충하는 것이 중요함

 치트 역시 네트워크 공격, 즉 클라이언트 공격을 이용하는 것이 일반적임

#### 네트워크 도청 및 조작을 해서 해킹하는 경우
1. 플레이어가 공격을 할 때마다 '플레이어가 공격행동을 한다'라는 메시지를 서버에 전송
2. 해커는 이 메시지를 갈무리함. 그리고 이 메시지를 복제해서 서버로 전송
3. 서버에서는 이 메시지를 모두 처리. 해커의 캐릭터는 엄청난 속도로 다른 플레이어를 공격 가능

##### 해결방법
 서버에서 받는 메시지가 시간 차이도 유효한지 살펴보아야 함

#### DDOS와 유사한 공격
1. 해커는 정밀하게 조작하지 않아도 되는 캐릭터를 가지고 있음
2. 해커는 게임 서버나 다른 게임 클라이언트에 엄청난 양의 네트워크 데이터를 전송하여 멀티플레이어 품질 하락
3. 이 상태에서 해커의 캐릭터는 정밀 컨트롤이 필요한 유저들을 상대로 승부 우위를 차지함

#### 클라이언트를 해킹하여 치트를 하기도 함
- 클라이언트 내부 데이터를 조작하여 클라이언트에서 판정하는 승부 판정을 조작
- 메모리에 있는 다른 플레이어 정보를 얻어냄(FPS게임에서 벽 뒤의 플레이어를 찾을 수 있음)
- 게임 컨트롤러 조작

 이러한 종류의 해킹을 차단하려면 게임 클라이언트 프로그램 측에서 자신이 조작되고 있는지 알아내야 함. 즉, 이러한 해킹을 진행 중인 프로그램이 있는지 감시해야 함