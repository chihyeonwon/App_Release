# App_Release
구글 플레이스토어 플러터 앱 출시 과정 정리


## 원주대 등교 앱 출시 개요
```
현재 내가 재학 중인 대학교의 출석 시스템은 교수님께서 임의의 출석 번호를 보여주면 해당하는 
출석 번호를 어플에 입력하는 형태로 이루어져 있다. 하지만 이러한 출석 방식은 부정 출석의 우려가 있다고 개인적으로
판단하여 구글 GPS 기능을 이용한 출석 시스템으로 개선하면 어떨까 해서 개발해 보았다.

이 앱은 목적지의 근방 200m로 이동하여 출석 버튼을 눌러야만 정상적으로 출석이 인정되어 카운트가 올라간다.

테스트용앱이기에 카운트가 올라가는 것 말고는 기능을 더 추가하지는 않았다.
하지만 출석하고자 하는 학생의 정보를 입력하고 핸드폰 내에 저장하는 기능은 추가하였다.
```
![image](https://user-images.githubusercontent.com/58906858/219273873-e2873a38-94c5-4386-bee8-bce618f3acc2.png)
![image](https://user-images.githubusercontent.com/58906858/219273823-a60251d0-848c-4682-b3de-e290408850d7.png)
![image](https://user-images.githubusercontent.com/58906858/219273749-961bdf81-923a-40ba-9a6f-a4e10768208b.png)

## STEP 1 앱 Bundle ID 설정하기
```
앱 Bundle ID는 앱을 식별하는 유일한 값으로 세 개의 마침표를 구분해서 입력합니다.
직접 모든 파일에 적혀 있는 Bundle ID를 수정할 수 있지만 실수가 생길 수도 있고 시간이 오래 걸리기에 플러그인의 도움을 받습니다.
pubspec.yaml 파일의 dev_dependencies에 change_app_package_name을 추가하고 pub get을 한 다음
flutter pub run change_app_package_name:main {Bundle ID 입력} Bundle ID에 com.wonchihyeon.wonjuCulcheck을 넣었습니다.

파이어스토어 데이터베이스를 사용한다면 flutterfire configure로 앱 번들 id를 파이어베이스에 등록합니다.
```
![image](https://user-images.githubusercontent.com/58906858/219274689-66a6c77a-efec-45a2-8b28-301aca6a9826.png)
![image](https://user-images.githubusercontent.com/58906858/219275097-72cb5047-e98d-411f-8fd0-b95fd482daa8.png)
