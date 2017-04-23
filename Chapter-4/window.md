### 유니티의 윈도우 살펴보기

한번 유니티를 켜보도록 해요. 프로젝트는 test로 만들어요.

![이미지1](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/1.png?raw=true)

이러한 화면이 기본적으로 나올 것 입니다. 한번 자세히 살펴보도록 해요.

##### 인스펙터 (Inspector)

인스펙터는 오브젝트나 파일등의 대한 정보들을 보여주는 뷰입니다.

인스펙터에서는 현재 클릭한 오브젝트에 대해서 정보를 보여주게 되는데요. 그게 소스코드라면 소스코드에 대해서 프리뷰를 보여주고, 게임 오브젝트라면 오브젝트의 정보를 보여줍니다. 새로 프로젝트를 생성했을때는 아무 오브젝트를 클릭하지 않은 상태니 아무것도 보이지 않겠죠?

![이미지5](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/5.png?raw=true)


##### 히어라키 (Hierarchy)

히어라키는 유니티에서 자신의 프로젝트에서 사용되는 오브젝트들의 계층 구조를 볼 수 있는 뷰입니다. 기본적으로 프로젝트를 새로 생성하면 히어라키에 씬에 기본적으로 제공되는 Untitled 라는 씬과 함께 카메라와 조명이 한개씩 배치되어 있습니다.

![이미지2](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/2.png?raw=true)

히어라키 안에서는 무제한으로 부모와 자식 계층을 만들 수 있습니다. 이런식으로요.

![이미지3](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/3.png?raw=true)

이렇게 계층을 나눠서 할일을 명확하게 나눌수 있게 할 수도 있고, 어디에 위치를 지정해서 그 위치에서 게임이 시작되게 할 수도 있답니다. 그런 내용은 차후 게임을 직접 만들어보면서 해볼 예정이에요.

##### 프로젝트 (Project)

프로젝트는 유니티에서 모든 자원들이 들어있는 뷰입니다. 프로젝트 안의 파일을 유니티 오브젝트들에 연결해서 사용하는 것이 주된 패턴입니다.

![이미지4](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/4.png?raw=true)

한번 소스코드를 만들어볼까요? 오른쪽 클릭을 통해서 C# 코드를 만들어봅시다.
프로젝트 뷰의 안에서 오른쪽 클릭을 해주세요. 그리고 Create > C# Script를 눌러주시고 이름을 입력해주세요.

그럼 이렇게 만들어집니다.

![이미지7](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/7.png?raw=true)

큰 아이콘 말고 리스트형식으로 볼 수도 있어요.
프로젝트 오른쪽 부분 탭에 버튼을 누르면 아래의 사진처럼 나와요. 거기서 `One Column Layout`을 눌러주세요.

![이미지8](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/8.png?raw=true)

그럼 이렇게 됩니다.

![이미지9](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/9.png?raw=true)


##### 콘솔 (Console)

콘솔은 `Debug.Log` 라는 명령어를 통해서 프로그램 사이클이 해당 지점을 넘어갈 때마다 어떤 일이 있었는지 기록을 통해 볼수있게 해주는 뷰입니다.

![이미지10](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/10.png?raw=true)

콘솔을 다루는 방법은 게임을 만들면서 자세히 알아보도록 해요.

##### 장면 (Scene)

장면은 히어아키에 계층으로 나누거나 만들어놓은 오브젝트들이 게임의 3D환경에서 어디 위치에 배치하고 할때 도움을 주거나, 어디에 있는지 시각적으로 볼 수 있는 뷰입니다.

![이미지11](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/11.png?raw=true)

여기서 한번 유심히 봐야할 오브젝트가 있는데요. 바로 `기즈모(Gizmo)` 입니다. 기즈모는 뷰의 보는 방향에 대해서 편리하게 바꿔주는 기능을 제공합니다.

![이미지12](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/12.png?raw=true)

기즈모의 각 축을 한번 눌러보세요. 그럼 그 축 기준으로 보는 뷰로 바뀌게 됩니다.

![이미지13](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/13.png?raw=true)

##### 게임 (Game)

게임뷰는 게임이 실제로 동작하는 뷰입니다. 플레이 버튼을 누르면 자동으로 게임뷰가 가장 처음에 보이게 됩니다.

![이미지14](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/14.png?raw=true)

게임뷰의 사이즈는 조절을 할 수 있습니다. Free Aspect를 누르게되면 아래와 같은 뷰가 나오게됩니다.
+ 버튼을 통해서 추가적인 사이즈 뷰도 만들수 있습니다.

![이미지15](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/15.png?raw=true)

##### 그 외 (ETC)

![이미지16](https://github.com/Vallista/unity-3d-teaching-material/blob/master/Image/Chapter-4/16.png?raw=true)

이미지의 가장 왼편에 존재하는 컨트롤 부분은 손모양, 십자모양, 등으로 이루어져 있는데요. 이 부분은 씬부분에서 오브젝트를 눌러서 어떻게 할 것 인지에 결정하는 부분입니다. 손모양을 누르면 화면을 스크롤 하게 되고 십자모양을 누르면 오브젝트를 움직일 수 있게 됩니다. 

화면의 가운데에 있는 컨트롤은 각각 플레이 / 정지 / 다음 액션 실행 버튼입니다.
자신이 게임을 어떻게 만들었나 보고싶으면 플레이 버튼을 눌러, 이상한 부분이 있다면 정지를 누르고, 천천히 다음 액션 실행 버튼을 통해서 재생을 하나씩 하게 됩니다.

오른쪽에 있는 컨트롤들은 아직은 알 필요가 없는 컨트롤들 입니다. 나중에 천천히 알아보도록 해요.
