컨트롤 플레인 컴포넌트는 어떠한 머신에서든지 동작 할 수 있지만, 간결성을 위해 사용자 컨테이너와 분리한다.

## Control Plane Component

### kube-apiserver
---
쿠버네티스 API를 노출한다.
- API서버는 쿠버네티스 컨트롤 플레인의 **프론트 앤드**이다.
수평으로 확장 가능하다.
여러 인스턴스를 실행하고, 인스턴스간의 트래픽을 균형 있게 조절 할 수 있다.

[쿠버네티스 API 서버의 주요 구현](https://kubernetes.io/docs/reference/generated/kube-apiserver/)
### etcd
---
모든 클러스터 데이터를 담는 쿠버네티스 뒷단의 **저장소**로 사용되는 일관성·고가용성 key-value 저장소이다.
- 쿠버네티스 클러스터에서 etcd를 뒷단의 저장소로 사용한다면, 이 데이터를 백업하는 계획은 필수이다.
- [백업 참조](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster)
- [공식 문서 참조](https://etcd.io/docs)

### kube-scheduler
---
노드가 배정되지 않은 새로 생성된 파드를 감지하고, 실행할 노드를 선택한다.

> 스케쥴링 고려 요소
> - 리소스에 대한 개별 및 총체적 요구 사항
> - 하드웨어 제약
> - 소프트웨어 제약
> - 정책적 제약
> - 어피니티(affinity) 및 안티-어피티니(anti-affinity) 명세
> - 데이터 지역성
> - 워크로드간 간섭
> - 데드라인

### kube-controller-manager
---
컨트롤러 프로세스를 실행

> 논리적으로 각 컨트롤러는 분리된 프로세스이지만, 복잡성을 낮추기 위해 모두 단일 바이너리로 컴파일되고 단일 프로세스 내에서 실행된다.

- NodeController: 노드가 다운되었을 때 통지와 대응에 관한 책임을 가진다.
- JobController: 일회성 작업을 나타내는 **잡 오브젝트**를 감시한 다음, 해당 작업을 완료할 때까지 동작하는 파드를 생성한다.
- EndpointSliceController: EndpointSlice Object를 채운다.(서비스와 파드 사이의 연결고리를 제공하기 위해)
- ServiceAccountController: 새로운 Namespace에 대한ServiceAccount를 생성한다.

### cloud-controller-manager
---
클라우드 별 **컨트롤 로직**을 포함하는 컴포넌트이다.

> 클러스터를 **클라우드 공급자의 API에 연결**하고, 해당 클라우드 플랫폼과 상호작용하는 컴포넌트와 클러스터와 클러스터와만 상호작용하는 컴포넌트를 구분 할 수 있게 해준다.
> 클라우드 제공자 전용 컨트롤러만 실행한다.
> 
> kube-controller-manager와 마찬가지로 독립적인 여러 컨트롤 루프를 단일 프로세스로 실행하는 단일 바이너리로 결합한다.
> 수평적 확장이 가능하다.

- NodeController: 노드가 응답을 멈춘 후 클라우드 상에서 삭제되었는지 판별하기 위해 클라우드 제공 사업자에게 확인
- RouteController: 기본 클라우드 인프라에 경로를 구성
- ServiceController: 클라우드 제공 사업자 로드벨런서를 생성, 업데이트 및 삭제



