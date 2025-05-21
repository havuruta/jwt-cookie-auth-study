# JWT + 쿠키 기반 인증 시스템 스터디 (Spring Boot + Vue 3)

Vue 프론트엔드와 Spring Boot 백엔드를 활용하여 `AccessToken`, `RefreshToken`, `HttpOnly 쿠키`, `보호된 API`, `토큰 갱신`, `자동 로그아웃`, `보안 설정` 등을 실습하는 모노레포 프로젝트입니다.

---

## 프로젝트 구조

```

study-jwt-cookie-auth/
├── backend/     # Spring Boot - JWT 인증 백엔드
└── frontend/    # Vue 3 - 인증 테스트용 프론트엔드

````

---

## 인증 시스템 특징

- `JWT Access Token + Refresh Token` 기반 인증
- `httpOnly`, `Secure`, `SameSite=None` 쿠키 사용
- `Redis` 기반 Refresh Token 저장 및 블랙리스트 관리
- XSS/CSRF 방지 보안 설정
- 자동 토큰 갱신 및 로그아웃 처리

---

## 기능 요약

| 구분 | 기능 |
|------|------|
| 로그인 / 회원가입 | 백엔드에서 토큰 발급, 프론트에서 쿠키 저장 |
| 토큰 관리 | 쿠키 기반 저장, 토큰 만료시 자동 갱신 |
| 보호 라우트 | 인증 없을 시 접근 차단 |
| Redis | 토큰 관리 및 블랙리스트 저장 |
| 테스트 페이지 | 인증 상태, API 요청, 갱신 테스트 UI 제공 (`/test`) |

---

## 기술 스택

### Frontend (Vue 3)
- Vue 3, TypeScript
- Vue Router 4, Pinia
- Axios + 인터셉터
- Vite

### Backend (Spring Boot)
- Spring Boot 3.4, Spring Security 6
- JWT
- Redis, MySQL
- Gradle / Java 17
- Docker

---

## 인증 테스트 UI
![image](https://github.com/user-attachments/assets/fe0004de-6914-45bf-8cfd-4354a344ad06)


> 인증 상태, 토큰 보유 여부, 갱신 요청 결과 등을 시각적으로 테스트할 수 있습니다.

---

## 시작하기

### 1. 백엔드 실행

```bash
cd backend
./gradlew bootRun
````

* 기본 포트: `8080`
* H2 또는 MySQL 사용 가능 (`application.yml` 확인)

### 2. 프론트엔드 실행

```bash
cd frontend
npm install
npm run dev
```

* 기본 포트: `5173`
* `.env` 설정 확인: `VITE_API_BASE_URL=http://localhost:8080`

---

## 🧾 API 요약

| 엔드포인트                | 설명             |
| -------------------- | -------------- |
| POST `/auth/signup`  | 회원가입           |
| POST `/auth/login`   | 로그인 (쿠키 포함 응답) |
| POST `/auth/reissue` | 토큰 재발급         |
| POST `/auth/logout`  | 로그아웃           |
| GET `/users/info`    | 보호된 사용자 정보 조회  |

---

## 보안 설정 요약

* 모든 요청은 HTTPS 기반
* `AccessToken`은 필요 시만 사용, 주요 인증은 `httpOnly` 쿠키로 처리
* SameSite=None + Secure + httpOnly 조합
* Redis를 통한 `RefreshToken` 저장 및 폐기 처리

---

## 스터디 목적

* 실무 수준 인증 시스템 이해
* JWT 기반 토큰 처리 흐름 마스터
* 쿠키 기반 보안 처리 방식 학습
* 프론트-백 간 인증 통신 협업 구조 실습
