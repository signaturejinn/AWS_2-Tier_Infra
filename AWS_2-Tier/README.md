## VPC 생성
![image](https://user-images.githubusercontent.com/117608997/216535436-c901f042-fe03-4325-8774-702eb021f1d5.png)


### 💡 VPC
- Public Subnet : 2개
- Web Subnet : 2개
- DB Subnet : 2개
- EFS Subnet : 2개
- NAT Gateway : 2개
</br>

### 💡 서브넷 추가 생성
- a 영역 Subnet : 10.0.4.0/24
- c 영역 Subnet : 10.0.44.0/24
</br>
<hr/>

## Security Group 생성
![image](https://user-images.githubusercontent.com/117608997/216542776-fae05863-072e-4fe2-ae94-567035ce83e2.png)

### 💡 Security Group
- HTTP : Web Security Group
- MySQL : DB Security Group
- EFS : EFS Security Group
</br>
<hr/>

## RDS 생성
![image](https://user-images.githubusercontent.com/117608997/216536797-4bf0b531-099e-4b9b-9d3e-9cb9f4e2bce0.png)

### 💡 DB Subnet 가용영역 추가
- Private 2a : 10.0.3.0/24
- Private 2c : 10.0.33.0/24
</br>
<hr/>

## EC2 생성
![image](https://user-images.githubusercontent.com/117608997/216537101-cc064bbf-7980-4581-b379-a58460b42a59.png)

### 💡 EC2 인스턴스 Public 2c에 생성
</br>
<hr/>

## EFS 생성
![image](https://user-images.githubusercontent.com/117608997/216538453-0aab5944-caf7-4b91-a8ff-2451d5e8df2b.png)

### 💡 EFS 생성 후 영구 마운트 설정
</br>
<hr/>

## Load Balancer
![image](https://user-images.githubusercontent.com/117608997/216538813-74fb2c19-214e-4d61-b967-7d5ad354d2a5.png)

### 💡 Load Balancer Target Group 후 Load Balancer 생성
</br>
<hr/>

![TargetGroup](https://user-images.githubusercontent.com/117608997/215333986-fe91473e-c282-4a32-a52a-c53386696eda.jpg)
### 💡 Target Group 생성
</br>
<hr/>

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
</br>
<hr/>

## Auto Scaling
![image](https://user-images.githubusercontent.com/117608997/216540912-9b53d90d-fb8b-4185-85ee-9c6189dfe530.png)

### 💡 Auto Scaling AMI 이미지로 시작 그룹 생성 후 Auto Scaling 생성
</br>
<hr/>

![AMI](https://user-images.githubusercontent.com/117608997/215333749-f880d18b-4983-42e7-be4a-d1913818107f.jpg)
### 💡 Auto Scaling AMI 이미지 생성
</br>
<hr/>

![시작구성](https://user-images.githubusercontent.com/117608997/215333757-4674a58f-dce4-46f4-b6e8-deda93a9cd87.jpg)
### 💡 Auto Scaling 시작구성 생성 
**< 시작 구성 >**
- AMI 이미지 선택
- Load Test 확인을 위해 모니터링 활성화
- 인스턴스 유형 : t2.micro
- 보안그룹 : SSH, HTTP Security Group
- 키 페어 사용
</br>
<hr/>

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
</br>
<hr/>

![Auto Scaling 확인](https://user-images.githubusercontent.com/117608997/215333831-dca840b4-f27c-480d-bb3c-2de1feeaf6ed.jpg)
### 💡 Auto Scaling으로 인스턴스 최소 2개 증가 확인
</br>
<hr/>

![가용영역 변경 확인](https://user-images.githubusercontent.com/117608997/215333845-d470ca85-630c-48ec-9f15-b37d751fbb11.jpg)
### 💡 로드밸런서 DNS로 접속 → 가용영역 변경 확인
</br>
<hr/>

![인스턴스 증가](https://user-images.githubusercontent.com/117608997/215334420-7988ff65-8dfc-4466-ac49-34497d177e1a.jpg)
### 💡 부하 분산 및 Auto Scaling 확인
</br>
<hr/>

## S3
![image](https://user-images.githubusercontent.com/117608997/216542241-f31814a2-ca2b-4f41-8c11-fefb4bc88554.png)

</br>

![S3 static 편집](https://user-images.githubusercontent.com/117608997/215333892-e543f8a2-97b0-45d3-aadc-f8701d158420.jpg)
### 💡 S3 버킷 생성 후 파일 업로드 및 퍼블릭 설정, Cloudfront에서 EC2 Load Balancer 배포
</br>

![S3](https://user-images.githubusercontent.com/117608997/215331385-59945152-4262-484e-88b2-b900cf5e6357.jpg)
### 💡 Static Web Site 파일 S3에 추가
</br>
<hr/>

## Cloud Front 및 Failover
![CloudFront](https://user-images.githubusercontent.com/117608997/215331915-aa259c14-3ef2-49e6-a6aa-93d290e7b517.jpg)

### 💡 생성한 도메인을 cloudfront에 대체도메인 추가 후 접속
</br><hr/>

![Failover_normal](https://user-images.githubusercontent.com/117608997/215331395-429a806c-0ad3-446f-b140-5b9feb687ccf.jpg)
### 💡 정상 접속시 Web 확인
</br><hr/>

![Failover_static](https://user-images.githubusercontent.com/117608997/215331422-ad9f9d25-1c3d-4086-b0b3-530a5d242bb8.jpg)
### 💡 장애 발생 후 도메인 접속 시 Statice Web 접속 확인
</br><hr/>
