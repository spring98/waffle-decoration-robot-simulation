# Waffle Decoration Robot Simulation

## Preview
https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/4c35c273-1c62-4d75-ac70-3a0ae670f535

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
<img width="574" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/2bb162bf-1ab0-4b21-b805-50eed281c2b7">

$joint2$, $joint3$ 그리고 와플 플레이트의 중점을 질점으로 가정하였습니다. <br/>
기구학을 통해 얻어낸 각 질점 위치의 $(x, y, z)$ 좌표를 나타낸 식입니다.

## Control

### k=10, c=10
<img width="1000" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/009378e1-a9e0-4daf-947e-88fa64175edd">

왼쪽 4개의 그래프는 각 조인트 프사이,세타1,2,3의 그래프이고, 오른쪽 3개의 그래프는 waffle-plate 의 x, y, z 그래프이며,
노란색이 desired 경로, 파란색이 실제 로봇이 움직인 경로를 나타냅니다.

k와 c가 모두 작아서, 조인트 각도들이 desired 각도와 일정한 오차를 유지하며 진행하고, 세타3의 경우 매우 큰 오차를 보입니다.
<br/><br/>

### k=10, c=50
<img width="1000" alt="스크린샷 2024-05-15 14 12 24" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/9cc671a7-e165-4a91-8203-cdfaaebd1cd0">

c값을 50으로 올려서 제어를 진행하였지만, 큰 변화는 관찰할 수 없었습니다.

따라서 저희는 k값이 작아서 sliding line에 도달하지 못해 큰 오차가 발생하는 것으로 추정하였습니다.
<br/><br/>

### k=30, c=50
<img width="1000" alt="스크린샷 2024-05-15 14 12 40" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/a034c6bf-c85b-4526-8658-a468ec1b893c">

k를 30으로 올려서 제어한 결과 desired 경로를 추종하지 못했던 문제가 해결되었습니다.

### k=30, c=10
<img width="1000" alt="스크린샷 2024-05-15 14 12 55" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/431ef733-7ead-4a23-a57d-c7174b6af9d6">

k값을 유지하고 c를 낮춘상태에서 제어했을때도 경로를 잘 추종하였습니다.

결과적으로 k=30, c=10으로 적절한 파라미터를 구할 수 있었습니다.
<br/><br/>

### k=30, c=10, with disturbance
<img width="1000" alt="스크린샷 2024-05-15 14 13 15" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/c4fc7359-aa96-45b1-a988-9297ce839245">

외란을 고려하여 추가적으로 시뮬레이션을 진행하였습니다.

disturbance = 0.1 sin(t)

결과를 보면 다른 조인트 각도들은 큰 영향을 받지 않지만, 비교적 link의 질량이 가벼운 세타3가 크게 요동치는 것을 확인할 수 있습니다.
<br/><br/>

### k=100, c=10, with disturbance
<img width="1000" alt="스크린샷 2024-05-15 14 13 34" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/53158981-4ee6-4fc8-a50b-ca7bad34c578">

k값을 키워주면 해결할 수 있으나, k=100처럼 너무 큰 값을 주게 되면 채터링이 커져 액츄에이터에 무리가 갈 수 있습니다.

<br/>

### k=50, c=60, with disturbance
<img width="1000" alt="스크린샷 2024-05-15 14 14 50" src="https://github.com/spring98/waffle-decoration-robot-simulation/assets/92755385/e9c21b9d-2b0c-4832-8fef-3cf4dd7691c2">

따라서 k값을 낮추고 c값을 조정하며 여러 번 시뮬레이션을 진행하여 desired trajectory를 잘 추종하는 파라미터를 도출하였고, 
결과적으로 적절한 계수를 k=50, c=60 얻을 수 있습니다.

<br/>


## Integration


## Result
