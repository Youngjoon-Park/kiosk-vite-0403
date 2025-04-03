# Kiosk System - Vite 기반 키오스크 프로젝트

이 프로젝트는 **Vite + React**를 사용하여 **키오스크 시스템**을 개발한 프로젝트입니다. 시스템은 주문, 결제, 관리자 페이지 기능을 포함하고 있으며, 백엔드는 **Spring Boot**와 **MySQL**을 사용하여 구현되었습니다. **Config Server**를 통해 외부에서 설정을 관리하고 있으며, 포트 설정을 통해 클라이언트와 서버의 연결을 구성했습니다.

## 프로젝트 구조

프로젝트는 **프론트엔드**, **백엔드**, **설정 서버**로 나누어져 있으며, 각각의 주요 역할은 다음과 같습니다:

# 🖥️ Kiosk System (Vite + Spring Boot + Config Server)

키오스크 주문 시스템 풀스택 프로젝트입니다.  
- **프론트엔드**: React + Vite (포트 5173)  
- **백엔드**: Spring Boot (포트 8081, Gradle 기반)  
- **설정 서버**: Spring Cloud Config (포트 8888, GitHub 연동)

---

## 📁 디렉토리 구조 요약
/config-server - 설정 서버 (GitHub 연동) /kiosk-app - 백엔드 API 서버 (MySQL + KakaoPay) /kiosk-frontend-vite - 프론트엔드 (React + Vite)

---

## ⚙️ 설정 개요

### ✅ 설정 서버 `application.yml`

```yaml
server:
  port: 8888
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/Youngjoon-Park/config-repo0327
          default-label: main
          search-paths: .
spring.application.name=kiosk-basic
spring.config.import=optional:configserver:http://localhost:8888
server.port=8081
kakao.admin-key=관리자_키
logging.level.org.springframework=DEBUG
spring.mvc.pathmatch.matching-strategy=ant_path_matcher


vite.config.js
server: {
  port: 5173,
  proxy: {
    '/api': {
      target: 'http://localhost:8081',
      changeOrigin: true,
      rewrite: (path) => path.replace(/^\/api/, '/api'),
    },
  },
}
cd config-server
./gradlew bootRun

cd kiosk-app
./gradlew bootRun

cd kiosk-frontend-vite
npm install
npm run dev

포트 요약
구성	포트	설명
Config Server	8888	설정 파일 로드 (GitHub)
Spring Boot	   8081	API, 결제, DB 처리
Vite + React	5173	UI + API 프록시 연동




