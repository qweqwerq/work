# ■MySQL 8.0.31 Cluster 구성■

### ● 구성도
![image description](https://user-images.githubusercontent.com/8789421/216266513-7ba0c569-4e77-49af-ac62-99952cf39763.png)

>서비스IP : <3번 서버 IP>
>서비스포트 (Read/Write용) : 6446
>서비스포트 (Read용) : 6447


## **※ NOTICE!! ※**
  
● PK 사용 필수 (PK 사용하지 않을 경우 클러스터 구성 에러발생)
  
● PK 생성을 안하고 테이블 생성 시, Error나 Warning을 제공해주지 않지만, sql_require_primary_key 셋팅 (0 --> 1) 으로 Error 제공 기능 활성화
  
● PK 자동 생성 => SET sql_generate_invisible_primary_key=ON;  
  
