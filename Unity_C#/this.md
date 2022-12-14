# this

C#에서 this는 여러군데 사용되기에 다른 질문을 하다가 연계 질문으로 잠깐 들어올 가능성이 있습니다. 스쳐 지나가듯 물어보는? 그런 느낌이 되겠네요.


## 클래스의 현재 인스턴스 this

흔히 다른 언어에서도 지원하는 것으로 **클래스의 현재 인스턴스**를 가리키는 키워드입니다. 매개변수 이름과 클래스 필드가 이름이 같다면 this로 구분할 수 있게 됩니다.

클래스 내에서 클래스 필드를 사용할 때는 다 this가 생략된 경우라고 볼 수 있습니다.


## 생성자 this()

생성자의 이름은 클래스 이름과 동일해야 하며 void 형식이어야 합니다.

```cs
class MyClass
{
    int a;
    int b;

    public MyClass()
    {
        a = 10;
    }

    public Myclass(int b)
    {
        a = 10;
        this.b = b;
    }
}
```

다만 이 경우 너무 중복되는 코드들이 양산될 수 있어서 `this()` 생성자를 사용하는 것입니다. `this()`는 자기 자신의 생성자를 가리키며 이는 생성자에서만 활용이 가능합니다.

```cs
class MyClass
{
    int a;
    int b;

    public MyClass()
    {
        a = 10;
    }

    public Myclass(int b) : this()
    {
        this.b = b;
    }
}
```

`this()` 키워드는 생성자를 가리키기에 인자를 줘서 인자를 받는 다른 생성자를 가리킬 수도 있습니다.


## 정적 함수 파라미터의 this

```cs
public static void Shuffle<T>(this IList<T> list)
```

정적 함수 파라미터에 하는 this는 `확장 메서드`를 만드는데 사용되는 키워드입니다. 이를 활용하면 멤버 함수를 호출하듯 함수를 호출할 수 있게 됩니다.

```cs
List<MyClass> exList = new List<MyClass>();
//...
Shuffle(exList);  // 이렇게도 되고
exList.Shuffle(); // 이렇게도 된다! this 덕분에!
```

이런 식으로 클래스나 인터페이스를 확장할 수 있게 됩니다. 

다만 기존 클래스의 함수와 동일한 시그니처로 정의하면 호출되지 않게 됩니다. 이 이유는 확장 메서드는 컴파일 타임에 바인딩이 되는데 컴파일러가 함수 호출을 볼 때 인스턴스 함수를 먼저 보게 되고 그 다음 확장 메서드를 보게 됩니다. 때문에 확장 메서드가 우선순위에서 밀려 호출되지 않게 되는 것입니다.