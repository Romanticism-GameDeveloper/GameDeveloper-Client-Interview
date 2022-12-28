# L-value, R-value

간단한게 요약하면

- L-value는 메모리 위치를 참조하는 식
- R-value는 해당 표현식이 끝나면 더이상 참조할 수 없는 값

입니다. 여기서 모든 L-value는 R-value가 될 수 있지만 R-value는 L-value가 아닐 수도 있습니다.



## 이 둘의 어원

과거에는 연산자 = 를 기준으로 왼쪽에 있으면 L-value, 오른쪽에 있으면 R-value 라고 했습니다. 다만 이 말은 **정답이 아니며** 대충 이정도의 느낌의 어원이라 생각하면 됩니다.



## C++의 R-value reference

보통의 경우 `&`를 통한 참조(L-value reference)를 알게 되는데 C++11이후로는 `&&`을 통해 R-value Reference를 만들 수 있습니다.

이 `&&`를 통해서 C++의 move semantics, 스마트 포인터 등의 질문이 자연스레 갈 수 있습니다.