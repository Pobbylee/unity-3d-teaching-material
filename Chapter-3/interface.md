### 인터페이스 (interface)

인터페이스는 아래와 같이 쓰입니다.

```csharp
interface 인터페이스명 {

}
```

쉽죠? 인터페이스는 클래스와 다른점이 있는데, 바로 멤버변수와 구현부를 가지지 않아요. 그렇다고 클래스와 아주 다르지도 않습니다. 모두 추상적으로 멤버로 만들어서 가시적, 또는 어떤 역할로 쓰는지 확실하게 명시적으로 나타내기 위해서 쓰는경우에 인터페이스를 사용하게 되요.

아래는 인터페이스의 특징입니다.

- 인터페이스는 다중 상속이 가능해요.
- 인터페이스 내에서는 필드를 포함할 수 없어요. `{}` 이런거요.
- 메소드, 인덱서, 이벤트, 프로퍼티 등을 사용 가능해요.
- 모든 멤버는 기본 접근 제한이 public 이에요.
- 모든 멤버는 추상적인 구현만 해놔야 합니다.
- 인터페이스는 다른 인터페이스 상속이 가능합니다.

다음은 인터페이스를 쓰는 예제입니다.

```csharp
public interface IStatus {
  int HP { get; set; }
  int MP { get; set; }
  int ATK { get; set; }
  int DEF { get; set; }
}

public interface ICharacter {
  int ID { get; set; }
  int SEX { get; set; }

  void hitBy(int damage, int idx);
}

public class User : IStatus, ICharacter {
  int hp, mp, atk, def;
  int id, sex;

  int HP { get { return hp; } set { hp = value; }}
  int MP { get { return mp; } set { mp = value; }}
  int ATK { get { return atk; } set { atk = value; }}
  int DEF { get { return def; } set { def = value; }}

  int ID { get { return id; } set { id = value; }}
  int SEX { get { return sex; } set { sex = value; }}

  public void hitBy(int damage, int idx) {
    if(idx == id) {
      hp -= damage;
    }
  }
}
```

위의 예제는 간단하게 인터페이스 다중상속을 받아서 자신에게 데미지가 들어올때 아이디 값을 맞나 체크를 한 후 데미지만큼 체력을 깎는 소스입니다.

다음과 같이 인터페이스는 인터페이스를 상속받을 수 있습니다.

```csharp
public interface IA {
  void methodA(int a);
}

public interface IB : IA {
  void methodA(string str);
  void methodB(string b);
}

public class A : IB {
  public void methodA(int a) {

  }
  public void methodA(string str) {

  }
  public void methodB(string b) {

  }
}
```

물론 인터페이스를 상속 받는다고 하여도 부모클래스의 내용도 클래스에서 구현부를 만들어줘야 합니다.
