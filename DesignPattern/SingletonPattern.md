# Singleton Pattern

싱글톤 패턴은 많이 사용하는 경우가 많지만 필연적으로 '멀티스레드에서 어덯게 활용해왔나' 라는 질문이 따라오게 됩니다. 때문에 관련 경험이나 지식이 없어 자신있게 대답할 수 없다면 가급적 다른 디자인 패턴으로 질문을 유도하는게 좋습니다.

## 싱글톤 패턴의 정의

`싱글톤 패턴(Singleton Pattern)`은 클래스의 인스턴스를 한개만 가지게 하는 디자인 패턴입니다.
유니티의 C#에서는 이를 간단하게 제작할 수 있습니다.
```cs
public SingletonClass : Monobehaviour
{
    public static SingletonClass instance;

    private void Awake()
    {
        if(instance == null)
        {
            instance = this;
        }
        else
        {
            Destroy(this);
        }
    }
}
```

C++ 에서는 생성자를 private에 넣고 이를 사용하게 됩니다. 또한 대입, 복사와 관련한 연산을 삭제해주게 됩니다.
```cpp
class SingletonClass 
{
public:
    static Singleton& GetInstance() {
        static Singleton* singleton = new Singleton();
        return *singleton;
    }

private:
    SingletonClass() = default;

    SingletonClass(const SingletonClass&) = delete;
    SingletonClass& operator=(const SingletonClass&) = delete;
    SingletonClass(SingletonClass&&) = delete;
    SingletonClass& operator=(SingletonClass&&) = delete;
};

// code from Wikipedia
```

## 싱글톤 패턴의 사용 이유, 장점

일단 싱글톤 패턴을 활용한 클래스의 생명주기는 프로그램의 생명주기와 같게 됩니다. 프로그램이 메모리에 올라감과 동시에 함께 올라가고 프로그램이 종료될 때 사라지게 됩니다.
이런 점을 이용해 메모리에 한번만 올라간다는 특징 덕분에 여러 인스턴스의 생성을 통한 메모리 사용을 막을 수 있습니다.
또한 전역으로 메모리에 올라가기에 다른 인스턴스들에서도 자유롭게 접근이 가능하다는 장점이 있습니다.


## 싱글톤 패턴의 단점

이러니 저러니 해도 계속 메모리에 올라가 있어 사용하지 않을떄도 메모리를 점유한다는 단점이 있습니다. 또한 소멸에 대한 부분이 정의되지 않기에 C++ 환경에서 사용할 때 소멸된 객체에 대한 역참조 문제가 있을 수도 있습니다. 그리고 이 싱글톤 인스턴스가 null인지 항상 체크하게 되는 비효율성이 있을 수 있죠.

가장 큰 문제는 동시성 문제입니다. 멀티스레드 환경에서 인스턴스가 2개 생기는 경우도 있고 여러 스레드에서 참조할 때 동기화 처리를 해줘야 하는 번거로움이 있습니다. 이로 인해 버그 탐색도 어려워지게 됩니다.

> 멀티 스레드 환경에서 싱글톤 패턴 사용 경험에 대한 질문이 많습니다.