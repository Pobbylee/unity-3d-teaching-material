### 충돌처리

충돌 처리해야할 것은 `총알과 타겟`, `총알과 지면` 이 두 개를 해야됩니다.
`총알과 타겟`은 충돌처리되면 `총알과 타겟`은 삭제가 됩니다. `총알과 지면`은 `총알`만 삭제되어야 합니다.

먼저 `총알과 지면`에 대해서 충돌처리를 만들어보도록 해요.

충돌처리는 아주 간단합니다. `Rigidbody`와 `Box Collider`이 두 개가 컴포넌트로 연결이 되어있고, 소스코드에 아래 처럼 써주면 됩니다.

```csharp
void OnCollisionEnter(Collision other) {
	// 충돌처리가 시작될 때
}

void OnCollisionStay(Collision other) {
	// 충돌처리가 진행되고 있을때 (첫 1회가 아닌 지속)
}

void OnCollisionExit(Collision other) {
	// 충돌처리가 끝날 때
}
```

위의 3개의 함수는 `Start`, `Update`처럼 `Rigidbody`가 존재하면 알아서 동작하는 함수들 입니다.

즉 어느 오브젝트와 충돌처리가 된다면 `Collision other` 보이죠? `other`에 충돌한 오브젝트가 들어갑니다. `other`에서는 `.transform` 을 이용해 `transform` 데이터도 가져올 수 있고, `.gameObject`를 통해서 `gameobject` 데이터도 가져올 수 있습니다.

그렇다면 충돌이 되면 총알이 삭제되는 코드를 만들어 보겠습니다.

```csharp
using UnityEngine;

public class Bullet : MonoBehaviour {

	new Rigidbody rigidbody = null;

	public void Create(Player player, int power) {
		// rigidbody에 데이터가 이미 들어가 있으면 데이터를 넣어줄 필요가 없기 때문에 공간이 비어있을때만 대입.
		if(rigidbody == null) rigidbody = GetComponent<Rigidbody>();

		transform.parent = player.bulletManager.transform;
		transform.localPosition = player.bulletPosition.transform.position;
		rigidbody.AddForce(player.transform.forward * power);
	}

	// Collision 충돌이 되었을 때, 말고도 OnCollisionStay, Exit가 있다.
	void OnCollisionEnter(Collision other) {
		Destroy(gameObject);
	}
}
```

아래의 `OnCollisionEnter`를 볼까요? 그럼 Destroy(gameObject)가 있군요.
`Destroy`는 말 그대로 삭제를 하는 함수입니다. 이 함수는 `MonoBehaviour`에 들어있습니다. `MonoBehaviour`를 상속받은 오브젝트를 유니티 상에서 삭제해버리는 함수입니다. `gameObject`를 넣는 이유는 `Hierarchy`의 기본 단위는 `gameObject`이기 때문에 `Hierarchy`에 직접 대응되는 오브젝트입니다. 그러므로 삭제를 하면 뷰에 보이지 않게 됩니다.

실행을 해보면 총알이 삭제가 되는 것을 볼 수 있습니다.

##### `tag`를 사용하여 충돌 분기 나누기

근데 우리는 총알과 지면, 총알과 타겟 이 두개에 대해서 만들어야 되는데 이렇게 되면 한가지 밖에 하지 못합니다. 그래서 `Unity`에서는 여러가지 방법을 제공하는데 그중에서 가장 쉬운 방법인 `tag`를 이용해서 분기를 나눠봅시다.

먼저, 지면의 태그를 설정해봅시다. 지면들을 드래그해서 `Inspector`의 `Tag`를 누르고, Tag창으로 가서 Tag를 입력해주세요. `Enemy`와 `Ground`를 입력해줍시다.

그리고 Ground와 그 밑에 Wall에는 `Ground`로 `Tag`를 설정해주세요.

![이미지33](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/33.png?raw=true)

`Enemy`에도 같이 등록해주세요.

![이미지34](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/34.png?raw=true)

이제 소스코드에서 불러와봅시다. `Bullet`에서 아래와 같이 처리해주면 됩니다.

```csharp
using UnityEngine;

public class Bullet : MonoBehaviour {

	new Rigidbody rigidbody = null;

	public void Create(Player player, int power) {
		// rigidbody에 데이터가 이미 들어가 있으면 데이터를 넣어줄 필요가 없기 때문에 공간이 비어있을때만 대입.
		if(rigidbody == null) rigidbody = GetComponent<Rigidbody>();

		transform.parent = player.bulletManager.transform;
		transform.localPosition = player.bulletPosition.transform.position;
		rigidbody.AddForce(player.transform.forward * power);
	}

	// Collision 충돌이 되었을 때, 말고도 OnCollisionStay, Exit가 있다.
	void OnCollisionEnter(Collision other) {
		//Debug.Log(other.transform.tag);
		// other에는 충돌된 오브젝트의 정보가 들어와요.
		if(other.transform.tag.Equals("ground")) {
			Destroy(gameObject);
		} else if(other.transform.tag.Equals("enemy")) {
			Destroy(other.gameObject);
			Destroy(gameObject);
		}
	}
}
```

`OnCollisionEnter`를 보면 `other.transform.tag`로 비교를 하는 것을 볼 수 있습니다. `Ground` 와 충돌하면 자기자신 총알만 삭제, `enemy`와 충돌하면 `other.gameObject`, 즉 부딪친 타겟과 자기 자신을 삭제하게 됩니다. 어렵지않죠?
