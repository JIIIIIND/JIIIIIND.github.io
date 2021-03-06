---
title: "프로토타입 패턴"
date: 2019-11-03 23:52:24 +0900
categories: DesignPattern
---

### 개요

>원형이 되는 인스턴스를 사용하여 생성할 객체의 종류를 명시하고, 이렇게 만든 견본을 복사해서 새로운 객체를 생성합니다.<br> -Gof의 디자인 패턴, 169쪽

### 동기

예를 들어 게임에 나오는 몬스터마다 Ghost, Demon, Sorcerer 같이 클래스를 만들어 보자.
* 한 가지 스포너는 한 가지 몬스터 인스턴스만 만든다고 하자
1. 스포너 클래스의 상속 구조는 몬스터 클래스의 상속 구조를 따라가게 된다.
2. 반복되는 코드가 많고 클래스도 많아지게 된다.
* 프로토타입 패턴으로 해결
1. 핵심은 어떤 객체가 자기와 비슷한 객체를 스폰할 수 있다는 점
2. 상위 클래스인 Monster에 추상 메서드 clone()을 추가
3. 하위 클래스에서는 자신과 자료형과 상태가 같은 새로운 객체를 반환하도록 clone()메서드를 구현

### 결과

#### 현실

>패턴을 써도 코드 양이 많이 줄지 않으며 현실적이지가 않다. 요즘 나오는 게임 엔진에서는 몬스터마다 클래스를 따로 만들지 않는다.<br>

클래스 상속 구조가 복잡하면 유지보수가 힘들기 때문에 개체 종류별로 클래스를 만들기보다 [컴포넌트]()나 [타입 객체]()로 모델링 하는 것을 선호한다.

### 프로토타입 언어 패러다임

#### Self

>Self는 객체 지향 프로그래밍에서 할 수 있는 걸 다 할 수 있지만 클래스가 없다.

* 상태와 동작을 같이 묶어놓은 것을 OOP
* 클래스 기반 언어는 상태와 동작 사이에 분명한 구별이 있다.
 1. 상태는 인스턴스에 들어 있고, 동작은 클래스에 있다.
* Self에는 이런 구별이 없다. 무엇이든 객체에서 바로 찾을 수 있다.<br>

* 클래스 기반 언어에서의 상속
 1. 다형성을 통해 코드를 재사용하고 중복 코드를 줄일 수 있다는 장점이 있다.
* 클래스 없이 이런 일을 수행하기 위해 셀프에는 위임(delegation) 개념이 있다.
 1. 해당 객체에서 필드나 메서드를 찾아보고 있으면 쓰고 없으면 상위 객체에서 찾는다.
 2. 상위 객체는 그냥 다른 객체 레퍼런스일 뿐이다.<br>
 3. 상위 객체를 살펴보고 없으면 상위 객체의 상위 객체에서 찾아보고, 이를 반복한다. <br>
 4. 다시 말해 찾아보고 없으면 상위 객체에 위임한다.<br>

* 클래스의 또 다른 역할은 인스턴스 생성
 1. 언어마다 다르지만 대부분 new를 통해 객체를 새로 만들 수 있다.<br>
* 클래스가 없기 때문에 Self에서는 프로토타입 패턴에서 본 것처럼 복제를 한다.<br>

### 데이터 모델링을 위한 프로토타입

프로토타입이 단점만 있는건 아니다.
* 시간이 지날수록 게임에서 코드보다 데이터가 차지하는 용량이 커지고 있다.<br>
* 기획자는 몬스터와 아이템 속성을 파일 어딘가에 정의해야 한다.<br>
* 이럴 때 많이 사용하는 방법 중 하나가 JSON
 1. 예를 들어 고블린은 이런 식으로 정의 될 수 있다.

```json
{
	"이름": "고블린 보병",
	"기본체력": "20",
	"최대체력": "30",
	"내성": ["추위", "독"],
	"약점": ["불","빛"]
}
```

 * 고블린 형제들도 다음과 같이 데이터로 만들 수 있다.

```json
{
    "이름": "고블린 마법사",
    "기본체력": "20",
    "최대체력": "30",
    "내성": ["추위","독"],
    "약점": ["불","빛"],
    "마법": ["화염구", "번개 화살"]
}

{
    "이름": "고블린 궁수",
    "기본체력": "20",
    "최대체력": "30",
    "내성": ["추위","독"],
    "약점": ["불","빛"],
    "공격방법": "단궁"
}
```

* 개체에 중복이 많은 것을 알 수 있다.
1. 코드였다면 Goblin 추상 자료형을 만들어 재사용
2. JSON에는 이런 개념이 없다.
* 객체에 '프로토타입' 필드가 있어서, 여기에서 위임하는 다른 객체의 이름을 찾을 수 있다고 하자.
1. 첫 번째 객체에서 원하는 속성이 없다면 프로토타입 필드가 가리키는 객체에서 대신 찾는다.
2. 프로토타입 필드는 실제 데이터가 아닌 메타데이터

```json
{
    "이름": "고블린 보병",
    "기본체력": "20",
    "최대체력": "30",
    "내성": ["추위","독"],
    "약점": ["불","빛"]
}

{
    "이름": "고블린 마법사",
    "프로토타입": "고블린 보병",
    "마법": ["화염구","번개 화살"]
}

{
    "이름": "고블린 궁수",
    "프로토타입": "고블린 보병",
    "공격방법": "단궁"
}
```

이런식으로 중복을 제거하여 몬스터나 아이템 등의 데이터를 쉽게 정의할 수 있다.