## IsValid, == nullptr, check 차이

### IsValid

```cpp
FORCEINLINE bool IsValid(const UObject *Test)
{
	return Test && FInternalUObjectBaseUtilityIsValidFlagsChecker::CheckObjectValidBasedOnItsFlags(Test);
}
```

`IsValid`의 경우 단순 nullptr 체크 뿐 아니라 내부 플래그도 검사하는 작업을 거치게 됩니다.

```cpp
struct FInternalUObjectBaseUtilityIsValidFlagsChecker
{
	FORCEINLINE static bool CheckObjectValidBasedOnItsFlags(const UObject* Test)
	{
		// Here we don't really check if the flags match but if the end result is the same
		PRAGMA_DISABLE_DEPRECATION_WARNINGS
		checkSlow(GUObjectArray.IndexToObject(Test->InternalIndex)->HasAnyFlags(EInternalObjectFlags::PendingKill | EInternalObjectFlags::Garbage) == Test->HasAnyFlags(RF_InternalPendingKill | RF_InternalGarbage));
		PRAGMA_ENABLE_DEPRECATION_WARNINGS
		return !Test->HasAnyFlags(RF_InternalPendingKill | RF_InternalGarbage);
	}
};
```

내부 플래그는 Functor로 되어 있는데 `PendingKill`, `InternalGarbage`인지 체크하는 작업을 거치게 됩니다.



즉 **IsValid는 nullptr인지, 가비지인지, PendingKill인지 살펴보는 작업을 거칩니다.**



### check, ensure 등의 어써트 (Assert)

이런 Assert 함수들은 에디터에서만 동작하는 함수로 안의 내용이 true, false 인지에 따라 동작이 달라지게 됩니다. 이들은 포인터의 operator bool() 연산에 기반해서 결과를 내므로 결론적으로는 nullptr과 비교하는 것과 동일한 결과를 내게 됩니다.



단 빌드를 하게 되면 해당 코드는 사라지게 됩니다.
