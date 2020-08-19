---
title: Unity MARS 기초 사용법 (2)
author: JadeBright
date: 2020-08-19 22:05:00 +0900
categories: [Unity&C#, AR&VR]
tags: [Unity MARS]
---

이번엔 간단한 몇가지 사용해 볼만한 기능들과 스크립트를 통해 얻을 수 있는 것들에 대해서 다루겠다.

## Plane Visualizer

Plane Visualizer는 Hierarchy에서 우클릭 후, MARS - Data Visualizer를 눌러서 킬 수 있다.
이 기능을 키면 mesh형태로 어느부분을 Plane으로 인식했는지 시각적으로 보여준다.

![plane_visualizer]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/plane_visualizer.png" | relative_url }})
> 그림1. Plane Visualizer

## 유니티 내 테스트 환경 전환 및 임포트

MARS는 유니티 내에서 테스트 환경을 제공해 주는데, 기본적으로 프리셋이 몇 개가 주어져있다.
이는 Simulation View 창의 상단에 *<*와*>* 모양의 버튼을 눌러서 확인 할 수 있다.
또한 기본적으로 주어진 프리셋말고 직접 임포트 할 수도 있는데, 이를 위해 Asset Store에서 적당한 모델의 프리 에셋을 임포트 해주겠다.
준비물이 준비됬다면, 먼저 Project에서 우클릭, Create - MARS - Simulated Environemnt Prefab을 눌러준다.
그러면 Simulated Environemnt가 생성되는데 이를 더블클릭하고 Simulated Environemnt의 Hierarchy에 이전에 준비한 모델 Prefab을 드래그앤드롭한다.
그리고 Hierarchy를 보면 Clipping Region이라고 있을텐데 이를 이용해 환경이 보여지는 범위와 AR을 적용할 범위를 정해주어야한다.

![simulated_environment]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/simluated_environment.png" | relative_url }})
> 그림2. Simluated Evironment

다음으로 준비한 모델 Prefab을 Clipping Region의 자식으로 둔다. 그리고 Simluated Environment 프리팹의 Inspector창을 보면 Plane Extraction Settings(Script)가 보일텐데 여기서 Voxel(3차원 상의 픽셀)과 Plane에 대한 수치 설정을 해준다.
이후 Extract Planes버튼을 누르면 Hierarchy에 Generated Planes가 생기는걸 볼 수 있다. 

![plane_extraction_settings]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/plane_extraction_settings.png" | relative_url }})
> 그림3. Plane Extraction Settings

이제 다시  Simluated Environment 프리팹의 Inspector창의 Plane Extraction Settings(Script)아래를 보면 MARS Environment Settings가 있는데 여기서 Save Environment View와 Save Simulation Starting Pose를 누른다.
위의 Default Camera World Pose는 Simulation View창에서 조망하는 카메라 위치이고 Simlation Starting은 Game창이나 Device View의 시작 카메라 위치이다. 딱히 설정을 하지 않고 버튼을 눌러도 알아서 위치를 찾아준다.

![mars_environment_settings]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/mars_environment_settings.png" | relative_url }})
> 그림4. MARS environment Settings

다 되었으면 Simulation View 창에서 만들어진 테스트 환경을 찾는다. 찾는 방법은 위에서 말했듯이 *<*와*>*를 이용해 넘기거나 좌측의 이름을 클릭해 찾으면 된다. 찾은 뒤에 Plane Visualizer를 켜고 실행하면 다음과 같다.
*Plane Visualizer를 추가할 때 Simluated Environment 프리팹이 아닌 기존의 Scene에 추가하도록 유의한다.*

![simluated_environment_test]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/simluated_environment_test.png" | relative_url }})
> 그림5. Simluated Evironment Test

## Proxy Group Queries

MARS는 MARS Database에 카메라에 비춰진 이미지의 특성들을 저장하고 그 특성들을 이용해 조건에 따라서 3D 오브젝트들을 등장시키거나 삭제하거나 한다.
이전에는 Image Marker를 이용해 예제를 작성하였는데 이는 단일 개체에 대한 생성 조건이었다. MARS는 단일 개체에 대한 생성 조건 뿐만이 아닌 개체들의 집합에 대한 생성 조건과 생성 이후의 업데이트까지 설정 가능하다.

**Condition**

Condition은 이전에 사용했던 Image Marker와 같이 단일 개체의 생성 조건을 다루는 것이다. 이전에 다뤘던 것처럼 Hierarchy 우클릭, MARS Proxy Object를 누르고 인스펙터의 Add MARS Component, Condition내에서 조건을 선택하면 된다.
이후 생성하고 싶은 물체를 Proxy Object의 자식으로 두면된다.
예재로 Condition - Trait - Is Plane을 사용해볼 것이다. 이것은 가장 기본적인 조건으로 Plane이 존재한다면 그 물체를 생성 하는 것이다.

![is_plane]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/is_plane.png" | relative_url }})
> 그림6. Is Plane Condition Test

**Relation**

Reation은 Proxy Object들을 자식으로 둔 Proxy Group에 각 자식들 간의 상관 조건을 이용해 생성 조건을 설정 하는 것이다. Proxy Group는 위와 같이 Hierarchy를 우클릭하고 MARS Proxy Group을 누르고 인스펙터에서 Add MARS Component를 누르면 Reation이 보인텐데 여기서 고를 수 있다.
예제는 Distance Relation으로 진행했다.

![distance_relation_inspector]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/distance_relation_inspector.png" | relative_url }})
> 그림7-1. Distance Relation Inspector & Hierarchy

![distance_relation_test]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/distance_relation_test.png" | relative_url }})
> 그림7-2. Distance Relation Test

**Action**

Action은 생성된 Object의 업데이트 주기별로 업데이트를 어떻게 할 것인가, 해당 실체 환경의 조건이 되는 물체가 오랫 동안 갱신이 되지 않거나 너무 많이 변형되어서 오브젝트를 삭제할 때 어떠한 이벤트를 줄 것인가를 설정하는 것이다.
위의 과정은 Match Action으로 함수 단위로 지정할 수 있다. 다른 프리셋들은 위의 과정이 분리되어 있지 않고 하나로 묶여있다. 사용법은 Proxy Object의  Add MARS Component, Action에서 선택하면 된다.
예제는 Match Action을 이용할 것이다. 먼저 Condtion - Is Plane으로 생성 조건을 달아준다. 그 뒤 Action에서 Match Action을 고르고 On Match Update를 눌러준다. 이는 개체 갱신마다 물체에 적용된다. 다른 On Match Acquire는 개체 생성시 최초에, On Match Loss는 개체의 조건이 더 이상 만족되지 않을 때, On Match Timeout은 특정 시간 동안 개체의 모습을 비추지 않을 때 적용된다.
그리고 테스트를 위한 CubeRotate 함수를 작성하고 Proxy Object 자식이 되는 Cube에 넣어준다. 이후 Proxy Object의 인스펙터에서 Match Action - On Match Update - None Object에 자식이 되는 Cube를 넣어주고 우측의 No Function에 CubeRotate bool.enabled를 선택하고 아래 체크를 해주면 된다.

![match_action_inspector]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/match_action_inspector.png" | relative_url }})
> 그림8-1. Match Action 인스펙터

![cube_inspector]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/cube_inspector.png" | relative_url }})
> 그림8-2. Cube 인스펙터

![cube_rotate]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/cube_rotate.png" | relative_url }})
> 그림8-3. CubeRotate

![match_action_test]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/match_action_test.gif" | relative_url }})
> 그림8-4. Match Action Test

## 참고사항

여기까지 기본적인 사항이고 추가적으로 제공되는 Provider를 제한하거나 Custom Condition을 만들거나 새로운 특성을 정의하는 등의 기능이 존재한다.

자세한 사항은 다음 링크를 참조해 보기를 바란다.

[Unity MARS Tutorial](https://docs.unity3d.com/Packages/com.unity.mars@1.0/manual/index.html)