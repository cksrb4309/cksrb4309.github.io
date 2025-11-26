---
layout: single
title: "ECS 2편 : 속도는 왜 빠를까 (메모리)"
categories: [study, unity_study, unity_study_ecs] # category: study 하나만 할 때는 이렇게
tag: [Unity_Study, ECS]
toc: true
author_profile: true
sidebar:
    nav: "docs"
search : true
---

---

# 속도는 왜 빠를까 (메모리)

메모리 접근 속도가 월등히 빨라졌기 때문이다.

이전에 작업하던 이동하는 코드가 예를 들어

```
public A : MonoBehaviour
{
	[SerializedField] Rigidbody rb;
	[SerializedField] float speed;
	
	void Update()
	{
		rb.linearVelocity = forward * speed;
	}
}
```

라고 가정했을 때 (forward 는 우주 저 너머에서 정면 값(Vector3)를 가져왔다고 가정)

각 Rigidbody는 GameObject에 붙은 Component 단위로 흩어져 있음.
메모리 상에서 Rigidbody, Transform, Collider 등은 연속된 배열이 아님.
그렇기 때문에 CPU가 한 번에 여러 Component 데이터를 처리할 때 캐시 미스(Cache Miss)가 많이 발생됨.

Entity에 넣는 Component는 타입별로 구분하여 연속된 배열로 배치를 한다(SoA)
그렇기 때문에, 캐시 미스로 인한 성능 손실이 크게 줄어든다.

메모리에 어떤 방식으로 저장하는지를 알아보자.

데이터를 저장하는 단위는 Chunk로, 만약 LocalTransform과
PhysicsVelocity 컴포넌트 데이터를 가지고 있다면
해당 엔티티는 LocalTransform과 PhysicsVelocity를
가진 Archetype(... ,)에 대한 Chunk에 메모리를 할당하게 된다.

따라서, Archetype이 달라졌을 때의 해당 Entity에 대한 데이터를
다른 Archetype에 옮겨야해서 비용이 크다.
그래서 런타임 중에 잦은 Component 변동은 성능상 안 좋다.
