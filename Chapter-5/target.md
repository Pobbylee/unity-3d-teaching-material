### 타겟 제작

`Create > 3D Object > Capsule`을 눌러 타겟으로 제작할 원기둥을 생성합니다.

총알때 했던 것 처럼 생성될 타겟들을 깔끔하게 보여줄 `EnemyManager`를 생성합니다. 그리고 그 안에 타겟을 생성할 위치를 `Z, X`축을 이용해 움직여서 놓아주세요.

![이미지24](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/24.png?raw=true)

그리고 아까 만들었던 `Capsule`을 `Enemy`라는 이름으로 바꾸고 복사해서 각각의 위치에 넣어주세요.
가지런히 왼쪽, 중앙, 오른쪽으로 생성된 오브젝트가 보이나요? 필자는 위치를 이렇게 지정해 놓았습니다.

![이미지25](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/25.png?raw=true)

그리고 `Enemy`는 프리팹으로 만들어주세요. 사이즈도 줄여주시면 좋습니다.

![이미지27](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/27.png?raw=true)


##### 매니저 클래스를 만들어서 오브젝트를 생성하고 관리하기

총알은 플레이어 클래스에서 생성해주고 있습니다. 근데 플레이어 클래스에서 총알이 몇개 생성되었는지, 총알을 다시 회수하거나 제거하는등의 행동을 하진 못합니다. 그러한 행동을 하기 위해서는 총알들을 관리하는 클래스가 필수적입니다. 물론 이 프로그램에서 총알 관리자 소스코드는 만들지 않을 예정입니다. 대신 타겟 관리자 클래스를 만들고, 그 관리자 클래스처럼 여러분이 만드시면 되겠습니다.

먼저 `EnemyManager.cs`를 만들어서 소스코드를 작성해봅시다.

`EnemyManager.cs`가 가지고 있어야 할 정보는 생성될 위치의 배열값, 생성할 오브젝트 (타겟) 등이 있습니다.

```csharp
using UnityEngine;
using System.Collections;

public class EnemyManager : MonoBehaviour {

	public Transform[] createPosition;

	public GameObject enemyObject;

	public float createTime;

	void Start() {
		// 코루틴은 2초 후에 생성되게 했으므로 처음 한번은 Start에서
		CreateEnemy(createPosition);
		// 코루틴 실시
		StartCoroutine(CreateCycle());
	}

	IEnumerator CreateCycle() {
		// 무한 반복
		while(true) {
			// 2초마다 한번씩
			yield return new WaitForSeconds(2.0f);

			CreateEnemy(createPosition);
		}
	}

	void CreateEnemy(Transform[] position) {
		GameObject enemy = Instantiate(enemyObject);
		enemy.transform.parent = position[Random.Range(0, position.Length)];
		enemy.transform.localPosition = Vector3.zero;
	}
}
```

예제는 2초마다 한번씩 타겟이 해당 위치에 나오도록 만들어진 소스코드 입니다. `Bullet`을 작성할 때 보던 익숙한 코드들이 있네요? 그렇게 많이 차이나진 않습니다. 차이점은 `Player`에서 `EnemyManager`로 가지고 있는 클래스가 바뀌었다는 것뿐이네요.

`Inspector` 에서는 이렇게 추가해주시면 됩니다.

![이미지26](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/26.png?raw=true)

이제 실행을 해볼까요? 2초에 한번씩 타겟이 지정된 위치에 나오죠?

##### 코루틴을 이용해서 `Enemy` 움직이도록 만들기

간단히 말하자면 AI제작입니다. 볼륨이 작긴하지만 인공지능을 만든다고 보시면 되요..!

`Enemy.cs`를 만들어서 `Enemy`에 컴포넌트 추가를 해줍시다.

그리고 아래와 같이 코딩을 합시다.

```csharp
using System.Collections;
using UnityEngine;

public class Enemy : MonoBehaviour {

	Vector3 startPos;
	int count;
	public Vector3[] patternPos;

	void Start() {
		startPos = transform.localPosition;
		count = 0;

		StartCoroutine(Pattern());
	}

	void Destroy() {
		StopCoroutine(Pattern());
	}

	void Update() {
		transform.localPosition = Vector3.Lerp(transform.localPosition, patternPos[count], 0.01f);
	}

	IEnumerator Pattern() {
		while(true) {
			yield return new WaitForSeconds(2.0f);

			count ++;

			if(count >= patternPos.Length) {
				count = 0;
			}
		}
	}
}

```

위의 예제는 에디터에서 `Vector3[]` 배열로 위치를 지정해서 순차적으로 움직이도록 하는 예제입니다. 2초마다 움직일 지점이 변경이 되어 그 지점으로 이동하게 됩니다.

`Vector3.Lerp`라는 못보던 메소드가 있네요? 이 메소드는 `Vector3.Lerp(A,B,Time)` A를 B까지 Time의 속도 만큼 옮기는 메소드 입니다.

에디터에서 `Enemy` 컴포넌트에 좌표를 지정해주도록 합시다.

![이미지28](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/28.png?raw=true)

실행해보도록 해요. 실행이 잘 된다면 OK입니다!

![이미지29](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-5/29.png?raw=true)


### 직접 해보기

- `BulletManager`를 만들어서 Player에서 `BulletManager`를 통해 접근하여 생성하도록 만들어봅시다.
