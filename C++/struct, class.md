## struct, class의 차이

- 기본 접근지정자가 class는 `private`, struct는 `public` 입니다.

- 초기화 방식에 대해서도 struct는 아래 초기화 방법이 가능하지만 class는 불가능합니다.

  ```c++
  struct SomeStruct
  {
      int var;
      int varPrivate;
  };
  
  class SomeClass
  {
      int var;
      int varPrivate;
  };
  
  int main(){
      SomeStruct someS = {1, 2};
      SomeClass  someC = {1, 2};  // ERROR
  }
  ```