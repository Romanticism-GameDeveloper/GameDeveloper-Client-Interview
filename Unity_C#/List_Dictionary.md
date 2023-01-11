## List와 Dictionary

> C++에 대한 지식이 있다면 List는 vector, Dictionary는 unordered_map으로 생각하면 편합니다.

보통 면접에서는 List, Dictionary같은 C#의 컨테이너 클래스들을 사용해 봤는지 물어보게 됩니다. 그런 다음 내부 자료구조, 연산들에 대한 시간복잡도 이야기들이 오갈 수 있으니 알아두는게 좋습니다.

### 내부 자료구조

| 컨테이너              | 자료구조       |
| --------------------- | -------------- |
| `List<>`              | 배열           |
| `SortedSet<>`         | 레드-블랙 트리 |
| `HashSet<>`           | 해시 테이블    |
| `Dictionary<,>`       | 해시 테이블    |
| `SortedList<,>`       | 배열           |
| `SortedDictionary<,>` | 레드-블랙 트리 |



### List는 C++의 vector와 유사하다

`List`는 C++의 `vector`와 유사하게 동작하며 메모리에는 배열처럼 올라가게 됩니다. 또한 원소 삽입이 있을 때 `List`의 용량을 초과하게 되면 새 공간을 할당해 기존 원소들을 복사해 가기에 최대 O(N) 시간 복잡도를 가지게 될 수도 있습니다.

(Remove의 경우 따로 용량 변화가 없습니다)



### 그럼 SortedSet은 set, HashSet은 unordered_set 이다

C++과 비교를 하면 제목과 같은 이야기가 오게 됩니다. 

내부적으로 레드-블랙 트리를 사용하는 자료구조들의 경우 정렬된 완전 이진트리 이므로 삽입, 삭제에 있어서 O(logN) 시간이 소요되며 해시를 사용하는 자료구조들은 대부분 O(1)이지만 최악의 경우 O(N)이 될 수 있음을 알아야 합니다.

자세한 내용은 [C++에서 map과 unordered_map의 차이](https://github.com/Romanticism-GameDeveloper/GameDeveloper-Client-Interview/blob/main/C%2B%2B/map%20vs%20unordered_map.md)를 참고해 주세요.



### Dictionary vs SortedDictionary

대부분의 경우에서 성능은 `Dictionary`가 더 뛰어남을 알 수 있습니다. 오래 전이지만 [2008년의 자료](https://social.msdn.microsoft.com/Forums/vstudio/en-US/7513bbe6-5bd3-4309-8cca-7056043fb95a/sorteddictionary-vs-dictionary?forum=csharpgeneral)를 보면 50000만개 삽입에는 `Dictionary`가 3배 빠르고, 검색에는 아주 근소한 차이로 `SortedDictionary`가 빠름을 알 수 있었습니다.

때문에 항시 정렬된 상태로 데이터를 저장하는 것 외에는 `Dictionary` 사용이 더 좋습니다.