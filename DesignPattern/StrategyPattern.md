## 스트래터지(전략) 패턴 (Strategy Pattern)

`스트래터지 패턴`은 인터페이스를 통해 특정 행동들을 인터페이스로 묶고 이를 교환하면서 사용하는 패턴입니다. 

게임을 예시로 만일 캐릭터의 무기가 총, 칼이 있다고 하면 아래처럼 전략 패턴을 활용할 수 있습니다.

```cpp
// IWeapon.h
class IWeapon
{
public:
    virtual void Attack() = 0;
};

// Player.h
class Player
{
    IWeapon* Weapon;

    //... 만약 공격 키가 눌리면
    Weapon->Attack();
};

class Sword : public Weapon
{
    virtual void Attack() override
    {
        //.. 검을 휘두른다
    }
};

class Gun : public Weapon
{
    virtual void Attack() override
    {
        //.. 총을 쏜다
    }
};
```

이런 식으로 플레이어가 무기를 변경한다고 해도 무기들의 `IWeapon`의 정의만 알고 있으면 플레이어의 코드 변경 없이 교체가 가능합니다. 
즉, 구체적인 클래스와 알고리즘 사이의 결합도를 낮추는 디자인 패턴으로 구체 클래스를 수정하는 일이 줄어드는, 유지보수에 도움이 되는 디자인 패턴입니다.

### 스트래터지 패턴은...
사실 바로 정의를 이야기 하기 보다는 이를 활용한 본인의 프로젝트 예시를 드는게 좋아 보입니다.