## typedef vs using(별칭 선언)



C++11 후로는 using  이라는게 가능하게 됩니다.

```c++
typedef std::unique_ptr<std::unordered_map<std::string, std::string>> UPtrMapSS;
using UPtrMapSS = std::unique_ptr<std::unordered_map<std::string, std::string>>;
```



이 둘의 차이를 두고 질문이 오가는데 using 사용을 권장하는 이유 는 포인터 관여시 using이 더 이해하기 쉽다는 점, using은 템플릿화가 가능하다는 점이 있습니다.

```c++
typedef void (*FP)(int, const std::string&);
using FP = void (*)(int, const std::string&);

template<typename T>
using AllocWList = std::list<T, MyAlloc<T>>;

AllocWList<Some> some;

// Code from 'Effective Modern C++'
```

