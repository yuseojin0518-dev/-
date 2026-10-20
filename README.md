# EduSpace — 우리 반 올인원 협업 공간

Flask 기반 학급 협업 웹앱입니다. 나이스 학사일정·급식 조회, 공유 달력, 클래스룸과 과제 제출, 문서함, 실시간 공유 노트, 손필기, 공부 타이머를 한곳에서 제공합니다.

## 기능

- 학교 검색, 학사일정과 급식 (나이스 API 키가 없으면 예시 데이터로 동작)
- 반 단위 공유 달력과 댓글
- 과목별 클래스룸, 과제·질문·제출·채점
- 파일 문서함과 버전 관리
- 여러 사용자의 실시간 공유 노트와 손필기
- 서버 기반 공부 타이머와 반 순위
- PWA 설치 지원

## 로컬 실행

Python 3.11 이상을 권장합니다.

```bash
python -m venv .venv
# Windows: .venv\\Scripts\\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env  # Windows PowerShell: Copy-Item .env.example .env
python app.py
```

`http://127.0.0.1:5000`에서 엽니다. 운영 환경에서는 Gunicorn과 환경 변수를 사용하세요.

## Render 배포

저장소 루트의 `render.yaml`은 Render에서 무료 데모 서비스를 만들 수 있도록 준비되어 있습니다.

1. Render 계정에 로그인합니다.
2. 대시보드에서 **New → Blueprint**를 선택합니다.
3. GitHub 저장소 `yuseojin0518-dev/-`를 연결하고 `render.yaml` 설정을 적용합니다.
4. 배포가 끝나면 Render가 제공하는 `https://...onrender.com` 주소를 다른 사람에게 공유합니다.

무료 설정은 빠르게 시연하기 위한 구성입니다. `/tmp`에 SQLite 데이터와 업로드 파일을 보관하므로 재배포·재시작·인스턴스 재생성 후 데이터가 유지된다고 보장할 수 없습니다. 실제 학급 데이터에 사용하려면 영구 디스크를 지원하는 유료 서비스로 바꾸고 `ES_DB`, `ES_UPLOADS`를 영구 저장 경로로 옮기세요.

## 환경 변수

- `SECRET_KEY`: 세션 보안을 위한 비밀키 (Render 설정이 자동 생성)
- `TEACHER_CODE`: 선택 사항인 교사 인증 코드
- `NEIS_API_KEY`: 선택 사항인 나이스 API 키
- `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`: 선택 사항인 Google OAuth 설정
- `APP_URL`: 선택 사항인 공개 앱 주소
- `ES_DB`, `ES_UPLOADS`: SQLite DB와 업로드 파일 경로

실제 값이 들어 있는 `.env` 파일은 GitHub에 올리지 마세요. Render에서는 대시보드의 Environment 설정에 비밀값을 입력하세요.

## 보안 및 데이터 주의

- 이 앱의 빠른 로그인은 비밀번호를 요구하지 않습니다. 이름과 학교/학년/반 정보만으로 사용자 구분을 하기 때문에, 실제 학생의 개인정보·성적·과제·파일을 운영하는 용도로 쓰기 전에는 별도의 강한 인증과 개인정보 보호 검토가 필요합니다.
- 체험 반의 사용자·일정·자료는 시연용 예시입니다.
- 업로드한 원본의 `.env`, 데이터베이스, `uploads/`, 로그 및 `_backup/`은 개인정보와 비밀값 노출을 막기 위해 저장소에서 제외했습니다.
- 공개 배포 전에 `SECRET_KEY`와 `TEACHER_CODE`를 새 값으로 교체하세요.

## 시험

```bash
pip install -r requirements-dev.txt
python -m pytest -q tests/test_api.py
node --test tests/js/ot.test.js
```
