---
title: "01. 팩토리 매서드 패턴"
categories:
  - Design Pattern
tags:
  - Tech Study
  - Notes
---

## 팩토리 메서드 패턴(Factory Method Pattern)
객체지향 디자인 패턴이다. Factory method는 부모(상위) 클래스에 알려지지 않은 구체 클래스(Robot)를 생성하는 패턴이며. 자식(하위) 클래스가 어떤 객체(SuperRobot, PowerRobot)를 생성할지를 결정하도록 하는 패턴이기도 하다. 부모(상위) 클래스 코드에 구체 클래스 이름을 감추기 위한 방법으로도 사용한다.

* Factory Method라는 패턴 이름이 적절하지 못한데, 이름으로 인해 객체를 생성하는 메소드를 Factory method라 오해하는 개발자가 많이 있다

## 예시

<div class="notice">
  <h4>Robot(추상 클래스)</h4>
  <p>SuperRobot</p>
  <p>PowerRobot</p>

  <h4>RobotFactory(추상 클래스)</h4>
  <p>SuperRobotFactory</p>
  <p>ModifiedSuperRobotFactory</p>
</div>

* 즉, Robot 이라는 클래스를 RobotFactory에서 생성함

* RobotFactory 클래스 생성
public abstract class RobotFactory {
	abstract Robot createRobot(String name);
}

* SuperRobotFactory 클래스 생성
public class SuperRobotFactory extends RobotFactory {
	@Override
	Robot createRobot(String name) {
		switch(name) {
		case "super" :
			return new SuperRobot();
		case "power" :
			return new PowerRobot();
		}
		return null;
	}
}

SuperRobotFactory는 RobotFactory를 상속하고 있기 때문에, 반드시 createRobot을 선언해야함.

name으로 건너오는 값에 따라서 생성되는 Robot이 다르게 설계됨.

## 주의점
Factory Method가 중첩되기 시작하면 굉장히 복잡해 질 수 있다. 또한 상속을 사용하지만 부모(상위) 클래스를 전혀 확장하지 않는다. 따라서 이 패턴은 extends 관계를 잘못 이용한 것으로 볼 수 있다. extends 관계를 남발하게 되면 프로그램의 엔트로피가 높아질 수 있으므로 Factory Method 패턴의 사용을 주의해야 한다.

<img src="/assets/images/designPattern/FactoryMethod.svg" alt="FactoryMethod"/>