---
title: Unity MARS 기초 사용법 (1)
author: JadeBright
date: 2020-08-16 18:00:00 +0900
categories: [Unity/C#, AR/VR]
tags: [Unity MARS]
---

## 개요

Unity MARS(Mixed and Augmented Reality Studio)는 지능형 AR 어플리케이션 개발을 위한 Unity의 툴셋이다. 주요 장점으로는 Unity Editor상에서 Modeling을 이용해 만들어진 가상환경으로 제작된 AR/MR 어플리케이션을 테스트해 볼 수 있다는 점이 있다.

## 설치법

[다운로드 링크](https://unity.com/kr/products/unity-mars)에서 다운로드 가능하며 unitypackage 형식으로 제공된다. 만약 unitypackge 파일을 다시 다운로드 받고 싶다면 Unity 사이트 로그인후 settings의 내 계정 - 내 시트에서 다시 다운로드 가능하다. 또한 *무료 체험판만 사용해보고 싶다면 settings의 내 계정 - 내 시트에서 톱니바퀴 모양의 관리 버튼을 누른 뒤 구독 관리에서 자동 갱신을 꺼주고 저장해주어야 다음 회분이 자동으로 결제되지 않는다.*
유니티는 월 단위 구독을 해도 년 단위로 구독 해지가 가능하기 때문에 주의하여야 한다.
이후 Unity에 새로운 프로젝트를 만들고 다운받은 unitypackage를 Assets - Import Package - Custom Package...에서 찾아서 임포트 해주면 사용 가능하다.

## 빌드 환경 설정

Andriod 운영체제를 기준으로 작성 하겠다. 먼저 Unity에서 Window - Package manager를 클릭하고 ARCore XR Plugin을 검색한 뒤 오른쪽 아래의 Install 버튼을 눌러서 설치한다. 다음으로 Edit-Project Settings-Player에서 안드로이드 모양 버튼을 클릭, Other Settings를 펼쳐 Graphics APIs의 Vulkan을 제거하고 아래로 내리면 Minimum API Level이 있는데 이를 Android를 7.0 이상으로 설정한다. 이후 Edit-Project Settings-MARS 아래의 Scene Module의 Simulate In Play Mode를 활성화 시킨다. 마지막으로 Edit-Preferences-MARS에서 Camera permission이 활성화되어있는지 확인한다.

## 사용 예제

모든 기능을 뜯어보기에는 너무 장황해지고 실용적이지 못하기 때문에 실제적인 사용법을 통한 이해가 더 좋을 것이다.
Image Marker를 통한 예제를 작성 하겠다.

먼저 메뉴의 Window - MARS - Simulation View를 켠다. Simulation View는 유니티 에디터 상에서 개발한 AR 어플리케이션을 테스트 해 볼 수 있는 환경을 제공한다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/simulation_view.png" | relative_url }})
> 그림1. Simulation View 화면

Window - MARS - MARS Panel 또한 켠다. 이는 Simulation View에서 보이는 가상 환경(?) 상의 오브젝트들의 Hierarchy를 관리하고 MARS의 다양한 기능들을 간단한 클릭 한번으로 구현 가능하게 한다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/MARS_panel.png" | relative_url }})
> 그림2.  MARS Panel 인터페이스

이 때 Simulation View 아래 쪽을 보면 노란색 삼각형 안에 느낌표가 있는 오류창이 보일텐데 이는 Hierarchy에 MARS Session을 추가하라는 것이다. MARS Session은 MARS Database에 저장될 특성의 목록들을 관리한다.
MARS Session을 추가하는 법은 Hierarchy에서 우클릭하고 MARS - MARS Session을 누르면 된다. 지금 다루는 Hierarchy는 일반 Hierarchy이다. MARS Panel의 Hierarchy가 아니다. MARS Panel의 Hierarchy를 사용할 때는 특별히 언급할 것이다.

이제 인식할 이미지를 담아둘 Marker Library를 만들 것이다. Project 창에서 우클릭 후에 Create - MARS - Marker Liberary를 누른다. 그러면 프로젝트 상에 MarsMarkerLiberary가 추가 될텐데 클릭하면 Inspector창에 Add Image라는 버튼이 있을 것이다. 이를 클릭한다.
클릭하면 아래와 같은 그림이 나올텐데 그림에 보이는 None(Texture 2D)에 원하는 이미지를 드래그앤 드롭 하거나 아래 Select를 누르고 선택해주면 된다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/marker_library.png" | relative_url }})
> 그림3.  Marker Library 인스펙터

그 후 이렇게 이미지를 추가한 Marker Library를 MARS session에 넣어준다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/MARS_session.png" | relative_url }})
> 그림4.  Marker Library를 추가한 MARS Session

Hierarchy에서 우클릭, MARS - Presets - Image Marker를 추가한다. 원래 MARS에서는 다양한 조건들을 설정한 객체의 아래에 자식으로 둔 오브젝트를 설정한 조건에 맞춰서 생성되게 할 수 있는데 이는 MARS에서 기본적으로 제공하는 이미지 상에 오브젝트를 생성하게 하는 프리셋이다.
Hierarchy에 생성된 Image Marker를 누르고 Inspector에서 Maker Condition을 펼쳐 아까 Marker Library에 넣어둔 이미지를 눌러준다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/image_marker.png" | relative_url }})
> 그림5.  Image Marker의 Maker Condition

그리고 Image Marker 아래에 원하는 오브젝트 하나를 자식으로 둔다. 기본적으로 3D Object - Cube로 진행하겠다. 이 후 Scene창을 보면 생성한 오브젝트가 보일텐데 scale을 0.05 정도로 작게 줄이면 다음과 같은 화면이 보일 것이다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/scene1.png" | relative_url }})
> 그림6-1.  Image Marker의 Maker Condition
이는 이미지가 있을 때 생성 오브젝트의 위치를 지정해주는 것으로 이미지와 오브젝트가 겹치면 부자연스러우니 오브젝트를 약간 위로 올려주겠다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/scene2.png" | relative_url }})
> 그림6-2.  Image Marker의 Maker Condition

이렇게 하고 빌드하면 작동이 된다. 하지만 MARS에서는 위에서 말했듯이 유니티 에디터 상에서 테스트를 할 수 있다. MARS Panel의 Create - Simulated - Synthetic Image를 누르면 MARS Panel의 Environment Hierarchy에서 Simluated Markers - Syntheic Image Marker가 생긴다. 클릭하면 인스펙터의 Sysnthesized Marker Id에서 이미지를 선택한다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/synthesized_marker_id.png" | relative_url }})
> 그림7.  Synthesized Marker Id

그리고 MARS Panel의 Environment Hierarchy에서 Simluated Markers - Syntheic Image Marker를 더블클릭하면 Simulation View창에서 이 이미지가 존재하는 위치로 화면이 이동되는데 이를 원하는 대로 옴겨주면 된다. 이후 Simulation View창의 재생 모양의 Start Simulation 버튼이나 유니티의 Play 버튼을 눌러서 해당 위치로 이동해 확인을 한다.
카메라 조작법은 w: 앞으로 이동, s: 뒤로 이동, a: 좌로 이동, d: 우로 이동, q: 아래로 이동, e: 위로 이동이며 *마우스 우클릭으로 화면을 잡고 있어야만 이동 가능* 상태가 된다. 이동하여 확인하면 다음과 같다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/test_in_unity.png" | relative_url }})
> 그림8.  유니티 상에서 테스트 

마지막으로 핸드폰에 빌드를 해 볼 것이다. 이를 위해서는 위의 빌드 환경 설정 과정을 모두 마치고 개발자 모드를 켜놓는다. 그리고 File - Build Settings에 들어가 Android를 누른다. 이후 핸드폰과 컴퓨터를 연결하고 핸드폰에서 디버깅을 허용해 준다. 다음으로 Run Device를 Refresh해주면 핸드폰 모델명이 적혀있는데 이를 클릭하고 아래의 Switch Platform를 누른다. 변환이 끝나면 Build And Run을 눌러준다. apk파일은 적당한데 저장해 둔다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/build_settings.png" | relative_url }})
> 그림9.  Build Settings

핸드폰을 켜면 Unity 어플리케이션이 자동으로 실행되고 카메라 허용 여부를 묻는다. 허용을 눌러주고 카메라가 켜지면 모니터에 이미지를 띄우고 비춰주면 다음과 같다. 이 때 이미지나 주면 광원 밝기 등에 따라서 잘 인식이 안되는 경우도 있다.
![simulation_view]({{ "/assets/img/posts/2020-08-16-UnityMARS_basic_usage/test_in_real_world.png" | relative_url }})
> 그림10.  실제 테스트

## 다른 조건

위의 예제에서 Image Marker를 예제로 사용하였는데 기본적으로 주어지는 다른 조건들(Plane Size: Plane 사이즈 범위를 조건으로 함, GeoFence: 위도 경도의 위치와 범위를 조건으로 함, Trait - Face: 얼굴 인식 Etc.) 또한 사용 가능하다. 조건들은 Hierarchy 우클릭, MARS - Proxy Object를 누르고 인스펙터의 Add MARS Componnent...의 Condtion을 이용해 추가할 수 있다. 이는 Hierarchy의 Image Marker와 동일한 방식으로 작동한다.

Etc...