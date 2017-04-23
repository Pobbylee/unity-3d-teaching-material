#
## 상속 (Inheritance)

C# 에서는 상속을 이렇게 할 수 있어요.

```csharp
public class job {}

public class programmer : job {

}
```

상속 값을 넘겨주는 방법을 한번 봐요.

```csharp
public class job {
  int salary;
  int years;
}

public class programmer : job{
  public programmer() {
    this.salary = 3500;
    this.years = 3;
  }
}
```

`sealed`를 통해 상속을 더이상 못시킬 수도 있어요. `sealed`를 통해서 하게되면 상속을 한 경우가 있다면 컴파일 에러가 발생합니다.

```csharp
sealed class job {
  int salary;
  int years;
}

public class programmer : job{
  public programmer() {
    this.salary = 3500;
    this.years = 3;
  }
}

// 실행하면 에러가 발생!
```

`virtual`과 `override`를 사용해서 똑같은 이름을 가진 함수라도 그냥 써버릴 수도 있어요.

```csharp
public class parent {
  public virtual void a() {
    Console.WriteLine("parent의 호출");
  }
}
public class child1 : parent {
  public override void a() {
    Console.WriteLine("child1 호출");
  }
}
public class child2 : parent {
  public override void a() {
    Console.WriteLine("child2 호출");
  }
}

main() {
  parent p = new parent();
  p.a();

  child1 c1 = new child1();
  c1.a();

  child2 c2 = new child2();
  c2.a();
}
```

`new`를 사용해서 부모 클래스의 멤버를 숨길수도 있어요.

```csharp
public class parent {
  public int a = 0;
  public void A() {
    Console.WriteLine("parent의 호출");
  }
}
public class child : parent {
  public new int a = 100;
  public new void A() {
    Console.WriteLine("child1 호출");
  }
}

main() {
  parent p = new parent();
  p.A();
  Console.WriteLine("{0}", p.a);

  child c = new child();
  c.A();
  Console.WriteLine("{0}", c.a);
}
```

다중 상속은 안되요. 하기 위해서는 `interface`를 써야되요.

```csharp
public interface IJob {}
public interface IIT {}

public interface IProgrammer : IJob, IIT {}

public class Programmer : IProgrammer {
  // job, IT, IProgrammer의 상속받은 함수들 사용.
}

```

인터페이스에 대해서는 나중에 다시 다뤄보도록 하겠습니다.

### 실습

 - 아래의 소스코드에 ???에 무엇을 넣어야 할까요?




 ```csharp
 class Unit {
   //???
 }

 class Marine : ??? {
   //???
 }

 class Ghost : ??? {  
   //???
 }

 main() {
   Unit[] list = new Unit[12];
   list[0] = new Marine(50, 6, 2);
   list[1] = new Ghost(45, 12, 4);

   list[0].hp = list[0].hp - 10;
   list[0].atk = list[0].atk + 1;
   list[0].range = list[0].range + 1;
   list[1].range = list[1].range + 2;
 }
 ```
