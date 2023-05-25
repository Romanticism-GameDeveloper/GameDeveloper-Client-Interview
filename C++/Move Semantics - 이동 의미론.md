# Move Semantics - 이동 의미론


C++ 11부터 들어오게 된 중요 개념으로 기술면접 시작으로 나오기도 하는 질문입니다. 이전 C++ 에서는 복사만을 사용했기에 생성이나 대입에 있어서 연산이 느렸습니다. 하지만 C++ 11 후로부터 `&&`연산자를 통한 r-value 참조가 되게 됩니다. 이를 이용해서 기존 객체가 실제로 이동하는게 아닌 객체를 가리키는 포인터의 이동이 있는 것입니다. 타 언어에서의 얕은 복사라고 생각하면 됩니다.

이를 사용하기 위해서는 각 객체, 클래스에 이동 생성자, 이동 대입 연산자가 정의되어 있어야 사용이 가능합니다.

앞서 말한 '객체 이동이 아닌 포인터의 이동'이라는 점 때문에 이전에 소유하고 있는 객체가 포인터를 들고 있으면 한쪽에서 delete를 할 때 dangling pointer문제가 생길 수 있습니다. 때문에 이전에 소유하던 객체는 nullptr을 가지게 만드는 편입니다.



[이와 관련한 Stackoverflow의 좋은 글](https://stackoverflow.com/questions/3106110/what-is-move-semantics)



## std::move의 역할

std::move는 실제 이동을 해주는 함수가 아닌 l-value를 r-value로 바꿔주는 역할을 합니다. 이를 통해서 이동 연산자가 정의되어 있는 경우 변경된 r-value로 오버로딩이 될 수 있는 것입니다.	

대략 아래 코드의 느낌이라고 보시면 됩니다.

```c++
template<typename T>
typename remove_reference<T>::type&& move(T&& param)
{
	using ReturnType = typename remove_reference<T>::type&&;
	
	return static_cast<ReturnType>(param);
}

// C++ 14 이후
template<typename T>
decltype(auto) move(T&& param)
{
	using ReturnType = remove_reference_t<T>&&;

	return static_cast<ReturnType>(param);
}
```
예시코드입니다.
```
  // push_back(const T&) 가 오버로딩 되어서 문자열의 복사가 발생한다.
  v.push_back(str);
  std::cout << "After copy, str is \"" << str << "\"\n";

  // push_back(T&&) 가 오버로딩 되서 문자열의 복사 없이 그대로 전달된다.
  v.push_back(std::move(str));
```

때문에 실제로 하는 일은 move 가 아닌 rvalue_cast 입니다.



## std::forward의 역할

std::forward의 경우에는 move와 다르게 오른값일때는 오른값으로 전달, 왼값일 때는 왼값으로 전달하는 역할을 합니다.



> std::forward는 어떻게 왼값, 오른값을 알 수 있는가?

```c++
template<typename T>
T&& forward(typename remove_reference<T>::type& param)
{
	return static_cast<T&&>(param);
}
```

std::forward는 C++의 템플릿 매개변수 연역 방식을 통해 알아내게 됩니다. 여기서 C++은 원래 참조에 대한 참조는 안되지만 **특정 문법에서는 참조에 대한 참조가 허용됩니다. 그게 템플릿 인스턴스화 입니다.** 그리고 추가적으로 C++ 에서는 **연역 과정에서 둘 중 하나라도 l-value 참조라면 결과는 l-value 참조**가 된다는 규칙이 있어 std::forward는 이런 전달을 할 수 있는 것입니다.



아래 코드를 보면 어느정도 이해할 수 있게 됩니다.

- Some& 가 전달된 경우

    ```C++
    Some& && forward(typename remove_reference<Some&>::type& param)
    {	
        return static_cast<Some& &&>(param);
    }
    ```

- Some&& 의 경우에는 T가 Some로 연역됨



## move 대신 다 forward 쓰면 되는거 아닌가?

move와 forward의 차이는 forward는 조건에 따른 캐스팅을 한다는 이야기입니다. 때문에 다 move의 존재 의의를 묻게 됩니다.

일단 move의 경우는 사용이 편하고 코드의 명확성이 좋아집니다. 둘의 역할도 약간의 차이가 있는것이 move의 경우는 이동 준비가 목적이고 forward의 경우는 전달이 목적입니다. 때문에 이런 구별되는 이름을 두는게 바람직합니다.
