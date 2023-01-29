## AWS_3-Tier_Infra
</br>
</hr>

![large Architecture](https://user-images.githubusercontent.com/117608997/215330995-0e11e851-e3ae-41f7-b1ff-18dd90494823.jpg)
###  💡 AWS를 활용해 기본적인 3-Tier 웹 서비스를 제공하고 S3를 활용한 정적 웹사이트 호스팅
</br>

![VPC](https://user-images.githubusercontent.com/117608997/215331179-01215ede-df9d-4391-85bd-c2134a0a23a5.jpg)
### 💡 VPC
- Public Subnet : 2개
- Private Subnet : 4개
- EFS Subnet : 2개
- NAT Gateway : 2개
</br>

### 💡 서브넷 추가 생성
- a 영역 Subnet : 10.0.4.0/24
- c 영역 Subnet : 10.0.44.0/24
</br>---

![Security Group](https://user-images.githubusercontent.com/117608997/215331194-dd4bff1f-f1fd-4b91-bb0d-6c013822d954.jpg)
### 💡 Security Group
- HTTP : Web Security Group
- SSH : SSH Security Group
- MySQL : DB Security Group
- EFS : EFS Security Group
</br>---

![RDS](https://user-images.githubusercontent.com/117608997/215331199-761ec737-47d4-4f9a-9bda-299510af5daf.jpg)
### 💡 DB Subnet 가용영역 추가
- Private 2a : 10.0.3.0/24
- Private 2c : 10.0.33.0/24
</br>---

![EC2](https://user-images.githubusercontent.com/117608997/215331207-35969406-3e73-4e14-ac3b-99b33f979655.jpg)
### 💡 EC2 인스턴스 Public 2c에 생성
</br>---

![EFS](https://user-images.githubusercontent.com/117608997/215331212-aa596faf-7e12-41fc-8e49-41950455e771.jpg)
### 💡 EFS 생성 후 영구 마운트 설정
</br>---

![Load Balancing](https://user-images.githubusercontent.com/117608997/215331227-b897c32e-d91e-491e-be83-73ed83d58975.jpg)
### 💡 Load Balancer Target Group 후 Load Balancer 생성
</br>---

![TargetGroup](https://user-images.githubusercontent.com/117608997/215333986-fe91473e-c282-4a32-a52a-c53386696eda.jpg)
### 💡 Target Group 생성
</br>---

![Load Balancer 생성](https://user-images.githubusercontent.com/117608997/215334100-15039965-990e-47f2-a46b-f7eb45223ff6.jpg)
### 💡 Load Balancer 생성
**< 기본구성 >**
- AteamLoadBalancer
- 인터넷 경계
- IPv4

**< 보안그룹 >**
- Web Security Group

**< 네트워크 매핑 >**
- VPC : A team- (public 2a/ public 2c)

**< 리스너 및 라우팅 >**
- HTTP : 80 (default)
</br>---

![Auto Scaling](https://user-images.githubusercontent.com/117608997/215331232-bb8dfc33-e5e7-4257-b42b-7b17624839cc.jpg)
### 💡 Auto Scaling AMI 이미지로 시작 그룹 생성 후 Auto Scaling 생성
</br>---

![AMI](https://user-images.githubusercontent.com/117608997/215333749-f880d18b-4983-42e7-be4a-d1913818107f.jpg)
### 💡 Auto Scaling AMI 이미지 생성
</br>---

![시작구성](https://user-images.githubusercontent.com/117608997/215333757-4674a58f-dce4-46f4-b6e8-deda93a9cd87.jpg)
### 💡 Auto Scaling 시작구성 생성 
**< 시작 구성 >**
- AMI 이미지 선택
- Load Test 확인을 위해 모니터링 활성화
- 인스턴스 유형 : t2.micro
- 보안그룹 : SSH, HTTP Security Group
- 키 페어 사용
</br>---

![AutoScaling  생성](https://user-images.githubusercontent.com/117608997/215333774-efba4114-10da-4afd-a857-e95e0df1338e.jpg)
### 💡 Auto Scaling 생성 
**< Auto Scaling 생성 구성>**
</br>
**- 1단계**
  - 생성한 시작 구성 선택

**- 2단계**
  - Auto Scaling 네트워크 설정

**- 3단계**
  - 고급 옵션 구성

**- 4단계**
  - 그룹 크기 및 크기 조정 정책 구성

**- 5,6단계**
  - 알림/태그 추가 설정 x
</br>---

![Auto Scaling 확인](https://user-images.githubusercontent.com/117608997/215333831-dca840b4-f27c-480d-bb3c-2de1feeaf6ed.jpg)
### 💡 Auto Scaling으로 인스턴스 최소 2개 증가 확인
</br>---

![가용영역 변경 확인](https://user-images.githubusercontent.com/117608997/215333845-d470ca85-630c-48ec-9f15-b37d751fbb11.jpg)
### 💡 로드밸런서 DNS로 접속 → 가용영역 변경 확인
</br>---

![인스턴스 증가](https://user-images.githubusercontent.com/117608997/215334420-7988ff65-8dfc-4466-ac49-34497d177e1a.jpg)
### 💡 부하 분산 및 Auto Scaling 확인
</br>---

![S3](https://user-images.githubusercontent.com/117608997/215331385-59945152-4262-484e-88b2-b900cf5e6357.jpg)
</br>

![S3 static 편집](https://user-images.githubusercontent.com/117608997/215333892-e543f8a2-97b0-45d3-aadc-f8701d158420.jpg)
### 💡 S3 버킷 생성 후 파일 업로드 및 퍼블릭 설정, Cloudfront에서 EC2 Load Balancer 배포
</br>

### 💡 Static Web Site 파일 S3에 추가
</br>---

![CloudFront](https://user-images.githubusercontent.com/117608997/215331915-aa259c14-3ef2-49e6-a6aa-93d290e7b517.jpg)
### 💡 생성한 도메인을 cloudfront에 대체도메인 추가 후 접속
</br>---

![Failover_normal](https://user-images.githubusercontent.com/117608997/215331395-429a806c-0ad3-446f-b140-5b9feb687ccf.jpg)
### 💡 정상 접속시 Web 확인
</br>---

![Failover_static](https://user-images.githubusercontent.com/117608997/215331422-ad9f9d25-1c3d-4086-b0b3-530a5d242bb8.jpg)
### 💡 장애 발생 후 도메인 접속 시 Statice Web 접속 확인
</br>---
