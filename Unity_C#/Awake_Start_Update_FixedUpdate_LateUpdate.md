
> 이 질문을 보기 전 사전 지식으로 [유니티 생명주기](https://github.com/Romanticism-GameDeveloper/GameDeveloper-Client-Interview/blob/main/Unity_C%23/Unity%EC%9D%98%20%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0.md)문서를 보는걸 추천드립니다.

# Awake vs Start

둘 다 클래스의 초기화에 사용되는 이벤트 함수로 호출 시기에 따른 차이가 있습니다. 

- Awake
  - 스크립트와 연결된 GameObject가 인스턴스화 되거나 스크립트가 처음 로드될 떄 불림
  - 해당 오브젝트가 Enable 상태가 아니라고 해도 위 조건에 따라 로드되면 호출됨
  - 다른 오브젝트에 대한 참조를 생성할 때 주로 사용하게 됨
    - 단 Awake 호출은 무작위
    - 무작위성으로 인해 다른 스크립트의 참조를 통해 접근을 하면 `NullReferenceException`이 발생하게 됨
- Start
  - 해당 스크립트 컴포넌트가 활성화 되는 순간 불리게 됨
  - 호출 시기는 Awake 보다는 느리게 첫 Update보다는 빠르게 불린다
  - Start에서는 참조를 통해 접근하는 작업이 가능함


## OnEnable vs Start

둘 다 '컴포넌트가 활성화 될 때' 불린다는 공통점이 있어 묶이게 되지만 Start는 한번, OnEnable은 활성화 될 때 마다 불리게 된다는 차이점이 있습니다. 때문에 초기화 작업에 OnEnable을 활용하면 안됩니다. OnEnable은 주로 오브젝트 풀링에 사용하게 되는 함수라고 볼 수 있습니다.


# Update vs FixedUpdate vs LateUpdate

- Update : 프레임 단위로 호출됨
- LateUpdate : Update 호출 뒤 불리게 됨
- FixedUpdate : 고정 단위로 불리게 되는 함수

여기는 FixedUpdate의 '고정 단위'를 아는게 중요합니다. 이 고정 단위는 물리 엔진에 의해 결정이 되므로 컴퓨터 성능에 따라 프레임이 다르게 나와 호출 간격이 일정하지 않은 Update와는 달리 일정하게 불리게 됩니다. 이런 이유로 인해서 Rigidbody를 조작할 때는 FixedUpdate를 사용하게 됩니다.