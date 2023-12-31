# MRP

> 1. $v(s) = E[R_{t+1} + \gamma v(S_{t+1}) | S_t = s]$
> 2. $v(s) = R_{t+1} + \gamma E[v(S_{t+1})|S_t = s]$
> 3. $v(s) = R_{t+1} + \gamma\sum_{s' \in S}P_{ss'}v(s')$
# MDP

> 1. $v_{\pi}(s) = E_{\pi}[R_{t+1} + \gamma v_{\pi}(S_{t+1}) | S_t = s]$
> 2. $v_{\pi}(s) = \sum_{a \in A}\pi(a | s)\left (R^a_s + \gamma \sum_{s' \in S} P^a_{ss'}v_{\pi}(s')\right)$
> 3. $v_{\pi}(s) = \sum_{a \in A}\pi(a | s)R^a_s + \gamma\sum_{a \in A}\pi(a | s)\sum_{s' \in S}P^a_{ss'}v_{\pi}(s')$

1. [[상태 가치 함수(MRP)]]와 동일하나 정책($\pi$)이 고려되었다.
2. 정책은 행동을 선택하기 위한 확률이고 하나의 상태에서 선택할 수 있는 행동에 대한 확률의 합은 1이다. 정책에 대한 기대값을 구하기 위해서는 *선택 할 수 있는 행동별로 조건부 확률(정책)을 곱하여 합산해야 한다.*
3. 상태 S에서 정책을 고려한 직접적인 보상을 계산
	1. 정책과 상태 전이 매트릭스를 함께 고려해야 하기 때문에 $\sum$이 여러번 사용 되었다.
		1. 첫번째는 **행동별 정책**
		2. 두번째는 **상태별 전이 확률**

이를 보다 더 간단한 형태로 나타낼 수 있다.

> 1. $v_{\pi}(s) = R^{\pi} + \gamma P^{\pi}v_{\pi}$
> 	1. 직접적인 보상은 [[정책]] $\pi$를 따랐을 경우의 보상을 계산하는 것임($R^\pi$)
> 	2. 다음 타임스텝에서 받을 수 있는 보상의 경우에는 [[정책]] $\pi$를 따랐을 경우에 받을 보상 + 상태 전이 확률  + [[감가율]]을 동시에 고려한다.
> 2. $v_{\pi}(s) = (1 - \gamma P^{\pi})^{-1}R^{\pi}$
> 	1. 정책, 보상, 상태 전이 확률, 감가율만을 사용해서 상태 전이 확률을 구하기 위해서는 $\gamma P{^\pi}v_{\pi}$ 를 좌변으로 넘겨서 $v_\pi$로 묶고 양변을 나눠주면 된다.