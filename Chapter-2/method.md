### 메소드 (Method)

메소드는 C,C++에서 사용했던 함수 (Function)와 비슷한 기능을 한다고 보면 되요.

```csharp
public void method(int a) {
  Console.WriteLine("{0}", a * a);
}
```

위의 메소드는 간단한 코드로 이루어진 매개변수가 들어오면 그 매개변수를 동일한 값으로 곱해주는 구문이에요.
한번 상세히 알아볼께요.

```csharp
액세스수준 선택적한정자 반환값 이름 (매개변수) {}
```

**액세스 수준**

액세스 수준에는 아래와 같은 3가지가 있습니다. (2가지 더 있는데 언급하지 않도록 하겠습니다.)

- `public` : 모든 액세스가 가능하게 됩니다. 즉 모든 곳에서 이 메소드에 접근이 가능하다로 보시면 됩니다.
- `protected` : 상속 받은 클래스나 인터페이스에 한해서만 접근이 가능하다는 것입니다.
- `private` : 오로지 자기 자신만 접근할 수 있습니다.

**선택적 한정자**

선택적 한정자에는 `abstract`, `sealed`, `virtual` 등이 있습니다.
이 값들은 나중에 차차 알아볼께요.

**반환 값**

반환 값에는 저번 시간에 공부했던 데이터 타입들이 들어갑니다.
단 반환값이 `void`가 아니면 `return` 메소드를 통해 값을 반환해주어야 하는데요. 아래와 같습니다.

```csharp
public void method1() {
  // return이 필요없음. void는 없다는 뜻.
}

public int method2() {
  return 0; //없으면 에러!
}
```

void가 아닌 다른 값들은 전부 리턴값을 써주어야 합니다.

**이름**

이름에는 자신이 적을 이름을 써넣으면 됩니다. 써넣은 이름으로 다른 곳에서 함수를 자유로이 호출 할 수 있습니다. 하지만 이름의 시작은 무조껀 영어 혹은 한글등 숫자나 특수문자는 되지 않습니다.

이 이름이 중복되면 안되냐구요? 되는경우가 있고 안되는 경우가 있습니다. 그것에 대해서는 마라톤에서 보도록 하겠습니다.

**매개 변수**

매개 변수에는 여러가지 값이 제한없이 들어갈 수 있습니다. 30개든 100개든 들어갈 수 있어요.
보통 4~5개는 넘지않습니다. 차라리 함수를 나눠버리는게 더 좋습니다.

---

위에서 메소드의 부분에 대해서 알아봤는데 이제 실제로 쓰는 예를 봅시다.
아래는 간단히 더하기 하는 코드를 다르게 써봤습니다.

```csharp
public int Plus(int a, int b) {
  return a + b;
}
```

파라미터 선언과 동시에 값을 넣어봅시다. 만약 값이 안넘어온다면 저 값이 쓰입니다.
Optional / Named 파라미터(Parameter) 라고합니다.

물론 C++과 같이 오른쪽 부터 순서대로 써주어야해요.

```csharp
public int Plus(int a = 4, int b = 0) {
  return a + b;
}
```

이런식으로 무제한으로 입력받을 수도 있어요.

```csharp
public int Plus(params int[] values) {
  int result = 0;
  for (int i = 0; i < values.Length; i++)
    result += values[i];

  return result;
}
```

### 실습

메소드는 중요한 개념이므로 한번 해보도록 합시다.
아래의 메소드의 빈칸에 알맞게 넣어서 실행해보도록 해요.


- 각각의 함수안에 설명을 보고 코딩을 해보세요.
```csharp
public int Plus(int a, int b) {
  // 덧셈해서 return 하는 코드를 작성하세요~
}

public int Minus(int a, int b) {
  // 뺄셈해서 return 하는 코드를 작성하세요~
}

public int Sub(int a, int b) {
  // 나눗셈해서 return 하는 코드를 작성하세요~
}

public int Mul(int a, int b) {
  // 곱셈해서 return 하는 코드를 작성하세요~
}
```

- 이름을 한번, int형 데이터를 무제한으로 받는 함수를 만들어서 이름과 int형 데이터의 합을 `return` 하는 함수를 만들어보세요.
