## AWS_3-Tier_Infra
![large Architecture](https://user-images.githubusercontent.com/117608997/215330995-0e11e851-e3ae-41f7-b1ff-18dd90494823.jpg)
### - AWS를 활용해 기본적인 3-Tier 웹 서비스를 제공하고 S3를 활용한 정적 웹사이트 호스팅
</br>

![VPC](https://user-images.githubusercontent.com/117608997/215331179-01215ede-df9d-4391-85bd-c2134a0a23a5.jpg)
### <VPC>
- Public Subnet : 2개
- Private Subnet : 4개
- EFS Subnet : 2개
- NAT Gateway : 2개

### < 서브넷 추가 생성 >
- a 역 Subnet : 10.0.4.0/24
- c 영역 Subnet : 10.0.44.0/24
</br>

![Security Group](https://user-images.githubusercontent.com/117608997/215331194-dd4bff1f-f1fd-4b91-bb0d-6c013822d954.jpg)
### < Security Group >*
- HTTP : Web Security Group
- SSH : SSH Security Group
- MySQL : DB Security Group
- EFS : EFS Security Group

![RDS](https://user-images.githubusercontent.com/117608997/215331199-761ec737-47d4-4f9a-9bda-299510af5daf.jpg)
![EC2](https://user-images.githubusercontent.com/117608997/215331207-35969406-3e73-4e14-ac3b-99b33f979655.jpg)
![EFS](https://user-images.githubusercontent.com/117608997/215331212-aa596faf-7e12-41fc-8e49-41950455e771.jpg)
![Load Balancing](https://user-images.githubusercontent.com/117608997/215331227-b897c32e-d91e-491e-be83-73ed83d58975.jpg)
![Auto Scaling](https://user-images.githubusercontent.com/117608997/215331232-bb8dfc33-e5e7-4257-b42b-7b17624839cc.jpg)
![S3](https://user-images.githubusercontent.com/117608997/215331385-59945152-4262-484e-88b2-b900cf5e6357.jpg)
![Failover_normal](https://user-images.githubusercontent.com/117608997/215331395-429a806c-0ad3-446f-b140-5b9feb687ccf.jpg)
![Failover_static](https://user-images.githubusercontent.com/117608997/215331422-ad9f9d25-1c3d-4086-b0b3-530a5d242bb8.jpg)
