# Waffle Decoration Robot Simulation

## Preview
https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/8a2aa832-9004-43b3-ad49-f4488fbff049
https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/189d8a68-1032-453e-ad4d-8337906fa2b8

## Research Topic
와플 데코레이션 로봇 시뮬레이션 개발

## Scheme
<img width="437" alt="스크린샷 2024-05-15 13 26 41" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/5325d96b-74d6-4c1e-ac61-527fb1f6ab1c">

로봇의 전체적인 스키마입니다.

## Specification
<img width="451" alt="스크린샷 2024-05-15 13 27 48" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/88bd44ce-5b98-4d9c-b136-75e7a37d4563">

링크 길이
|   | $$d$$ | $$L_1$$ | $$L_2$$ | $$L_3$$|
|---|---|---|---|---|
|$$Length (m)$$|$$1.5$$|$$0.3$$|$$0.3$$|$$0.08$$|

링크 질량
|   | $$m_1$$ | $$m_2$$ | $$m_2$$ |
|---|---|---|---|
|$$Mass (kg)$$|$$3$$|$$3$$|$$1$$|

해당 로봇은 $\psi$, $\theta_1$, $\theta_2$, $\theta_3$ 총 4자유도를 가집니다.

위치 $(x, y, z)$를 결정하기 위해 $\psi$, $\theta_1$, $\theta_2$ 를 사용하며 $\theta_3$ 는 와플을 떨어뜨리지 않도록 항상 
 $+z$ 축을 바라보도록 설계되었습니다.

링크는 실제 사람과 유사하도록 길이와 질량을 설정하였습니다.

## Kinematics
<img width="170" alt="스크린샷 2024-05-15 13 33 59" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/65ec39fb-0238-4e83-9776-1d53d5c0bdae">

### DH Parameter
| $$i$$  | $$\alpha_{i-1}$$ | $$a_{i-1}$$ | $$d_i$$ | $$\theta_i$$ |
|---|---|---|---|---|
|$$1$$|$$0$$|$$0$$|$$d$$|$$\psi$$|
|$$2$$|$$\pi/2$$|$$0$$|$$0$$|$$\theta_1$$|
|$$3$$|$$0$$|$$L_1$$|$$0$$|$$\theta_2$$|
|$$4$$|$$0$$|$$L_2$$|$$d_4$$|$$\theta_3$$|
|$$Tool (Waffle Plate)$$|$$0$$|$$L_3$$|$$0$$|$$0$$|

<img width="483" alt="스크린샷 2024-05-15 13 36 11" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/9880999f-4427-453d-aa94-7cf5c098466f">

DH Parameter 로 forward kinematic 을 통해 다음과 같은 $(x, y, z)$ 좌표를 얻을 수 있습니다.

<img width="537" alt="스크린샷 2024-05-15 13 36 29" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/aa976aad-2aca-4380-bbe8-0869e1f5861c">

역기구학을 통해 얻어낸 $\psi$, $\theta_1$, $\theta_2$, $\theta_3$ 의 관계식입니다. <br/>
$\theta_3$ 는 지면과 항상 수평을 이뤄야하므로 $\theta_3 = \pi/2 - \theta_1 - \theta_2$

## Trajectory

## Dynamics
<img width="574" alt="스크린샷 2024-05-15 13 36 53" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/2bb162bf-1ab0-4b21-b805-50eed281c2b7">

$joint2$, $joint3$ 그리고 와플 플레이트의 중점을 질점으로 가정하였습니다. <br/>
기구학을 통해 얻어낸 각 질점 위치의 $(x, y, z)$ 좌표를 나타낸 식입니다.

## Control

## Result
