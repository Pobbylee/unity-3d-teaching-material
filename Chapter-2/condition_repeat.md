### 조건문

조건문은 2개만 알면 모든 프로그래밍을 할 수 있답니다. 바로 `if`, `switch` 에요.

- `if`

```C#
int score = 100;
string rank = "A";

if(score <= 50) {
  rank = "D";
} else if (score <= 70) {
  rank = "C";
} else if (score <= 90) {
  rank = "B";
} else if (score <= 100) {
  rank = "A";
}
```

이렇게 되면 rank의 결과값은 몇을 출력할까요? 맞습니다. A를 출력하게 됩니다.

`if`는 해당 조건을 true와 false로 판단하는 문법입니다. 즉 score는 100이기 때문에 가장 마지막 줄의 else if의 `score <= 100` 조건에 해당이 되죠. 그러므로 마지막줄의 if는 true를 연산을 하여 `{}`[^1] 안에 진입하게 됩니다.

위의 소스처럼 조건을 한개만 써서 깔끔하게 표현되지 않는 것들은 어떻게 표현해야 할까요?

```C#
bool isClicked = true;
bool isUsed = true;
bool isHave = true;

int damage = 100;

if(isClicked == true && isUsed == true && isHave == true) {
  damage += 500;
}

if(isClicked == false || isUsed == false || isHave == false) {
  damage = 100;
}

```
위의 예제는 대충 아이템을 가지고있고, 사용중에, 버튼을 누르면 그 때 데미지가 올라가는 코드입니다. 이런식으로 여러가지 조건을 `&&` 을 통해서 한번에 적용되도록 할 수 있습니다. 한글로 말하면 `그리고` 가 어울리겠네요.

두번째 조건문은 `||` 를 사용하는 예제인데요. 이 `||`는 `혹은`을 나타냅니다. 즉 isClicked, isUsed 그리고 isHave 중 하나가 false가 되기만 한다면 원상복귀 되는 소스입니다.

> 이렇게도 내타낼 수 있어요.
> ```C#
> if(isClicked) {
>   // 코딩
> }
> ```
> 이렇게 하면 isClicked == true와 같은 문장입니다.
> 앞에 !를 붙인다면 isClicked == false와 같겠죠?

---

- `Switch`

```C#
int score = 100;
bool isPerfect = false;

switch(score) {
  case 100:
    isPerfect = true;
    break;
  default:
    isPerfect = false;
    break;
}
```

위의 소스코드는 간단하게 만점을 체크하는 코드입니다. 딱봐도 이해가 가능하죠?

---

### 반복문

반복문은 for, while 이 두개만 알면 되지만 보통 while은 잘 쓰지 않는답니다.

- `for`

```C#
for (int i = 0; i < 10; i++) {
  // 코드
}
```

위의 예제는 for문을 단순 10번 반복시키는 코드입니다.
조금 변형 시켜볼까요?

```C#
List<int> list = new List<int>;
list.Add(10);
list.Add(20);
list.Add(30);

for (int a in list) {
  // a는 list를 순차적으로 돌아 list[0]부터 끝까지 루프마다 대입됩니다.
}
```

이 코드는 list등의 collection들의 데이터를 순차적으로 도는 코드입니다.

- `While`

```C#
int loop = 0;

while(loop < 100) {
  loop ++;
}
```

이 소스코드는 loop가 100이 되면 루프가 멈추는 소스코드에요.
while은 괄호안의 데이터가 true일때만 동작한답니다.

즉 `loop < 100`는 true인 상태로 내부 소스가 loop++이므로 더해지는것이 멈추는 것은 100이 되면 멈추겠죠?

[^1]: `코드블럭` 이라고 합니다.
