---
title: Unity MARS ���� ���� (2)
author: JadeBright
date: 2020-08-19 20:00:00 +0900
categories: [Unity&C#, AR&VR]
tags: [Unity MARS]
---

�̹��� ������ ��� ����� ������ ��ɵ�� ��ũ��Ʈ�� ���� ���� �� �ִ� �͵鿡 ���ؼ� �ٷ�ڴ�.

##Plane Visualizer

Plane Visualizer�� Hierarchy���� ��Ŭ�� ��, MARS - Data Visualizer�� ������ ų �� �ִ�.
�� ����� Ű�� mesh���·� ����κ��� Plane���� �ν��ߴ��� �ð������� �����ش�.

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/plane_visualizer.png" | relative_url }})
> �׸�1. Plane Visualizer

##����Ƽ �� �׽�Ʈ ȯ�� ��ȯ �� ����Ʈ

MARS�� ����Ƽ ������ �׽�Ʈ ȯ���� ������ �ִµ�, �⺻������ �������� �� ���� �־����ִ�.
�̴� Simulation View â�� ��ܿ� *<*��*>* ����� ��ư�� ������ Ȯ�� �� �� �ִ�.
���� �⺻������ �־��� �����¸��� ���� ����Ʈ �� ���� �ִµ�, �̸� ���� Asset Store���� ������ ���� ���� ������ ����Ʈ ���ְڴ�.
�غ��� �غ��ٸ�, ���� Project���� ��Ŭ��, Create - MARS - Simulated Environemnt Prefab�� �����ش�.
�׷��� Simulated Environemnt�� �����Ǵµ� �̸� ����Ŭ���ϰ� Simulated Environemnt�� Hierarchy�� ������ �غ��� �� Prefab�� �巡�׾ص���Ѵ�.
�׸��� Hierarchy�� ���� Clipping Region�̶�� �����ٵ� �̸� �̿��� ȯ���� �������� ������ AR�� ������ ������ �����־���Ѵ�.

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/simulated_environment.png" | relative_url }})
> �׸�2. Simluated Evironment

�������� �غ��� �� Prefab�� Clipping Region�� �ڽ����� �д�. �׸��� Simluated Environment �������� Inspectorâ�� ���� Plane Extraction Settings(Script)�� �����ٵ� ���⼭ Voxel(3���� ���� �ȼ�)�� Plane�� ���� ��ġ ������ ���ش�.
���� Extract Planes��ư�� ������ Hierarchy�� Generated Planes�� ����°� �� �� �ִ�. 

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/plane_extraction_settings.png" | relative_url }})
> �׸�3. Plane Extraction Settings

���� �ٽ�  Simluated Environment �������� Inspectorâ�� Plane Extraction Settings(Script)�Ʒ��� ���� MARS Environment Settings�� �ִµ� ���⼭ Save Environment View�� Save Simulation Starting Pose�� ������.
���� Default Camera World Pose�� Simulation Viewâ���� �����ϴ� ī�޶� ��ġ�̰� Simlation Starting�� Gameâ�̳� Device View�� ���� ī�޶� ��ġ�̴�. ���� ������ ���� �ʰ� ��ư�� ������ �˾Ƽ� ��ġ�� ã���ش�.

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/mars_environment_settings.png" | relative_url }})
> �׸�4. MARS environment Settings

�� �Ǿ����� Simulation View â���� ������� �׽�Ʈ ȯ���� ã�´�. ã�� ����� ������ ���ߵ��� *<*��*>*�� �̿��� �ѱ�ų� ������ �̸��� Ŭ���� ã���� �ȴ�. ã�� �ڿ� Plane Visualizer�� �Ѱ� �����ϸ� ������ ����.
*Plane Visualizer�� �߰��� �� Simluated Environment �������� �ƴ� ������ Scene�� �߰��ϵ��� �����Ѵ�.*

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/mars_environment_settings.png" | relative_url }})
> �׸�5. Simluated Evironment Test

##Proxy Group Queries

MARS�� MARS Database�� ī�޶� ������ �̹����� Ư������ �����ϰ� �� Ư������ �̿��� ���ǿ� ���� 3D ������Ʈ���� �����Ű�ų� �����ϰų� �Ѵ�.
�������� Image Marker�� �̿��� ������ �ۼ��Ͽ��µ� �̴� ���� ��ü�� ���� ���� �����̾���. MARS�� ���� ��ü�� ���� ���� ���� �Ӹ��� �ƴ� ��ü���� ���տ� ���� ���� ���ǰ� ���� ������ ������Ʈ���� ���� �����ϴ�.

**Condition**

Condition�� ������ ����ߴ� Image Marker�� ���� ���� ��ü�� ���� ������ �ٷ�� ���̴�. ������ �ٷ�� ��ó�� Hierarchy ��Ŭ��, MARS Proxy Object�� ������ �ν������� Add MARS Component, Condition������ ������ �����ϸ� �ȴ�.
���� �����ϰ� ���� ��ü�� Proxy Object�� �ڽ����� �θ�ȴ�.
����� Condition - Trait - Is Plane�� ����غ� ���̴�. �̰��� ���� �⺻���� �������� Plane�� �����Ѵٸ� �� ��ü�� ���� �ϴ� ���̴�.

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/is_plane.png" | relative_url }})
> �׸�6. Is Plane Condition Test

**Relation**

Reation�� Proxy Object���� �ڽ����� �� Proxy Group�� �� �ڽĵ� ���� ��� ������ �̿��� ���� ������ ���� �ϴ� ���̴�. Proxy Group�� ���� ���� Hierarchy�� ��Ŭ���ϰ� MARS Proxy Group�� ������ �ν����Ϳ��� Add MARS Component�� ������ Reation�� �����ٵ� ���⼭ �� �� �ִ�.
������ Distance Relation���� �����ߴ�.

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/distance_relation_inspector.png" | relative_url }})
> �׸�7-1. Distance Relation Inspector & Hierarchy

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/distance_relation_test.png" | relative_url }})
> �׸�7-2. Distance Relation Test

**Action**

Action�� ������ Object�� ������Ʈ �ֱ⺰�� ������Ʈ�� ��� �� ���ΰ�, �ش� ��ü ȯ���� ������ �Ǵ� ��ü�� ���� ���� ������ ���� �ʰų� �ʹ� ���� �����Ǿ ������Ʈ�� ������ �� ��� �̺�Ʈ�� �� ���ΰ��� �����ϴ� ���̴�.
���� ������ Match Action���� �Լ� ������ ������ �� �ִ�. �ٸ� �����µ��� ���� ������ �и��Ǿ� ���� �ʰ� �ϳ��� �����ִ�. ������ Proxy Object��  Add MARS Component, Action���� �����ϸ� �ȴ�.
������ Match Action�� �̿��� ���̴�. ���� Condtion - Is Plane���� ���� ������ �޾��ش�. �� �� Action���� Match Action�� ���� On Match Update�� �����ش�. �̴� ��ü ���Ÿ��� ��ü�� ����ȴ�. �ٸ� On Match Acquire�� ��ü ������ ���ʿ�, On Match Loss�� ��ü�� ������ �� �̻� �������� ���� ��, On Match Timeout�� Ư�� �ð� ���� ��ü�� ����� ������ ���� �� ����ȴ�.
�׸��� �׽�Ʈ�� ���� CubeRotate �Լ��� �ۼ��ϰ� Proxy Object �ڽ��� �Ǵ� Cube�� �־��ش�. ���� Proxy Object�� �ν����Ϳ��� Match Action - On Match Update - None Object�� �ڽ��� �Ǵ� Cube�� �־��ְ� ������ No Function�� CubeRotate bool.enabled�� �����ϰ� �Ʒ� üũ�� ���ָ� �ȴ�.

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/match_action_inspector.png" | relative_url }})
> �׸�8-1. Match Action �ν�����

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/cube_inspector.png" | relative_url }})
> �׸�8-2. Cube �ν�����

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/cube_rotate.png" | relative_url }})
> �׸�8-3. CubeRotate

![simulation_view]({{ "/assets/img/posts/2020-08-19-UnityMARS_basic_usage2/match_action_test.gif" | relative_url }})
> �׸�8-4. Match Action Test

##�������

������� �⺻���� �����̰� �߰������� �����Ǵ� Provider�� �����ϰų� Custom Condition�� ����ų� ���ο� Ư���� �����ϴ� ���� ����� �����Ѵ�.

�ڼ��� ������ ���� ��ũ�� ������ ���⸦ �ٶ���.

[Unity Tutorial](https://docs.unity3d.com/Packages/com.unity.mars@1.0/manual/index.html)