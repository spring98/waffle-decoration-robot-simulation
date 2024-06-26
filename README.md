# Waffle Decoration Robot Simulation

## Preview
https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/4c35c273-1c62-4d75-ac70-3a0ae670f535

## Research Topic
와플 데코레이션 4자유도 로봇 시뮬레이션 개발

## Scheme
<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/53d1bf3c-1591-4a23-a4b6-f71c5213a043"> 
</p>

로봇의 전체적인 스키마입니다.

우측하단에서 생성한 Trajectory 와 좌측상단 매니퓰레이터의 현재각도, 현재 각속도를 좌측하단 제어블록에 입력하여 매니퓰레이터에 입력할 토크를 계산하고 다시 매니퓰레이터에 입력하는 폐루프 제어 구조로 설계하였습니다.

## Specification
<p align="center">
 <img width="50%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/88bd44ce-5b98-4d9c-b136-75e7a37d4563"> 
</p>

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
<p align="center">
 <img width="50%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/65ec39fb-0238-4e83-9776-1d53d5c0bdae"> 
</p>

### DH Parameter
| $$i$$  | $$\alpha_{i-1}$$ | $$a_{i-1}$$ | $$d_i$$ | $$\theta_i$$ |
|---|---|---|---|---|
|$$1$$|$$0$$|$$0$$|$$d$$|$$\psi$$|
|$$2$$|$$\pi/2$$|$$0$$|$$0$$|$$\theta_1$$|
|$$3$$|$$0$$|$$L_1$$|$$0$$|$$\theta_2$$|
|$$4$$|$$0$$|$$L_2$$|$$d_4$$|$$\theta_3$$|
|$$Tool (Waffle Plate)$$|$$0$$|$$L_3$$|$$0$$|$$0$$|

<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/9880999f-4427-453d-aa94-7cf5c098466f"> 
</p>

DH Parameter 로 forward kinematic 을 통해 다음과 같은 $(x, y, z)$ 좌표를 얻을 수 있습니다.

<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/aa976aad-2aca-4380-bbe8-0869e1f5861c"> 
</p>

역기구학을 통해 얻어낸 $\psi$, $\theta_1$, $\theta_2$, $\theta_3$ 의 관계식입니다. <br/>
$\theta_3$ 는 지면과 항상 수평을 이뤄야하므로 $\theta_3 = \pi/2 - \theta_1 - \theta_2$

## Trajectory
<p align="center">
 <img width="80%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/d63207ff-c309-469b-ba68-e1eb24ed1321"> 
</p>

앞서 Scheme 에서 소개한 것 처럼 Trajectory 는 해당 블럭에서 생성하며 내부 구조는 아래와 같습니다.
<br/><br/>

<p align="center">
 <img width="60%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/a932b37d-5cc8-43ca-9c9e-e3966d90b68c"> 
</p>

좌측에 보이는 것 처럼 와플 데코레이션 캐릭터의 눈, 코, 입이 각각의 함수형태로 구현되어있습니다. 
시간(t)에 대해 그려져야하는 x,y,z 값을 만들고 다시 theta 로 변환하여 반환합니다.

<p align="center">
 <img width="85%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/5ef4fa5a-11e0-4623-9a16-12baffb9d451"> 
</p>

https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/38ba28b1-943a-4106-82b2-d1bb0b124f35

## Dynamics
<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/2bb162bf-1ab0-4b21-b805-50eed281c2b7"> 
</p>

$joint2$, $joint3$ 그리고 와플 플레이트의 중점을 질점으로 가정하였습니다. <br/>
기구학을 통해 얻어낸 각 질점 위치의 $(x, y, z)$ 좌표를 나타낸 식입니다.

## Control
해당 시뮬레이션에서는 SMC 제어를 수행하였습니다.

<p align="center">
 <img width="70%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/1a1372fa-4834-4345-94b3-457b4bcc0334"> 
</p>

Trajectory 의 desired theta 와 Manipulator 의 피드백 받은 현재 각도, 각속도를 가지고 제어를 수행합니다.

<p align="center">
 <img width="90%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/b5a86632-c2e6-42e9-b715-6bc5a14a9add"> 
</p>

해당 블럭의 내부구조 입니다. Manipulator 의 state 는 그대로 사용하고, desired theta 는 미분하여 desired dtheta, desired ddtheta 로 만들어서 사용합니다.

### k=10, c=10
<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/009378e1-a9e0-4daf-947e-88fa64175edd"> 
</p>

왼쪽 4개의 그래프는 각 조인트 프사이,세타1,2,3의 그래프이고, 오른쪽 3개의 그래프는 waffle-plate 의 x, y, z 그래프이며,
노란색이 desired 경로, 파란색이 실제 로봇이 움직인 경로를 나타냅니다.

k와 c가 모두 작아서, 조인트 각도들이 desired 각도와 일정한 오차를 유지하며 진행하고, 세타3의 경우 매우 큰 오차를 보입니다.
<br/><br/>

### k=10, c=50
<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/9cc671a7-e165-4a91-8203-cdfaaebd1cd0"> 
</p>
c값을 50으로 올려서 제어를 진행하였지만, 큰 변화는 관찰할 수 없었습니다.

따라서 저희는 k값이 작아서 sliding line에 도달하지 못해 큰 오차가 발생하는 것으로 추정하였습니다.
<br/><br/>

### k=30, c=50
<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/a034c6bf-c85b-4526-8658-a468ec1b893c"> 
</p>
k를 30으로 올려서 제어한 결과 desired 경로를 추종하지 못했던 문제가 해결되었습니다.

### k=30, c=10
<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/431ef733-7ead-4a23-a57d-c7174b6af9d6"> 
</p>
k값을 유지하고 c를 낮춘상태에서 제어했을때도 경로를 잘 추종하였습니다.

결과적으로 k=30, c=10으로 적절한 파라미터를 구할 수 있었습니다.
<br/><br/>

### k=30, c=10, with disturbance
<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/c4fc7359-aa96-45b1-a988-9297ce839245"> 
</p>
외란을 고려하여 추가적으로 시뮬레이션을 진행하였습니다.

disturbance = 0.1 sin(t)

결과를 보면 다른 조인트 각도들은 큰 영향을 받지 않지만, 비교적 link의 질량이 가벼운 세타3가 크게 요동치는 것을 확인할 수 있습니다.
<br/><br/>

### k=100, c=10, with disturbance
<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/53158981-4ee6-4fc8-a50b-ca7bad34c578"> 
</p>
k값을 키워주면 해결할 수 있으나, k=100처럼 너무 큰 값을 주게 되면 채터링이 커져 액츄에이터에 무리가 갈 수 있습니다.

<br/>

### k=50, c=60, with disturbance
<p align="center">
 <img width="100%" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/e9c21b9d-2b0c-4832-8fef-3cf4dd7691c2"> 
</p>
따라서 k값을 낮추고 c값을 조정하며 여러 번 시뮬레이션을 진행하여 desired trajectory를 잘 추종하는 파라미터를 도출하였고, 
결과적으로 적절한 계수를 k=50, c=60 얻을 수 있습니다.

<br/>
