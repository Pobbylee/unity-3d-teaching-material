### 델리게이트와 이벤트(Delegate & Event)

 `delegate`는 대리자입니다. 우리가 뭔가를 던지면 그것을 대신 해주는 메소드입니다.

 ```csharp
 delegate 반환형 이름 (매개변수..);
 ```

`delegate`는 아래와 같이 쓰입니다.

```csharp
public delegate int exampleDelegate(int a, int b);

int plus(int a, int b) {
  return a + b;
}

main() {
  exampleDelegate d1 = plus;
  exampleDelegate d2 = delegate(int a, int b) {
    return a - b;
  };

  Console.WriteLine("{0}", d1(20, 10));
  Console.WriteLine("{0}", d2(20, 10);
}
```

`delegate`는 함수를 담는데 많이 쓰여요. 다른 클래스에서 다른 클래스, 다른 네임스페이스에서 네임스페이스 단위로 함수를 단위로 쓰거나 하는데 요긴하게 쓰입니다.

이렇게 여러 메소드를 한번에 호출할 수도 있어요. 이런 방법을 `Delegate Chain` 이라고 합니다.

```csharp
public delegate int exampleDelegate(int a, int b);

int plus(int a, int b) { return a + b; }
int minus(int a, int b) { return a - b; }
int mul(int a, int b) { return a * b; }
int sub(int a, int b) { return a / b; }

main() {
  exampleDelegate d = (exampleDelegate)Delegate.Combine(new exampleDelegate(plus),
  new exampleDelegate(minus), new exampleDelegate(mul), new exampleDelegate(sub));

  d(10, 10);
}

// 20, 0, 1, 100
```

`delegate`는 `event`를 이용하여 발생시킬 수 있습니다. 아래처럼요.

```csharp
public delegate void eventHandler (int data);

class A {
  public event eventHandler Active;
  public void DoAction(int val) {
    Active(val);
  }
}

public void Handler(int data) {
  Console.WriteLine(data);
}

main() {
    A a = new A();
    a.Active += new eventHandler(Handler);

    for (int i = 1; i< 100; i++) {
      a.DoAction(i);
    }
}

// 1 ~ 99 까지 출력됨.
```

`Class` A에 Active 이벤트에 main에서 eventHandler를 추가해줫습니다. 이 말은 event에는 delegate를 지정할 수 있고 넣었다가 뺏다가 할 수 있다는 말인데요. 굉장히 유용하다는 것을 볼 수 있는 예제입니다.

사용 예를 들자면 마이너스 연산이 필요할 때에 넣었다가 빼고 덧셈연산 할때 넣고 해서 코드 줄을 줄일 수 있는 효과가 있다는 말입니다.

### 실습

 - `event`에 `delegate`를 여러개 등록하는 방법을 한번 공부해보세요.
