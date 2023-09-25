## Fstring & FName & FText

위 세가지는 언리얼 엔진에서 문자열들을 처리하는 클래스들 입니다. 이들의 간단한 차이점을 알아두는게 좋습니다.

### [FName](https://docs.unrealengine.com/4.27/ko/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/FName/)
- 문자열 사용에 있어서 상대적으로 가벼움
	+ 주어진 문자열이 재사용 되어도 데이터 테이블에 한번만 저장
	
- 대소문자 구별 없음
- 한번 지정 후 변경 불가능
- 이런 특징들로 인해 FName을 키로 지정해 찾는 연산이 많음


### [FString](https://docs.unrealengine.com/4.27/ko/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/FString/)
- 다른 두 클래스와 다르게 여러 조작이 가능한 클래스
- 여러 검색, 텍스트 조작, Sub String 추출 등의 기능을 제공
- 다른 두개의 클래스보다 상대적으로 무겁습니다.


### [FText](https://docs.unrealengine.com/4.27/ko/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/FString/)

- 로컬라이징을 위한 문자열 클래스입니다.
- UMG 등 여러가지 유저들에게 보이는 텍스트들은 이 클래스를 사용한다고 보시면 됩니다.