### 스크립트 연동하기

유니티에서 스크립트 연동하는 작업은 간단합니다.

먼저 C# 스크립트를 하나 만듭시다. Controller 라는 이름으로요.

![이미지17](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/17.png?raw=true)

> VSCode는 상관없는 파일입니다. 맥에서는 비주얼 스튜디오가 없기 때문에 비주얼 스튜디오 코드를 사용하게 됩니다. 그런데 이 비주얼 스튜디오 코드는 완벽히 지원하는 툴이 아니기 때문에 유니티와 연동을 위해서는 이러한 파일이 필요합니다. 즉 윈도우를 쓰는 사람들은 관련이 없습니다. ㅠㅠ

이 스크립트를 열면 아래와 같은 화면이 나옵니다.

![이미지18](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/18.png?raw=true)

기본적으로 `Start`, `Update` 라는 메소드가 만들어집니다. 이 메소드는 유니티에서 중요한 역할들을 하는 메소드들 인데요 이런 메소드들을 `Life Cycle` 메소드라고 합니다.

그럼 간단하게 `Life Cycle` 메소드들이 어떤 일을 하고 뭐가 존재하는지 알아보도록 해요.

- `Awake` : Awake는 제일 처음에 호출된다고 보시면 되요. 즉 오브젝트가 만들어지고 가장 먼저 호출되는 메소드입니다.


- `OnEnable` : Awake가 호출되고 나서, 이 메소드는 켜져있다고 판단되면 호출이 되게 됩니다.


- `Start` : Start는 스크립트가 활성화 되고 첫 번째 업데이트 프레임이 시작되기 이전에 호출이 됩니다.


- `Update` : Update는 게임이 동작하는 동안 계속 돌아가는 영역입니다.

이제 이 메소드들을 직접 써봐야겠죠? 그리고 자세히 알아보도록 해요.

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Controller : MonoBehaviour {

	void Awake () {
		Debug.Log("Awake 호출!");
	}

	void OnEnable () {
		Debug.Log("On Enable 호출!");
	}

	void Start () {
		Debug.Log("Start 호출!");
	}

	void Update () {
    Debug.Log("Update 호출!");
	}
}
```

위의 소스코드처럼 작성을 해보고 저장해주세요.

> 여기서 공통적으로 쓰인 소스코드가 있는데요 바로 `Debug.Log` 입니다. 이 코드는 지난 시간에 뷰들을 한번씩 봤었는데요 그 중에 `Console` 이라는 뷰가 있었습니다. 그럼 뭘까요? 맞습니다. `Debug.Log` 라는 뷰에 `Awake`, `OnEnable`, `Start`, `Update`가 호출될 때마다 한줄씩 기록이 되게 됩니다.

> 또 중요한 한가지 팁!
> 맨위의 소스를 보면
> ```csharp
> using System.Collections;
> using System.Collections.Generic;
> ```
> 이 부분은 쓰지 않습니다. 그래서 아래에 밑줄이 생길꺼에요. 이때, 컨트롤 + . 를 눌러줍시다.
>
> ![이미지24](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/24.png?raw=true)
> Remove Unnecessary Usings를 눌러줍시다.
> 그러면 정의되어 있지만 쓰지 않는 라이브러리들이 제거가 된답니다.
> 또 에러부분에도 쓰면 에러에 대해서, 라이브러리가 안쓰여있는 곳에 하게되면 자동으로 라이브러리 추가까지 해줍니다. 꼭 기억하세요.


지난 시간에 3D 오브젝트 큐브를 한번 만들어봤었죠? (물론 첫강때 했습니다.) 근데 까먹었을 것 같아서 사진을 첨부합니다.

![이미지19](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/19.png?raw=true)

큐브를 만들어주시고, 큐브에 스크립트를 드래그 앤 드롭을 해주세요.

![이미지20](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/20.png?raw=true)

이렇게 컴포넌트를 추가할 수도 있지만 아래와 같이 `Add Component`로 추가 할 수 있습니다.

![이미지21](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/21.png?raw=true)

Play 버튼을 눌러 실행을 해주세요. 실행을 해주시면 `Console` 뷰에 아래와 같이 기록됩니다.

![이미지22](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/22.png?raw=true)

기록이 되는군요! 근데 `Update`는 계속 호출이 되니 보기가 어려워요. 그러므로 동일한 이름으로 기록된 것들을 축약 시켜봅시다. 왼쪽 상단의 `Collapse`를 눌러보세요.

![이미지23](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/23.png?raw=true)

`Collapse` : 같은 내용으로 기록된 것들을 횟수 단위로 축약을 해주고, 로그가 몇회 되었는지도 간단하게 볼 수 있게 지원합니다.

`Clear` : 현재 기록된 내용을 초기화 해줍니다.

`Clear on play` : 플레이시 기존 콘솔에 있던 내용을 `Clear`시킵니다.

`Error Pause` : 플레이시 에러가 나올 경우 중지를 자동으로 시킵니다.

콘솔의 버튼들이 어떤 역할을 하는지도 익혔고, 정상적으로 호출이 되는 것을 볼 수 있습니다.

호출 순서는 `Awake` -> `On Enable` -> `Start` -> `Update` 순서군요?

> 여기서 중요한 점은 플레이 버튼을 눌러 실행중 스크립트를 수정하면 안됩니다. 왜냐하면 스크립트 변경사항이 실행 중과 매칭이 되야 하는데 다르게 매칭이 되면 뻑이 나서 유니티 에디터가 팅기게 되요. 조심하셔야 합니다!

##### 간단하게 움직이는 예제 제작 해보기

어렵지 않은 큐브를 자유롭게 움직이는 예제를 만들어봅시다.

`Controller` 스크립트에 아래와 같이 추가를 해주세요.

```csharp
using UnityEngine;

public class Controller : MonoBehaviour {

	float speed = 2;

	void Update () {
		if(Input.GetKeyDown(KeyCode.LeftArrow)) {
			Vector3 vec = transform.localPosition;
			vec.x -= speed * Time.deltaTime;
			transform.localPosition = vec;
		}
	}
}
```

게임으로 돌아가서, 플레이 후 왼쪽 화살표를 연타해보세요. 그럼 움직이죠? 근데, 게임에서는 누르고 있으면 움직이는게 정상인데요 그렇게 해줘봅시다.

```csharp
void Update () {
	if(Input.GetKey(KeyCode.LeftArrow)) {
		Vector3 vec = transform.localPosition;
		vec.x -= speed * Time.deltaTime;
		transform.localPosition = vec;
	}
}
```

`GetKeyDown`을 `GetKey`로 바꿔줫어요. 이제 누르고 있으면 움직일꺼에요.

이번엔 왼쪽뿐만 아니라, 오른쪽, 위, 아래도 해보도록 합시다.

```csharp
void Update () {
	if(Input.GetKey(KeyCode.LeftArrow)) {
		Vector3 vec = transform.localPosition;
		vec.x -= speed * Time.deltaTime;
		transform.localPosition = vec;
	} else if(Input.GetKey(KeyCode.RightArrow)) {
		Vector3 vec = transform.localPosition;
		vec.x += speed * Time.deltaTime;
		transform.localPosition = vec;
	}
	if(Input.GetKey(KeyCode.UpArrow)) {
		Vector3 vec = transform.localPosition;
		vec.y += speed * Time.deltaTime;
		transform.localPosition = vec;
	} else if(Input.GetKey(KeyCode.DownArrow)) {
		Vector3 vec = transform.localPosition;
		vec.y -= speed * Time.deltaTime;
		transform.localPosition = vec;
	}
}
```

어때요 잘 움직이나요?

##### 실습

- 키보드를 때고 있으면 움직이고, 누르면 움직이지 않는 코드를 작성해보세요. 물론 이 코드는 모든 방향으로 되면 안되겠죠? 왼쪽으로만 움직이도록 해요.
