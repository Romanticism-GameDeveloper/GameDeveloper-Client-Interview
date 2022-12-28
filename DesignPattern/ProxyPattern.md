# 프록시 패턴 (Proxy Pattern)

> Proxy : 대리인, 대리권, 대리

`프록시`는 클래스를 이어주는 대리인 역할을 하는 클래스 입니다. 이를 활용한게 프록시 패턴인 것이죠.

![Proxy UML from Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/7/75/Proxy_pattern_diagram.svg/400px-Proxy_pattern_diagram.svg.png)

위 UML에서 객체 사용시 객체를 직접 호출하는게 아닌 프록시 클래스를 부르게 되고 프록시는 실제 역할을 하는 클래스에게 처리를 요구하는 패턴인 것입니다.

## 프록시 패턴의 장단점
- 장점
  - 실제 일을 하는 클래스와 구분 지을 수 있음
  - 사이즈가 큰 객체가 있을 시 로딩 전에 프록시 객체를 통해 참조 가능
- 단점
  - 로직이 복잡해지면서 코드 읽기가 좋지 않을 수 있습니다. 때문에 가급적 다른 해결법을 찾는게 좋습니다.
  - 객체 생성시 단계가 늘어나게 됩니다. 이로 인해서 빈번한 생성, 삭제에서는 메모리가 무거워 집니다.

## C++의 `vector<bool>`, 스마트 포인터도 프록시 패턴이다

[c++ vector 문서 참고](https://github.com/Romanticism-GameDeveloper/GameDeveloper-Client-Interview/blob/main/C%2B%2B/vector%EC%99%80%20%EA%B4%80%EB%A0%A8%ED%95%9C%20%EC%9D%B4%EC%95%BC%EA%B8%B0%EB%93%A4.md)

스마트 포인터의 경우에는 일반 포인터의 인터페이스를 유지할 수 있으면서 작업을 하게 됩니다. (operator ->, * 를 사용할 수 있는 점 등)



## 자료 출처
- [Proxy UML Image](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%ED%8C%A8%ED%84%B4)