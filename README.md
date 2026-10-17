# 페이지 사이 — 나만의 독서 아카이브

PC 브라우저에서 사용하는 독서 기록 앱입니다. 책·부제목·표지·최대 5단계 목차·본문 선택 주석(정의/나의 생각)·A4 인쇄를 지원합니다.

## 기록 안전 보관
- 기록은 입력 약 1초 후 자동으로 **이 브라우저에 먼저 저장**됩니다.
- Firebase 연결 후에는 Google 로그인 계정으로 Cloud Firestore에도 자동 저장되며 다른 PC와 동기화됩니다.
- 상단 **PC 파일 백업** 버튼을 누르면 JSON 파일로 책·목차·표지·기록·부제목을 내려받을 수 있습니다.
- 반드시 Firebase 설정 후 실제 클라우드 저장까지 완료되었는지 확인하세요. 동기화가 지연되면 백업 파일을 다운로드하세요.
- 기존 v7과 동일한 브라우저 저장 키 `pagesai.archive.v1`을 사용하며 기존 기록을 삭제하지 않습니다.
- 여러 PC에서 **같은 기록을 동시에 편집하지 않는 것**을 권장합니다. 최신 수정 시각을 기준으로 충돌을 처리합니다.

## Firebase 무료 설정 (처음 한 번)
1. [Firebase Console](https://console.firebase.google.com/)에서 프로젝트를 만듭니다. 사용량이 적다면 무료 Spark 요금제를 선택하세요.
2. **Authentication → Sign-in method → Google**을 활성화합니다.
3. **Authentication → Settings → Authorized domains**에 `hyunjint.github.io`를 추가합니다.
4. **Firestore Database**를 생성하고 **Rules** 탭에 이 저장소의 [firestore.rules](./firestore.rules)를 입력해 게시합니다. 공개 테스트 규칙을 그대로 사용하지 마세요.
5. **Project settings → Your apps → Web app**에서 웹앱을 등록하고 Firebase 웹 설정 `firebaseConfig` 객체를 복사합니다.
6. 앱 **설정 → Firebase 웹앱 설정(JSON)**에 웹 설정 내용을 붙여넣고 **Google 로그인 및 연결**을 누릅니다.
7. 클라우드 저장이 완료된 후 다른 PC에서도 설정 없이 로그인하려면, 공개해도 되는 웹 설정 객체를 이 저장소의 `firebase-config.json`에 추가하면 됩니다. **절대 서비스 계정 키나 비밀번호를 넣지 마세요.**

`firebase-config.json` 예:
```json
{
  "apiKey": "YOUR_PUBLIC_WEB_API_KEY",
  "authDomain": "YOUR_PROJECT.firebaseapp.com",
  "projectId": "YOUR_PROJECT_ID",
  "appId": "YOUR_APP_ID"
}
```

**중요:** 웹 설정 JSON만 올린다고 데이터베이스가 자동 생성되지는 않습니다. Authentication 및 Firestore 보안 규칙을 먼저 설정해야 합니다. 클라우드 연동 전 데이터는 해당 PC 브라우저에만 저장됩니다.
