안드로이드(모바일) 보안 테스트 및 취약점 진단 

 보안테스트 환경 구축
  
- Android 기기: Android Studio / Android Virtual Device (6.0, 마시멜로 OS) - 주 테스트 환경
                        스마트폰 - 보조(Cross-Check) 환경

  - APK 분석 및 취약점 진단 도구

   ① APK EasyTool : https://apk-easy-tool.en.lo4d.com/windows / APK 디컴파일과 재 컴파일 도구 
   ② dex2jar: https://sourceforge.net/projects/dex2jar/ / APK 압축 해제 후 .dex 파일을 jar 파일로 변환
   ③ JAVA Decompiler: https://github.com/java-decompiler/jd-gui/releases / jar 파일에서 JAVA Class 소스코드 추출 도구
   ④ adb.exe: https://developer.android.com/studio/command-line/adb?hl=ko  / 안드로이드 장치 연결 및 제어 도구 
   ⑤ tcpdump: https://ko.wikipedia.org/wiki/Tcpdump / 패킷 캡쳐 도구
   ⑥ Wireshark: https://www.wireshark.org/download.html / 패킷 캡쳐 및 분석 도구
   ⑦ HxD: https://mh-nexus.de/en/hxd/ / 헥사(바이너리코드) 데이터 분석 도구
   ⑧ Android Studio: https://developer.android.com/studio/ / 안드로이드 앱 개발 및 에뮬레이터 도구

  -  배포된 앱을 대상으로 한 보안 테스트(취약점 진단 절차)
    ① 안드로이드 실제폰을 이용하여, 구글 PlayStore에서 대상 앱 다운로드 및 기본 동작 확인
    ② APK 추출  
    ③ Android Virtual Device에 추출한 APK 설치
    ④ 보안 테스트 및 취약점 점검 수행

보안테스트/ 취약점 점검 항목
  - Ref: https://www.owasp.org/index.php/OWASP_Mobile_Security_Project#tab=Top_10_Mobile_Risks
            https://www.boannews.com/media/view.asp?idx=56892
            Black Falcon

|구분|취약점 설명|점검 및 테스트 항목|
|----|----------|-----------------|
|M1. 적절하지 않은 플랫폼 사용|- 플랫폼의 보안 개발지침 위반
- 개발/운영 중 실수|* 설치 : adb install ImageViewer-debug.apk
M1-01) 과도한 앱 권한 요청 여부
M1-02) 안드로이드 가상장치 실행 여부
※ http://www.bluestacks.co.kr|
M2. 취약한 데이터 저장소
- 취약한 데이터 저장소
- 의도하지 않은 데이터 노출
M2-01) App 저장소 정책 적절성 (Private, Public)

-----------------------------------------------------------------
adb shell : 진입
cd data
cd data
cd com.example.boanteam.imageviewer
cd files
cat hello.txt :   확인

echo “1234” > hello.txt
-----------------------------------------------------------------

M2-02) 민감 데이터 저장 여부 (sqlite, 개인정보, 사용자 정보)

M2-03) 데이터 변조 여부 (파일 내용 변경 후 App 동작 영향)

M2-04) M5 항목의 취약한 암호화 함께 점검
M3. 취약한 통신
- 악의적인 핸드 세이킹
- 잘못된 SSL 버전
- 만감정보 평문통신
M3-01) ID/PW 전송시 SSL(암호화) 적용 여부
M3-02) 민감정보 전송시 SSL(암호화) 적용 여부

-----------------------------------------------------------------
<안드로이드에서 실행할 수 있는 tcpdump를 설치>
1) adb push tcpdump /sdcard/Download
2) adb shell 
3) cd /sdcard/Download
4) tcpdump -w data.pcap  => ctrl+c
5) adb pull /sdcard/Download/data.pcap ./

* 프로그램은 WebBrowser
-----------------------------------------------------------------
M4. 취약한 인증
- 사용자 식별 불가
- 사용자 신원 유지
- 세션 관리 취약점
M4-03) ID/PW 무작위 공격 취약점 (입력 제한 적용 여부)
M5. 취약한 암호화
- 데이터 암호화, 복호화 알고리즘 취약점
※ M2 항목과 함께 점검
M6. 취약한 권한부여
- 클라이언트 권한부여, 강제 검색
M6-01) 인증 우회 후 주요 기능 사용 (인증 Activity 우회 등)

-----------------------------------------------------------------
adb shell
am start -n 패키지이름/Activity이름
ex) am start -n com.example.boanteam.imageviewer/.TextEditActivity
-----------------------------------------------------------------

M7. 취약한 코드 품질
- 버퍼 오버플로우, 형식문자열 등
M7-01) 민감 정보 입력창 필터링 (Security 속성 미적용 여부)
M8. 코드 변조
- 바이너리 패치, 로컬 리소스 수정, 메소드 후킹/변경
- 메모리 수정
M8-01) 항목의 리버스 엔지니어링, 재 패키지 여부
M8-02) M8-01이 안될 경우, APK 수정 후 추출
M8-03) 앱 변조(무결성) 점검 여부 확인
M8-04) 주요 정보 변경 (URL link 등)
M8-05) 사용자 화면 정보 변경 (이미지, Text, Layout  등)
M8-06) 앱 기능/구조 변경 (Activiy, Filter 수정) 
M9. 리버스 엔지니어링
- 최종 코어 바이너리 분석
- 백엔드, 암호화 상수 및 핵심 재산 정보 공개 확인
- 앱 초기 취약점 악용
M9-01) Progaurd 적용 여부
M9-02) 소스코드 내 민감정보 여부 확인
M10. 불필요한 기능
- 숨겨진 백도어
- 개발 단계의 테스트 기능
M10-01) 개발(테스트) 기능, 불필요한 코드 여부
               Manifest 파일, 코드 리뷰
※ 테스트 과정 중, ‘개발 코드, 검증 위한 데이터 등’이 있는지 확인

