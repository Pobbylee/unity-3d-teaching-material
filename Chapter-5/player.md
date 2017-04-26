### 플레이어 제작

만들어진 지형에 `Hierarchy`에서 `Create > 3D Object > Cube`를 눌러 큐브를 만들어줍시다.

![이미지4](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/4.png?raw=true)

`Scene`에서는 다음과 같이 출력됩니다.

![이미지5](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/5.png?raw=true)

`Player`라는 새로운 오브젝트를 만들어서 그 안에 지금 만든 `Cube`를 넣어주세요. 그리고 이름을 `Body`로 바꿔주세요.

이렇게 하는 이유는 `Player`를 움직이면 하위 오브젝트인 `Body`까지 움직이기 때문입니다. 이렇게 해주면 장점이 뭘까요? 하위 오브젝트들을 관리하기 쉬워진다는 장점이 있습니다. 또 명시적으로 `Player`안에 들어있기 때문에 `Player`의 것입니다를 알 수 있죠.

![이미지6](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/6.png?raw=true)

어이쿠 근데 사이즈가 크네요? 사이즈를 조금 줄여보고 끼어있는것이 보기 굉장히 좋지 않으니 약간 위로 올려봐요. 아래와 같이 값을 설정해주면 됩니다.

![이미지7](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/7.png?raw=true)

##### 물리 적용하기

이제 맵과 플레이어를 만들었으니 맵 위에 플레이어가 돌아다니는 것을 만들어보도록 합시다. 먼저 이러한 행동을 하기 위해서는 물리를 붙여야 합니다.

`Box Collider` 컴포넌트를 붙이게 되면 Box 형태의 물리 물체가 되게 되는데요. 우리는 이 컴포넌트를 통해 물리를 붙여보도록 하겠습니다.

아래와 같이 먼저 `Ground`와 `Player -> Body` 설정을 해주세요.

![이미지8](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/8.png?raw=true)

`Body`, `Ground`에 기존에 있던 `Mesh Collider`를 없애고 `Ground`에는 `Box Collider` 컴포넌트를 추가했습니다. `Mesh Collider`는 해당 모델의 크기만큼 정교하게 물리영역을 만들어주는 컴포넌트 입니다. 하지만 그만큼 연산을 잡아먹기 때문에 많이 남발하면 좋지 않습니다. 이 예제에서는 `Box Collider`를 사용하여 할 것이기 때문에 기회가 된다면 사용을 해보도록 하겠습니다.

그리고 `Player`에 `Rigid Body`와 `Box Collider`를 추가해주세요.

![이미지9](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/9.png?raw=true)

`Box Collider`는 알겠는데, 새로 추가한 `Rigid Body`는 무엇인지 모를거에요. `Rigid Body`는 `강체`라는 뜻으로 컴포넌트를 추가하면 물리의 영향을 받게 됩니다.

`Rigid Body`는 충돌할 때도 필요한데, 서로 다른 두 오브젝트가 충돌을 할 때 둘중 하나는 Rigid Body가 있어야 충돌처리가 됩니다. 굉장히 중요하니 까먹지마세요!

그리고 이제 실행하면 게임씬에서 바닥과 붙어있는 플레이어를 볼 수 있습니다.

##### 플레이어 움직이기

저번에 했던 `Input`을 사용하여 움직이는 소스코드를 만들어봅시다.

```csharp
using UnityEngine;

public class Player : MonoBehaviour {

	// new는 상속받은 변수를 무시하고 새로 작성.
	// transform과 rigidbody는 기존에 MonoBehaviour에 있으므로 무시하고 생성
	new Rigidbody rigidbody;
	new Transform transform;

	public float power;
	public float rotationSpeed;

	void Start() {
		// 이런 작업을 해주는 이유는 메모리에 캐싱을 해두기 위함.
		// 메모리가 캐싱이 안된 Monobehaviour에서 직접 사용한 오브젝트는 나중에 많이 사용할 때 부하가 일어남.
		rigidbody = this.GetComponent<Rigidbody>();
		transform = this.GetComponent<Transform>();
	}

	void Update() {
		Move();
	}

	void Move() {
		// 앞, 뒤 움직임은 한개만 체크되어야 한다.
		if(Input.GetKey(KeyCode.W)) {
			// transform.forward는 현재 각도상, 캐릭터의 앞을 가지고 있는 벡터.'
			// 즉 앞 * power를 하므로 앞을 향해서 가게 됨.
			// Time.deltaTime은 프레임에 따른 정확한 값을 매기게 해주는 값.
			rigidbody.AddForce(transform.forward * power * Time.deltaTime, ForceMode.Impulse);
		} else if(Input.GetKey(KeyCode.S)) {
			rigidbody.AddForce(-transform.forward * power * Time.deltaTime, ForceMode.Impulse);
		}

		// 왼쪽, 오른쪽 움직임은 한개만 체크되어야 한다.
		if(Input.GetKey(KeyCode.A)) {
			// 유니티에는 오일러값과 사원수 회전 값이 존재하는데, 이렇게 두개가 존재하는 이유는 오일러 현상을 방지하기 위함.
			// 오일러값으로 회전을 여러방향을 한번에 할 경우 오일러 현상이 발생한다.
			// 하지만 사원수 값으로 하게되면 현상이 발생하지 않는데 근데 우리는 한축으로만 회전하므로 상관없어서 오일러 값으로 사용함.
			Vector3 euler = transform.localEulerAngles;
			euler.y -= rotationSpeed * Time.deltaTime;
			transform.localEulerAngles = euler;
		} else if(Input.GetKey(KeyCode.D)) {
			Vector3 euler = transform.localEulerAngles;
			euler.y += rotationSpeed * Time.deltaTime;
			transform.localEulerAngles = euler;
		}
  }
}
```

`Move()`라는 함수안에 보면 움직임 동작을 따로 빼낸 것을 볼 수 있습니다. 좀 더 알아보기 쉬워졌죠?

가장 처음에 봐야될 부분은 앞, 뒤 움직임 부분입니다. 우리가 만들려고하는 것은 자동차와 같은 움직임 입니다. 자동차는 직선으로 움직입니다. 물론 각도에 따라서 다르게 움직이게 되는데 이 각도는 바퀴가 설정하게 됩니다. 즉. 앞을 보고있는 곳에 따라서 움직여야 한다는 것 입니다. 앞이 45도를 보고 있으면 45도로 직선 운동을 하도록요.

`Input.GetKey(KeyCode.W)` 코드블럭 내부를 보면, `rigidbody.AddForce(transform.forward * power * Time.deltaTime, ForceMode.Impulse)`라고 되어있네요.

`rigidbody`는 아까 강체라고 했죠? rigidbody가 의미하는 것은 플레이어 자신에 붙어있는 Rigidbody 컴포넌트를 의미합니다. 조금 시선을 위로 올려서 `Start()` 함수에 보면 `this.GetComponent<Rigidbody>()`를 대입하는군요. `GetComponent`는 컴포넌트를 가져오는 함수입니다. 즉 `this` 자기자신의 컴포넌트인 `Rigidbody`를 가져옵니다. `Rigidbody`가 없는경우 `NULL`이 리턴이 되어 들어갑니다.

`AddForce`는 `rigidbody`에 힘을 추가한다 라고 보면됩니다. 그 힘의 크기는 뒤에 있는 `transform.forward * power * Time.deltaTime` 만큼요. `transform.forward`는 아까 위에 언급했던 플레이어가 보고있는 방향값을 갖고있는 벡터값 입니다.

> 벡터는 기본 수학이니 알고계실꺼에요. 따로 다루진 않겠습니다.

벡터값에 `power`와 `Time.deltaTime`을 곱합니다. 근데 소스코드에서 `power`의 값을 지정해주는 부분은 없네요? 걱정마세요. 잠시후에 보게 될 거에요.

> `ForceMode.Impulse`는 힘을 주는 선택지가 몇가지 있는데, 그 몇가지중에 한개입니다. 한번 시간이 된다면 찾아보세요. 흥미로운 결과를 얻을 수 있을꺼에요.

자 그렇다는 것은 앞, 뒤로 가는 소스코드는 보고있는 방향과, 뒤로가는 소스코드에서는 -를 곱했으니 보는 방향의 반대값을 보고있겠죠? 즉 앞과 뒤를 향해 W, S키를 누르면 그만큼 힘을 준다는 뜻입니다. `AddForce`를 통해서 움직이게 되면 앞에 있는 다른 물체들은 밀리게 됩니다.

밑을 보게되면 왼쪽, 오른쪽 체크가 있습니다.
왼쪽 오른쪽 버튼을 누르면 각각 회전값을 넣어서 방향을 회전하게 됩니다.

소스코드를 저장하고, 이제 스크립트를 Player에 넣어봅시다. 아래와 같이 보일꺼에요.

![이미지10](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/10.png?raw=true)

어? 근데 보지못했던게 보이네요? Player 스크립트에 무언가 변수가 있습니다. Power라는 변수가 있네요? 입력도 가능하고. 아까 위에서 Power를 입력받는 곳이 없다고 했습니다. 근데 유니티에서는 스크립트 안에 `public` 변수를 선언하게 되면 에디터에서 값을 수정할 수 있게 된답니다. 값을 20정도 넣어보도록 합시다. 그리고 실행해서 움직여보세요.

> RigidBody의 Constaints
> Constaints는 해당 각도나 위치로 움직일 때 움직이지 못하도록 고정합니다.
> 해당 예제에서는 Freeze Rotation x,y,z 에 만들어줫는데 이러는 이유는 마찰로 인해서 x,y,z축으로 뒤집어지거나 하는 경우를 막기 위함입니다.

##### 근데 방향이 어디를 향하는지 잘..

방향이 어디를 가리키는지 잘 모르겠네요. 큐브를 하나 만들어서 정면을 표시해봅시다.

![이미지11](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/11.png?raw=true)

그리고 실행해서 움직여봅시다. 잘 보이나요?

![이미지14](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/14.png?raw=true)

> 필자는 플레이어가 잘 안보여서 라이트에 색깔을 변경했습니다. 따라하실분은 따라하셔도 됩니다.
>
> ![이미지12](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/12.png?raw=true)
