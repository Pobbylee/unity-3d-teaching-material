#
## 상속 (Inheritance)

C# 에서는 상속을 이렇게 할 수 있어요.

```csharp
public class job...

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
public new void A()) {
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

클래스를 분할시켜서 각각 다르게 구현할 수도 있습니다.
클래스를 분할시킬 때는 클래스가 길어지거나 할 때, 변수선언을 따로 해주고 싶을때 해주시면 됩니다.

```csharp
partial class partialClass {
public void test() {
Console.WriteLine("1");
}
}

partial class partialClass {
public void test1() {
Console.WriteLine("2");
}
}

partial class partialClass {
public void test2() {
Console.WriteLine("3");
}
}

main() {
partialClass pc = new partialClass();
pc.test();
pc.test1();
pc.test2();
}
```

클래스 안에 클래스를 쓸 수도 있습니다. 다만 클래스 안에 있는 클래스 (Inner class라고 합니다.) 가 래핑한 클래스의 데이터에 접근을 바로하진 못합니다. 하기위해서는 데이터를 받아와야 합니다.

```csharp
public class A {
public void a() {
Console.WriteLine("A");
}

public class B {
public void b() {
Console.WriteLine("B");
}
}
}

main() {
A a = new A();
A.B b = new A.B();

a.a();
b.b();
}
```

다중 상속은 안되요. 하기 위해서 `interface`를 써야되요.

```csharp
public interface IJob..
public interface IIT...

public interface IProgrammer : IJob, IIT...

public class Programmer : IProgrammer {
// job, IT, IProgrammer의 상속받은 함수들 사용.
}

```

보통 인터페이스는 위와 같이 앞에 I를 붙여주며. `interface`는 내부에 클래스처럼 변수를 사용할 수 없어요.

그러므로 다중상속을 해주려면 위처럼 거쳐야 합니다. `interface` 추후에 매우 요긴하게 쓰이고 구조 잡을대도 쓰이기 때문에 개인적으로 많이 연습하셔야 될 꺼에요.
