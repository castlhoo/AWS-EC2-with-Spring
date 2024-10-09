# AWS-EC2-with-Spring
AWS에 EC2를 형성하고, 우분투에서 Docker.io에서 Image를 받고 실행시키고, 이에 대한 Jmeter Test
1. EC2 형성 (Public)
  1) VPC 형성
  ![KakaoTalk_20241008_094745768](https://github.com/user-attachments/assets/8534b9c8-178c-4c02-8ed3-4927f62b61dc)
  2) 서브넷 형성
  ![image](https://github.com/user-attachments/assets/f05fd257-3779-42c1-8ad0-52e795e0cb3f)
  3) 라우팅 테이블 생성
  ![image](https://github.com/user-attachments/assets/2aad6964-1715-41bf-949d-d844f8fba374)
    - 라우팅 테이블에서 형성한 서브넷을 할당
     ![image](https://github.com/user-attachments/assets/245dae78-e184-4455-a5dc-e46615e781ed)
  4) 인터넷 게이트웨이 생성
  ![image](https://github.com/user-attachments/assets/fcc19ebb-3bc2-4ed5-8078-4ef622cb4336)
    - 인터넷 게이트웨이 생성 후, 생성했던 VPC에 할당
     ![image](https://github.com/user-attachments/assets/64937161-f4b2-45a7-ac7b-1d1dcc717d83)
  5) 라우팅 테이블에서 형성한 게이트웨이 할당
  ![image](https://github.com/user-attachments/assets/9f6ebf42-193f-4957-9974-03dc4ddbfabf)
  6) VPC 형성 완료
  ![image](https://github.com/user-attachments/assets/9d76560f-0084-4a55-a15e-23e1e0ae8c90)
  7) AWS EC2 형성을 위한 보안그룹 생성
     - HTTP, SSH 모두가 접근할 수 있도록 0.0.0.0/0 으로 설정
  ![image](https://github.com/user-attachments/assets/4dabb054-59b3-486d-ad7c-969aa5e194f3)
  8) AWS EC2 형성
    - 운영체제 선택
    ![image](https://github.com/user-attachments/assets/767705f9-363f-4193-ad29-0107c96de80e)
    - 키 페어 선택
     ![image](https://github.com/user-attachments/assets/47faae35-14ae-4c83-a351-dd17aeb8fc2a)
    - VPC 및 보안그룹 선택
     * 퍼블릭 IP 활성화 필수
     ![image](https://github.com/user-attachments/assets/d8a938a6-cf69-4dca-ac90-76ec90589a0b)
  8) 결과
  ![image](https://github.com/user-attachments/assets/504e1e0a-8f57-4dd4-9a32-6decd5587926)
  9) MobaXTerm을 통한 우분투 접속
    - 퍼블릭 IP 할당 및 접속
  ![image](https://github.com/user-attachments/assets/18b1265c-ad68-4a76-8964-72b47fea96a5)
  ![image](https://github.com/user-attachments/assets/660f4a4d-9536-4b81-827e-6135b7b5302e)



     



