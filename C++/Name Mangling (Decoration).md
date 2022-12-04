## Name Mangling (Decoration)

>Mangle : ~을 난도질하다 (파파고)



`Name Mangling`은 컴파일러가 함수나 변수의 이름을 임의로 변경하는 작업입니다. 이런 작업이 C++에서 일어나는 이유는 `함수 오버로딩`때문인데 만일 같은 이름의 함수들이 있고 시그니처들이 다르다고 할 때 컴파일러는 이들의 이름을 다르게 부릅니다.

- 만일 SomeFunc(), SomeFunc(int some) 가 있다고 하면

  - SomeFunc()는 컴파일러가 SomeFunc_ 로
  - SomeFunc(int some)는 컴파일러가 SomeFunc_i 로

  같은 이름으로 변경하게 됩니다.



> 이런 네이밍 규칙에 대해서 물어보지는 않겠지만 궁금하신 분들을 위한 [Wiki](https://en.wikipedia.org/wiki/Name_mangling) 링크입니다.



### C에서도 이런 Name Mangling는 있는가?

일단 C 에서는 함수 오버로딩이 없기에 이런 Name Mangling이 필요 없습니다. 다만 컴파일러에 따라 다르기는 한데 앞에 `_`를 붙이는 등의 작업을 하기는 합니다. 

한다 안한다에 대한 이야기는 여러 의견이 갈리는 모습이 있습니다. 어떤 곳에서는 하지 않지만 대부분의 경우 **C는 간단한 Name Mangling을 한다**라는 의견이 주류인 것 같습니다.

> 현재 이 C에 대한 내용을 제보받고 있습니다. 
>
> 컴파일을 한 뒤 확인을 하면 Mangling이 된 모습을 볼 수 있는데 이걸 확실하게 받침해줄 공신력 있는 자료가 필요한 상황입니다.



### extern "C"

해당 명령어는 컴파일 후 이후 내용을 C 처럼 만들어 주기에 C++에서 작성을 한다 해도 C 에서 사용할 수 있게 해주는 명령어 입니다. 

```C++
extern "C" int Some(int a)
{
    //...
}
```

