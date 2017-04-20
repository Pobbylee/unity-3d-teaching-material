### 클래스 (Class)

클래스는 `class` 로 사용하시면 되요.

```csharp
public class programmer {
  private string name = "마광휘";
  private int age = 23;

  public string isName {
    return name;
  }

  public int isAge {
    return age;
  }
}
```

클래스 안에 클래스를 만들어서 쓸 수 있습니다.

```csharp
public class Programmer...
public class Artist...
public class Producer...

public class job {
  private Programmer programmer;
  private Artist artist;
  private Producer producer;
}
```

그 안에 정보도 가져올 수 있어요.

```csharp
public class programmer {
  private string name = "마광휘";
  private int age = 23;

  public string isName {
    return name;
  }

  public int isAge {
    return age;
  }
}

public class job {
  private Programmer programmer;
  private int result;

  void plus() {
    result = programmer.age + programmer.age;
  }
}
```

### 생성자와 소멸자 (Constructor & Destructor)

클래스는 생성자와 소멸자를 가지고 있어서 생성될 때와 파괴될 때 소스코드를 통해서 컨트롤 할 수 있어요.

생성자와 소멸자는 각각 똑같은 이름을 써주고 `()`를 해주면 `생성자`, 앞에 `~`와 `()`를 해주면 `소멸자`에요.

```csharp
public class programmer {
  private string name = "마광휘";
  private int age = 23;

  public string isName {
    return name;
  }

  public int isAge {
    return age;
  }

  // 생성자
  public programmer() {
    name = "으아악";
    age = 30;

    // 출력 해보기
  }

  // 소멸자
  public ~programmer() {
    name = "호엑";
    age = 444;

    // 출력 해보기
  }
}

main() {
  public programmer pro = new programmer();
}
```

요로코놈 `생성자`에 페러미터도 넣을 수 있습니다.

```csharp
public class programmer {
  // 생성자
  public programmer(string _name, int _age) {
    name = _name;
    age = _age;

    // 출력 해보기
  }
}

main() {
  public programmer pro = new programmer("이름", 19);
}
```
