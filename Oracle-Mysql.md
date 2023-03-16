<h2>● **MySQL 8.0.31 Cluster 구성**

**구성도**
>![image](https://user-images.githubusercontent.com/88891704/225607734-511591c5-79aa-4d20-acdc-b6c79ff51d9f.png)
>서비스IP : <3번 서버 IP>
>서비스포트 (Read/Write용) : 6446
>서비스포트 (Read용) : 6447


**※ NOTICE!! ※**
PK 사용 필수 (PK 사용하지 않을 경우 클러스터 구성 에러발생)
PK 생성을 안하고 테이블 생성 시, Error나 Warning을 제공해주지 않지만, sql_require_primary_key 셋팅 (0 --> 1) 으로 Error 제공 기능 활성화
PK 자동 생성 => SET sql_generate_invisible_primary_key=ON;
