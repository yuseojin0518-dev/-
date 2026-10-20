# EduSpace — 우리 반 올인원 협업 공간

Flask 기반 학급 협업 앱입니다. 학사일정·급식 조회, 공유 달력, 클래스룸, 문서함, 실시간 노트, 손필기, 공부 타이머 기능을 제공합니다.

## 실행 방법

1. Python 3.11 이상을 설치합니다.
2. 의존성을 설치합니다: `pip install -r requirements.txt`
3. `.env.example`을 `.env`로 복사하고 환경 변수를 설정합니다.
4. `python app.py`로 실행합니다.

공개 배포 전에는 `SECRET_KEY`와 `TEACHER_CODE`를 반드시 새 값으로 설정하고 HTTPS를 사용하세요.

## 환경 변수

- `SECRET_KEY`: Flask 세션 서명용 비밀키
- `TEACHER_CODE`: 교사 인증 코드
- `NEIS_API_KEY`: (선택) 나이스 API 키
- `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`: (선택) Google 로그인 설정
- `APP_URL`: (선택) 공개 앱 주소

실제 비밀값이 들어 있는 `.env`, 데이터베이스, 업로드 파일, 로그, 백업 파일은 저장소에 포함하지 않습니다.
