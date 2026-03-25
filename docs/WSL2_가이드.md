# Windows 설치 빠른 시작 가이드

SmartBot KR을 Windows에서 실행하는 가장 빠른 방법입니다.

## 5분 설치 순서

**1. PowerShell(관리자)** 열기 → `wsl --install` 실행 → 컴퓨터 재시작

**2. Ubuntu** 실행 → 사용자 이름·비밀번호 설정

**3. [Docker Desktop](https://www.docker.com/products/docker-desktop/) 설치**
   - 설치 후: Settings → Resources → WSL Integration → Ubuntu 켜기 → Apply

**4. Ubuntu 터미널에서:**

```bash
git clone https://github.com/sinmb79/Gov-chat-bot.git
cd Gov-chat-bot
chmod +x install.sh && ./install.sh
```

**5. 브라우저에서 접속:**
- 관리자 화면: http://localhost:3000
- API 문서: http://localhost:8000/docs

---

자세한 내용은 [운영가이드.md](./운영가이드.md) 13장을 참고하세요.
