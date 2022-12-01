### map vs unordered_map

둘 다 key, value 쌍으로 되어 있지만 내부 자료구조가 다르게 동작하게 됩니다. 

- map의 경우 [레드 블랙 트리](https://ko.wikipedia.org/wiki/%EB%A0%88%EB%93%9C-%EB%B8%94%EB%9E%99_%ED%8A%B8%EB%A6%AC)로 되어 있는 자료구조로 내부 원소들이 key에 따라 정렬됨
- unordered_map의 경우에는 해시 테이블이 기반으로 되어 정렬이 없음

자료구조의 차이로 인해서 map은 일반적으로 O(logN) 시간 복잡도를 가지게 되고 unordered_map의 경우에는 주로 O(1) 시간 복잡도를 가지게 됩니다. 다만 최악의 경우에는 O(N) 시간 복잡도를 가질 수 있습니다.



> 추가적으로 해시 함수는 역함수가 없습니다



### unordered_map과 체이닝(chaining)

해시함수를 통과한 뒤 값이 같은 경우가 있습니다. 이런 경우에는 리스트처럼 체이닝을 통해 관리를 하게 됩니다. 이로 인해서 최악의 시간 복잡도가 O(N)이 나올 수 있게 되는 것입니다.



> 또 추가적인 개선 방법으로는 [Open Addressing](https://en.wikipedia.org/wiki/Open_addressing) 이 있습니다.

이는 충돌 발생시 다른 자리에 저장하는 방법으로 Linear Probing, Quadratic Probing, Double Hashing 이 있습니다.

- Linear Probing은 해당 해시 값에 자리가 있다면 근처 빈 슬롯에 저장하는 것입니다.
  - hash(n), hash(n) + 1, hash(n) + 2 순서로 검색하며 만약 테이블의 끝에 간다면 다시 테이블 처음으로 돌아와서 검색합니다.
- Quardratic Probing
  - +1^2, +2^2, +3^2 의 방식으로 올라가게 됩니다.

- Double Hashing
  - 서로 다른 두 해시 함수를 사용하게 됩니다.



### 여기서 좋은 해시 함수는 무엇일까?

좋은 해시 함수는 [SUHA - Simple Uniform Hashing Assumption](https://en.wikipedia.org/wiki/SUHA_(computer_science)) 이라 해서 각 해시 Key가 균등하게 분배되는 것을 의미합니다. 이를 통해 해싱 충돌을 최대한 막는게 좋은 함수라는 뜻입니다.

다만 이는 이론적인 이야기로 해시 함수의 성능 분석때 사용하게 됩니다.