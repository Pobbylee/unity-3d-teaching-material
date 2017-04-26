### 총알 제작

총알 오브젝트를 아래와 같이 만듭니다. `Create > 3D Objects > Cube`를 만들어 사이즈를 줄여봅시다.

![이미지15](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/15.png?raw=true)

만들었으면 드래그하여 프로젝트로 끌어 넣습니다.

![이미지16](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/16.png?raw=true)

파란색의 `Bullet`이라는 이름의 오브젝트가 `Project` 안에 생성이 됐네요? 그리고 `Hierarchy`의 `Bullet`은 파란색 처리가 되었습니다. 이 파란색은 `Project`의 생성된 오브젝트와 연결이 되어 있다는 말입니다. 저장을 하면 `Project`의 오브젝트까지 변경이 되요.

이 오브젝트를 `Prefab (프리팹)` 이라고 부릅니다. 이 프리펩으로 뭘 할수 있냐면, 게임이 실행되는 도중에 이 프리팹 단위의 오브젝트들을 생성이 가능합니다. 생성을 해보도록 합시다. `Player`로 가서 소스코드를 수정해봅시다.

```csharp
using UnityEngine;

public class Player : MonoBehaviour {

	new Rigidbody rigidbody;
	new Transform transform;

	public float power;
	public float rotationSpeed;

	public GameObject bulletObject;

	void Start() {
		rigidbody = this.GetComponent<Rigidbody>();
		transform = this.GetComponent<Transform>();
	}

	void Update() {
		Move();
	}

	void Move() {
		if(Input.GetKey(KeyCode.W)) {
			rigidbody.AddForce(transform.forward * power * Time.deltaTime, ForceMode.Impulse);
		} else if(Input.GetKey(KeyCode.S)) {
			rigidbody.AddForce(-transform.forward * power * Time.deltaTime, ForceMode.Impulse);
		}

		if(Input.GetKey(KeyCode.A)) {
			Vector3 euler = transform.localEulerAngles;
			euler.y -= rotationSpeed * Time.deltaTime;
			transform.localEulerAngles = euler;
		} else if(Input.GetKey(KeyCode.D)) {
			Vector3 euler = transform.localEulerAngles;
			euler.y += rotationSpeed * Time.deltaTime;
			transform.localEulerAngles = euler;
		}

		if(Input.GetKeyDown(KeyCode.Space)) {
			CreateBullet();
		}
	}

	void CreateBullet() {
		 GameObject obj = Instantiate(bulletObject);
		 obj.transform.localPosition = Vector3.zero;
	}
}

```

아래를 보면 `CreateBullet()` 이 보이네요? 이 메소드는 `bulletObject`를 생성하게 됩니다. `bulletObject`는 상단에 `public GameObject bulletObject;` 이렇게 선언되어 있어요. 저번 강의에 설명했죠? `public`으로 선언했기 때문에 `Player.cs` 컴포넌트에 뷰로 추가 되었을꺼에요.

그럼 그 GameObject에 이렇게 넣어주세요.

![이미지17](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/17.png?raw=true)

아까 Project에 끌어다 넣었던 `Bullet`이 들어가있네요? `GameObject`형에는 스크립트를 제외한 `Prefab`등의 오브젝트 데이터들이 들어갈 수 있습니다.

이렇게 넣어주고, 아래를 보면 이해가 쉬울꺼에요. `CreateBullet()`을 보면 `GameObject obj = Instantiate(bulletObject);`가 있어요. 여기서 주의깊게 봐야 할 부분은 `Instantiate`입니다.

`Instantiate`는 `Prefab`을 생성하는 메소드에요. 즉 아까 `bulletObject`에 넣어둔 `Bullet Prefab`을 생성하는 구문이에요. `Instantiate`는 GameObject형으로 반환하기 때문에 생성한 `Bullet`은 obj에 들어가게 됩니다.

 `obj.transform.localPosition = Vector3.zero;`는 생성된 `Bullet`오브젝트의 포지션을 0으로 만드는 구문입니다. 이러면 화면 가운데에 나오겠죠?

실행을 해보면 정상적으로 화면 가운데에 나오는 것을 볼 수 있습니다. 하지만 우리는 어디에 생성되어야 하나요? 총알은 총구에서 나와야합니다. 즉 이렇게 나와야 겠죠.

![이미지18](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/18.png?raw=true)

진하게 표시된 부분에 생성을 해야됩니다. 지금 저 사진은 생성을 해 놓은 화면입니다.
그러면 어떻게 해야할까요? `BulletPosition`이라는 오브젝트를 만들어서 `Player`의 안에 넣어두면 `Player`가 회전해도 그 위치가 유지되기 때문에 쉽게 구현을 할 수 있겠네요?

새로운 `GameObject`를 만들어서 `BulletObject`로 이름을 변경해주고. `Player`안에 넣어서 포지션을 바꿔줍시다.

![이미지19](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/19.png?raw=true)

그리고 그 위치에서 생성되야 하니 소스코드를 바꿔봅시다.

```csharp
using UnityEngine;

public class Player : MonoBehaviour {

	new Rigidbody rigidbody;
	new Transform transform;

	public float power;
	public float rotationSpeed;

	public GameObject bulletObject;
	public GameObject bulletPosition;

	void Start() {
		rigidbody = this.GetComponent<Rigidbody>();
		transform = this.GetComponent<Transform>();
	}

	void Update() {
		Move();
	}

	void Move() {
		if(Input.GetKey(KeyCode.W)) {
			rigidbody.AddForce(transform.forward * power * Time.deltaTime, ForceMode.Impulse);
		} else if(Input.GetKey(KeyCode.S)) {
			rigidbody.AddForce(-transform.forward * power * Time.deltaTime, ForceMode.Impulse);
		}

		if(Input.GetKey(KeyCode.A)) {
			Vector3 euler = transform.localEulerAngles;
			euler.y -= rotationSpeed * Time.deltaTime;
			transform.localEulerAngles = euler;
		} else if(Input.GetKey(KeyCode.D)) {
			Vector3 euler = transform.localEulerAngles;
			euler.y += rotationSpeed * Time.deltaTime;
			transform.localEulerAngles = euler;
		}

		if(Input.GetKeyDown(KeyCode.Space)) {
			CreateBullet();
		}
	}

	void CreateBullet() {
		 GameObject obj = Instantiate(bulletObject);
		 obj.transform.localPosition = bulletPosition.transform.position;
	}
}

```

추가된 부분은 `public GameObject bulletPosition`, `obj.transform.localPosition = bulletPosition.transform.position;`이에요.

`bulletPosition`에는 `bulletObject`에 `Bullet`을 넣어줫던 것처럼 `bulletPosition`을 넣어주시면 되요.

넣어주고 나서, `obj.transform.localPosition`는 알겠는데 `bulletPosition.transform.position;` 오잉? `position`? 저흰 여태까지 `localPosition`을 썻는데 갑자기 `position`이 나왔네요?

`position`은 상위 오브젝트의 위치 값까지 계산한 결과를 총합해서 가져옵니다. 즉 `Player`의 각도가 30도 돌려져 있고, 위치 값도 x값으로 10정도 옮겨져 있다고 한다면 그 값에 `bulletPosition`의 위치값이 더해진 결과가 `position`이 됩니다.

이 예제에서 움직이는 것은 `Player`입니다. 그러므로 `Player`의 위치값이 없으면 꽝이기 때문에 더해준 값인 `position`을 쓰는거에요. 그렇게 해서 한번 실행 해볼까요?

![이미지18](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/18.png?raw=true)

아까랑 똑같은 이미지인데 이렇게 나오죠? 움직여봐도 똑같이 나올꺼에요.

### 총알을 쏘기

이제 총알을 생성했으니 쏴봐야겠죠? `Space Bar`를 누르면 쏘도록 해볼께요.

`Bullet` 클래스를 만들어서 생성되면 `Bullet` 클래스에서 움직이도록 해봅시다.

```csharp
using UnityEngine;

public class Bullet : MonoBehaviour {

	new Rigidbody rigidbody = null;

	public void Create(Player player, int power) {
		// rigidbody에 데이터가 이미 들어가 있으면 데이터를 넣어줄 필요가 없기 때문에 공간이 비어있을때만 대입.
		if(rigidbody == null) rigidbody = GetComponent<Rigidbody>();

		transform.localPosition = player.bulletPosition.transform.position;
		rigidbody.AddForce(player.transform.forward * power);
	}
}
```

그렇게 소스가 길진 않아요. 간단합니다. 저번시간에 했듯 총알도 `AddForce`를 사용해서 힘을 줘서 날려보낼꺼에요.

`Bullet Prefab`에 컴포넌트를 추가해볼께요.
`Bullet`에는 `Rigidbody`를 사용해서 쏠때 힘을 줘서 밀기 때문에 강체가 붙어있어야 되요.

![이미지20](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/20.png?raw=true)

그리고 이제 생성하는 `Player` 부분에서 수정을 해보도록 해요.

```csharp
using UnityEngine;

public class Player : MonoBehaviour {

	new Rigidbody rigidbody;
	new Transform transform;

	public float power;
	public float rotationSpeed;

	public GameObject bulletObject;
	public GameObject bulletPosition;

	void Start() {
		rigidbody = this.GetComponent<Rigidbody>();
		transform = this.GetComponent<Transform>();
	}

	void Update() {
		Move();
	}

	void Move() {
		if(Input.GetKey(KeyCode.W)) {
			rigidbody.AddForce(transform.forward * power * Time.deltaTime, ForceMode.Impulse);
		} else if(Input.GetKey(KeyCode.S)) {
			rigidbody.AddForce(-transform.forward * power * Time.deltaTime, ForceMode.Impulse);
		}

		if(Input.GetKey(KeyCode.A)) {
			Vector3 euler = transform.localEulerAngles;
			euler.y -= rotationSpeed * Time.deltaTime;
			transform.localEulerAngles = euler;
		} else if(Input.GetKey(KeyCode.D)) {
			Vector3 euler = transform.localEulerAngles;
			euler.y += rotationSpeed * Time.deltaTime;
			transform.localEulerAngles = euler;
		}

		if(Input.GetKeyDown(KeyCode.Space)) {
			CreateBullet(300);
		}
	}

	void CreateBullet(int power) {
		Bullet bullet = Instantiate(bulletObject).GetComponent<Bullet>();
		bullet.Create(this, power);
	}
}

```

어라 아까보다 소스코드가 간결해졌네요? 그리고 `Instantiate`는 `GameObject`형을 반환하기 때문에 `GetComponent`를 사용해서 컴포넌트를 가져와야 합니다.

`Bullet`을 가져오고, 그 안에 `Bullet.Create`를 사용해서 생성하는 코드를 작성합시다.

실행을 해보고 움직이면서 스페이스 바로 쏴보세요.

![이미지21](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/21.png?raw=true)

잘 되는군요!

##### 더러워진 `Hierarchy` 청소하기

근데 총알을 생성하면 `Hierarchy`에 난잡하게 나오게되네요? 아래처럼요.

![이미지22](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/22.png?raw=true)

흐음 이걸 어떻게할까요? 어디에 한군데에 몰아두는게 좋을것 같아요. 보기싫으면 폴더를 닫게끔요. `BulletManager`라는 오브젝트를 만들어서 관리를 하는게 좋겠군요?

`GameObject`를 새로 하나 만들어서 `BulletManager`라고 만들어서 이번에는 Player안에 말고 밖에다 만들어주세요. 안에다 만들어서 그 안에 `Bullet`이 생성되면 플레이어 위치가 변할때마다 `Bullet`의 위치도 변하게 되요! 그럼 안됩니다.

소스코드도 약간씩 바꿔줍시다.

Player.cs 에 `bulletManager`를 추가해주세요. 그리고 에디터에서도 끌어다 넣어주세요.

```csharp
public GameObject bulletManager;
```

Bullet.cs 에서는 아래처럼 해주면됩니다.

```csharp
using UnityEngine;

public class Bullet : MonoBehaviour {

	new Rigidbody rigidbody = null;

	public void Create(Player player, int power) {
		if(rigidbody == null) rigidbody = GetComponent<Rigidbody>();

		transform.parent = player.bulletManager.transform;
		transform.localPosition = player.bulletPosition.transform.position;
		rigidbody.AddForce(player.transform.forward * power);
	}
}
```

`transform.parent = player.bulletManager.transform;`가 추가되었군요?
`transform.parent`는 해당 `transform`의 부모를 불러옵니다. 3계단 위의 부모를 가져오려면 `transform.parent.parent.parent`로 가져오면 됩니다. 쉽죠?

`BulletManager`에 넣어야줘야 하니까. `player.bulletManager.transform`를 넣어줍시다. 그리고 실행을 해보면 아래와 같이 나오게 되요!

![이미지23](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/23.png?raw=true)

효율적으로 볼 수 있게 되었군요!
