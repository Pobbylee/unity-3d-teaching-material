### 델리게이트 (Delegate)

 `delegate`는 대리자입니다. 우리가 뭔가를 던지면 그것을 대신 해주는 놈이라고 보면 됩니다.

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

`delegate`는 
