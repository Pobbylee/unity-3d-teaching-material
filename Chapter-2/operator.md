### 연산자 (Operators)

연산자는 수식연산자, 증감연산자, 조건연산자, 관계연산자 등.. 여러가지 연산자들이 존재하는데요.
언제까지나 이 수업은 유니티의 기본만 할 수 있도록 하는 자료이므로 상세하게 설명은 하지 않고, 수식연산자, 증감연산자, 관계 연산자 정도에 대해서만 알아볼께요.

---

- `수식연산자`

수식연산자는 기본적인 수식을 연산하는 기능을 제공하는 연산자를 말해요.

**덧셈**

```csharp
int a = 2;
int b = 3;

int result = a + b;
```

**뺄셈**

```csharp
int a = 3;
int b = 2;

int result = a - b;
```

**곱셈**

```csharp
int a = 3;
int b = 2;

int result = a * b;
```

**나눗셈**

```csharp
int a = 15;
int b = 5;

int result = a/b;
```

**나머지**

```csharp
int a = 15;
int b = 6;

int result = a%b;
```

---

- `증감연산자`

증감연산자는 1을 증가시키는 증가 연산자와 1을 감소시키는 감소연산자가 있습니다.

**전위 증가 연산자**

```csharp
int a = 10;
++a;
```

**전위 감소 연산자**

```csharp
int a = 10;
--a;
```

**후위 증가 연산자**

```csharp
int a = 10;
a++;
```

**후위 감소 연산자**

```csharp
int a = 10;
a--;
```
---

- `관계연산자`

관계 연산자는 연산 관계에 대해서 true, false를 반환하는 연산자입니다.

**>**

```csharp
int a = 10;
int b = 10;

bool chk = a > b;
```

**<**

```csharp
int a = 10;
int b = 10;

bool chk = a < b;
```

**>=**

```csharp
int a = 10;
int b = 10;

bool chk = a >= b;
```

**<=**

```csharp
int a = 10;
int b = 10;

bool chk = a <= b;
```

**==**

```csharp
int a = 10;
int b = 10;

bool chk = a == b;
```


**!=**

```csharp
int a = 10;
int b = 10;

bool chk = a != b;
```
