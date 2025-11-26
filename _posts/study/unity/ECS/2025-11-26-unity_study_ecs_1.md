---
layout: single
title: "ECS 1편 : ECS는 뭘까"
categories: [study, unity_study, unity_study_ecs] # category: study 하나만 할 때는 이렇게
tag: [Unity_Study, ECS]
toc: true
author_profile: true
sidebar:
    nav: "docs"
search : true
---

---

# ECS는 뭘까

우선 영어 약자를 풀어서 보면 Entity Component System이다.

Entity는 GameObject와 살짝 비슷한 느낌으로
GameObject에 Rigidbody, Collider를 달아서 물리 기능을 확인하는 것처럼
Entity는 PhysicsVeloticy, PhysicsCollider 등의 ComponentData를 통해서 물리 기능이 수행된다

다만! GameObject에 Component를 넣으면 플레이 시
해당 컴포넌트의 기능이 바로 적용되는 것을 볼 수 있지만

Entity의 기능 수행은 살짝 결이 다르다.
데이터를 들고 있을 Entity가 존재할텐데
해당 데이터 조작에 대해서는 System이 수행한다.

따라서, Entity에게 데이터를 잘 줘야지
System이 해당 데이터를 통해 기능을 수행한다.

ECS는 데이터 중심 설계(DOD : Data Oriented Design)으로
같은 조건으로 기존 GameObject를 통해 개발하던 것보다
훨씬 빠른 속도의 프레임을 확인할 수 있다.

