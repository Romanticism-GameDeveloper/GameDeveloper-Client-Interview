## delegate & event

> delegate : 대표, 위임하다

### delegate (델리게이트)

C# 에서 델리게이트는 함수를 타입화 한 것입니다. C++ 에서 함수 포인터와 비슷한 개념이라고 생각하면 됩니다.
파라미터와 리턴 타입을 통해 정의하게 되며 이후 리턴, 파라미터 타입이 같은 메소드들과 호환되어 이 메소드들에 대한 참조를 가질 수 있게 됩니다.

```cs
public delegate void VoidAndIntEx(int i);

public class ExampleClass
{
    public void DoSomething(VoidAndIntEx exFunc)
    {
        // 인자로 받은 함수를 호출한다
        exFunc(1);
    }
}
```

C#에서 이런 델리게이트를 활용해 메소드를 담아두는 역할을 하거나 함수 인자로 넘겨 콜백 패턴을 구현하는 등 다양한 곳에 사용하게 됩니다.


### event

이벤트는 결국 델리게이트와 비슷한 일을 하게 되지만 한가지 큰 차이점이 **이벤트를 호출 할 수 있는건 해당 이벤트를 가진 클래스**만 가능하다는 것입니다.

```cs
class ExampleClass
{
    // Action에 대한 설명은 아래
    public event Action ExampleEvent;

    //...
    if(ExampleEvent != null)
    {
        ExampleEvent();
    }
}
```

### Action, Func, Predicate

이 키워드들은 자주 사용하게 되는 델리게이트를 템플릿화 한 것들입니다.

- Action<T> 
  - 함수 파라미터가 T 이고 반환값이 void 인 경우
- Func<T, TResult>
  - 함수 파라미터가 T 이고 반환값이 TResult 인 경우
- Predicate<T>
  - 함수 파라미터가 T 이고 반환값이 bool 인 경우


### null 조건부 연산자 (?.)

> null 체크 연산자 등의 말이 있지만 현재 문서에서는 [MS docs](https://learn.microsoft.com/ko-kr/dotnet/csharp/language-reference/operators/member-access-operators#null-conditional-operators--and-)의 표기를 따랐습니다.

델리게이트나 이벤트를 다루다 보면 null인지 체크를 해줘야 합니다. 만일 null인 델리게이트를 호출한다면 NullReferenceException이 발생하게 됩니다.

```cs
if(ExampleEvent != null)
{
    ExampleEvent();
}
```

위 코드에서 문제점은 2가지 있습니다.
- 멀티 스레드에서 호출할 경우의 문제
- 그냥 타자가 많다

멀티 스레드에서 문제는 복잡하게 됩니다. 위 코드에 주석을 달아 설명을 해 보겠습니다.

```cs
if(ExampleEvent != null) // 여기서는 문제 없었는데
{
    // 여기서 다른 스레드가 구독을 취소해서 null이 됨!
    ExampleEvent(); // NullReferenceException!
}
```

이런 복잡한 문제는 검출이 어렵기에 아래 '복사 후 실행' 이란 방법을 통해서 예방할 수 있습니다.

```cs
var CopiedEvent = ExampleEvent;

if(CopiedEvent != null)
{
    // 여기서 ExampleEvent 구독 취소 해도 문제 X
    CopiedEvent();
}
```

다만 이 경우 위에 언급한 '타자가 많다' 문제는 해결하지 못합니다. 매번 복사한다는것도 좋은 방안이 아니구요.

때문에 `?.` 연산자를 활용하는 것입니다. `?.` 연산자는 `?` 왼쪽의 항이 null이 아니라면 `.` 뒷부분을 실행하겠다는 의미의 연산자 입니다.

```cs
ExampleEvent?.Invoke();
```

함수의 경우 `Invoke`를 붙여서 호출할 수 있게 됩니다. 그리고 이 연산자의 경우 **원자적으로 수행이 되는 연산자**라서 이 연산 도중 다른 스레드가 개입할 여지가 없어 멀티 스레드 환경에서도 안전하게 돌아가게 됩니다.