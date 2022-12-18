## 널 오브젝트 패턴

객체를 활용하는 경우에 어디선가 객체를 구해오면 이게 null인지 아닌지를 체크할 필요가 있습니다. 이 경우 코드가 상당히 보기 싫어지게 됩니다.

때문에 이런 경우에 객체를 반환하는 함수에서 null을 반환하는게 아닌 null과 의미가 유사한 `널 오브젝트`를 반환하는 것입니다.

이 반환되는 `널 오브젝트`는 실제로 null이 아닌 객체지만 **하는 일은 없는 객체**를 의미합니다. 만일 경험치를 줘야 하는 객체인데 NullExp 객체를 반환하면 경험치를 주지 않는 작업을 한다고 합시다.

```cs
Exp exp = DB.GetMonsterExp("MonsterName");
if(exp != null)
{
    exp.GiveExpToPlayer(player);
}
```

이런 코드에서 널 오브젝트 패턴을 활용하면

```cs
Exp exp = DB.GetMonsterExp("MonsterName");
// NullExp 객체는 아무 일도 안하기에 플레이어에게 경험치를 주지 않는다
exp.GiveExpToPlayer(player);
```

이런 식으로 코드를 짧게 가져갈 수 있다는 것입니다. 즉, null 여부를 검사하지 않는 코드를 만들 수 있는 것이죠.