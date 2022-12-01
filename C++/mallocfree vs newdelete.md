## malloc/free vs new/delete

malloc/free는 함수, new/delete는 연산자인게 가장 큰 차이점입니다.

- malloc/free
  - #include "stdlib.h" 를 해줘야 사용 가능
  - malloc는 void 함수이기 때문에 반환받은걸 해당 타입의 포인터로 형변환을 해줘야 합니다
  - 생성자를 호출할 수단이 없기에 초기값을 줄 수 없다는 단점이 있습니다.
  - 역시 free의 경우에도 소멸자를 부르는게 아닌 함수 호출입니다.
  - malloc로 할당한 경우에는 `realloc`을 활용해 메모리 크기를 조정할 수 있습니다.
- new/delete
  - new/delete는 기본적으로 C++ 내 있는 키워드로 따로 include 할게 없습니다.
  - new를 했을 시에는 반환값이 해당 타입의 포인터로 자동 반환이 됩니다.
  - 생성자를 호출해 초기값을 줄 수 있습니다.
  - delete는 소멸자를 호출해 줍니다.
  - new 로 할당한 경우 직접적으로 메모리 크기를 조정할 수 없습니다.
    - 때문에 재할당이 많다면 malloc가 나은 방법이 될 수도 있습니다.

