## Node Component

### kubelet
---
파드에서 컨텐이너가 확실하게 동작하도록 관리한다.
- 각 노드에서 실행되는 에이전트이다.
- 다양한 메커니즘을 통해 제공된 **PodSpec**의 집합을받아서 컨테이너가 해당 파드 스펙에 따라 건강하게 동작하는 것을 확실히 한다.
- **쿠버네티스**를 통해 생성되지 않는 컨테이너는 관리하지 않는다.

### kube-proxy
---
클러스터의 각 노드에서 실행되는 네트워크 프록시이다.
- 네트워크 규칙을 유지 관리한다.
- 내부 세션이나 클러스터 바깥에서 파드로 네트워크 통신을 할 수 있도록 해준다.
- OS에 가용한 패킷 필터링 계층이 있는 경우 이를 사용한다. 그렇지 않으면 트래픽을 forward 한다.
### 컨테이너 런타임
---
컨테이너 실행을 담당하는 소프트웨어이다.
containerd, CRI-O와 같은 런타임 및 모든 [kubernetes CRI](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md)구현체를 지원한다.