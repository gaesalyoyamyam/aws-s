## 사랑해요 쿨러스터
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: skills-cluster #이름
  region: ap-northeast-2 #리전
  version: "1.22" #버전
cloudWatch:
  clusterLogging:
    enableTypes: ["*"] #로깅
  # clusterLogging:
  #   enableTypes:
  #   - api
  #   - audit
  #   - authenticator
  #   - controllerManager
  #   - scheduler
iam:
  withOIDC: true #클러스터 보안 이증서 발급
vpc:
  id: vpc-xxxxxxxxxxxxxxxxx #VPC ID
  subnets:
    public:
      ap-northeast-2a-pub: { id: $subnet_id }
      ap-northeast-2b-pub: { id: $subnet_id }
      # ap-northeast-2c-pub: { id: $subnet_id }
    private:
      ap-northeast-2a-priv: { id: $subnet_id }
      ap-northeast-2b-priv: { id: $subnet_id }
      # ap-northeast-2c-priv: { id: $subnet_id }
managedNodeGroups:
  - name: skills-app #노드그룹 이름
    instanceName: skills-app #EC2 인스턴스 이름
    labels: { skills/dedicated: app } #노드그룹 라벨
    tags: { skills/dedicated: app } #노드그룹 태그
    instanceType: c5.large #인스턴스 타입
    minSize: 2 #최소 노드 수
    maxSize: 20 #최대 노드 수
    desiredCapacity: 2 #원하는 노드 수
    privateNetworking: true #프라이빗 네트워크 없으면 자동으로 퍼블릭 인스턴스로됨
    subnets: #퍼블릭 주소 원하지 않으면 프라이빗 서브넷만 추가
     - ap-northeast-2a-priv
     - ap-northeast-2b-priv
     - ap-northeast-2c-priv
    iam: 
      withAddonPolicies:
        imageBuilder: true #ECR
        autoScaler: true #오토스케일링
        awsLoadBalancerController: true #ALB
        cloudWatch: true #클라우드워치
```
