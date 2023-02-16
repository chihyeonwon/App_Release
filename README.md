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

### STEP2 업로드 키 생성
[JAVA 설치](https://www.java.com/ko/download)
```
업로드 키를 생성하려면 먼저 JAVA를 설치합니다. flutter doctor -v 명령을 실행해서
Java binary at에 보이는 경로 끝에 있는 java를 keytool로 변경하고 PATH에 경로를 추가합니다.

윈도우에서 업로드키를 생성하는 명령어를 입력해줍니다.
keytool -genkey -v -keystore ./upload-keystore.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias upload

현재 위치에 upload-keystore.jks 파일이 생성됩니다.
```
### [flutter doctor -v 실행]
![image](https://user-images.githubusercontent.com/58906858/219276631-abf7c21e-e8ec-4869-a6be-6c8a75a2548e.png)

### [환경 변수 PATH에 경로 추가]
![image](https://user-images.githubusercontent.com/58906858/219276814-e7d67309-c451-45d1-8a5d-49c5d76bf345.png)

### 윈도우에서 업로드 키 생성
![image](https://user-images.githubusercontent.com/58906858/219279287-2b2ebe56-2e46-47b5-98ef-86f1d25c9479.png)

### 업로드 키 설정
```
android 폴더에 key.properties 파일을 생성한 후
storePassword=<키를 생성할 때 입력한 비밀번호>
keyPassword=<키를 생성할 때 입력한 비밀번호>
keyAlias=upload
storeFile=<키 파일의 위치>
를 넣어줍니다.

key.properties 파일을 android/app/build.gradle 파일에 설정해주어야 합니다.
android 블록 바로 위에 다음 코드를 추가합니다.
android 블록 안에도 코드를 추가합니다.
```
### android/key.properties
![image](https://user-images.githubusercontent.com/58906858/219279792-63c8ddd3-263e-4206-b0b9-ff2575bf381b.png)

### android/app/build.gradle (android 블록 위)
![image](https://user-images.githubusercontent.com/58906858/219280191-720f1395-fc58-4ca3-bb20-c6db17f80de5.png)

### android/app/build.gradle (android 블록 내)
![image](https://user-images.githubusercontent.com/58906858/219280640-d75aa9c7-9bf6-42cc-bdcb-acdb2cb2f98e.png)

## 앱 이름 설정하기
```
출시할 앱의 이름을 설정할 차례입니다. android/app/src/main/AndroidManifest.xml 파일의 android:label 값을
원하는 앱 이름으로 변경해줍니다. 앱 이름을 원주대 등교로 설정하였습니다.
```
![image](https://user-images.githubusercontent.com/58906858/219280977-71d463b5-dede-4c47-a2f2-212c3c92c3f9.png)

## 앱 번들 생성하기
```
앱 번들은 앱을 플레이 스토어에 업로드할 수 있는 형태로 하나의 파일로 플러터 앱이 포장됩니다.
flutter build appbundle 명령어를 실행하여 앱 번들을 생성합니다.
파일의 경로는 build/app/outputs/bundle/release에 있습니다.
```
![image](https://user-images.githubusercontent.com/58906858/219284881-cae287dd-be46-4525-88ce-19979040895d.png)
