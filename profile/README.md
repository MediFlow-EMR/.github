# MediFlow EMR

> 간호사의 실무 경험으로 설계한 AI 기반 인수인계 자동화 EMR 시스템: 의료 업무 효율성 향상 솔루션

![Google Gemini](https://img.shields.io/badge/Google_Gemini-AI_Model-8E75B2?logo=google&logoColor=white)
[![AWS](https://img.shields.io/badge/AWS-Cloud-FF9900?logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5.6-6DB33F?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-19.1.1-61DAFB?logo=react&logoColor=black)](https://react.dev)
[![MariaDB](https://img.shields.io/badge/MariaDB-10.11-003545?logo=mariadb&logoColor=white)](https://mariadb.org)


---

## 프로젝트 소개

**MediFlow EMR**은 간호사의 실무 경험을 바탕으로 설계된 전자의무기록 시스템입니다.

### 핵심 가치

- **One-View Dashboard**: 환자 정보를 한 화면에서 통합 조회
- **AI 인수인계**: Google Gemini 기반 자동 요약으로 인수인계 시간 단축
- **실무 중심 설계**: 간호사가 직접 겪은 불편함을 기술로 해결

### 주요 지표

- **개발 기간**: 7일 (기획 1일 + 개발 4일 + 배포 2일)
- **배포**: AWS 3-Tier 아키텍처
- **목표**: 인수인계 시간 30-60분 → 5-10분 단축

---

## 배포 URL

- **프론트엔드**: [https://mediflow-emr.cloud](https://mediflow-emr.cloud)
- **백엔드 API**: [https://api.mediflow-emr.cloud](https://api.mediflow-emr.cloud)
- **API 문서**: [API 문서](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/6.API_DOCUMENTATION.md)

---
## 기능 명세

- [기능 명세서](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/3.FEATURES.md) 

## 기능 시연

### 1. 로그인 및 대시보드

**이메일 로그인**

![이메일 로그인](../assets/이메일로그인.gif)

**Google 소셜 로그인**

![Google 로그인]()

**통합 환자 뷰 (One-View Dashboard)**

![통합 환자 뷰]()

---

### 2. 환자 정보 관리

**대시보드 - 내 담당 환자 조회**

![대시보드]()

**바이탈 사인 등록 및 차트**

![바이탈 사인]()

**섭취배설량(I/O) 기록**

![섭취배설량]()

---

### 3. 간호 기록

**리치 텍스트 에디터 - 형광펜/글자색**

![간호기록 작성]()

**간호기록 조회 및 수정**

![간호기록 조회]()

---

### 4. 투약 관리
**의료 오더 조회**

![의료 오더]()

**약품 검색 (식약처 API)**

![약품 검색]()

**투약 기록 등록**

![투약 기록]()

---

### 5. AI 인수인계

**AI 인수인계 요약 생성**

![AI 인수인계]()

**인수인계 검토 및 저장**

![인수인계 저장]()

---

### 6. 검사 결과

**검사 결과 조회 및 필터링**

![검사 결과]()

---

## 핵심 기능

| 기능 | 기술 구현 | 효과 |
|-----|----------|------|
| **One-View Dashboard** | React 컴포넌트 모듈화 + 데이터 aggregation | 5+ 페이지 → 1개 화면 통합 |
| **AI 인수인계** | Gemini API 기반 의료 기록 요약 | 인수인계 시간 80% 단축 |
| **리치 텍스트 에디터** | HTML 저장 + Plain Text AI 처리 | 직관적 간호기록 작성 |
| **식약처 API 연동** | 실시간 약품 정보 조회 | 투약 안전성 향상 |

---

## 기술 스택

| 기술 (Technology) | 용도 (Usage) |
| :--- | :--- |
| ![React](https://img.shields.io/badge/React-19.1.1-61DAFB?logo=react&logoColor=black) | UI 컴포넌트 라이브러리 |
| ![Vite](https://img.shields.io/badge/Vite-7.1.2-646CFF?logo=vite&logoColor=white) | 빌드 도구 및 개발 서버 (HMR 지원) |
| ![React Router](https://img.shields.io/badge/React_Router-7.8.2-CA4245?logo=reactrouter&logoColor=white) | 클라이언트 사이드 라우팅 |
| ![Zustand](https://img.shields.io/badge/Zustand-5.0.8-443E38?logo=react&logoColor=white) | 경량 상태 관리 |
| ![Axios](https://img.shields.io/badge/Axios-1.13.2-5A29E4?logo=axios&logoColor=white) | HTTP 클라이언트 (API 통신) |
| ![Recharts](https://img.shields.io/badge/Recharts-3.5.0-22B5BF?style=flat) | 바이탈 사인 시계열 차트 |
| ![React Markdown](https://img.shields.io/badge/React_Markdown-10.1.0-000000?logo=markdown&logoColor=white) | 인수인계 마크다운 렌더링 |
| ![Highlight.js](https://img.shields.io/badge/Highlight.js-11.11.1-282C34?logo=javascript&logoColor=white) | 코드 하이라이팅 |


### Backend

| 기술 (Technology) | 용도 (Usage) |
| :--- | :--- |
| ![Java](https://img.shields.io/badge/Java-21-007396?logo=openjdk&logoColor=white) | 프로그래밍 언어 |
| ![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5.6-6DB33F?logo=springboot&logoColor=white) | 백엔드 프레임워크 |
| ![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?logo=springsecurity&logoColor=white) | 인증/인가 (JWT + OAuth2) |
| ![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-ORM-6DB33F?logo=spring&logoColor=white) | ORM (객체-관계 매핑) |
| ![QueryDSL](https://img.shields.io/badge/QueryDSL-5.0.0-0078D4) | 타입 안전 동적 쿼리 |
| ![JWT](https://img.shields.io/badge/JWT-0.12.3-000000?logo=jsonwebtokens&logoColor=white) | 토큰 기반 인증 |
| ![Spring Mail](https://img.shields.io/badge/Spring_Mail-SMTP-6DB33F?logo=gmail&logoColor=white) | 이메일 인증 발송 |
| ![Lombok](https://img.shields.io/badge/Lombok-Boilerplate-BC4521?logo=lombok&logoColor=white) | 보일러플레이트 코드 자동 생성 |

### Database

| 기술 (Technology) | 용도 (Usage) |
| :--- | :--- |
| ![MariaDB](https://img.shields.io/badge/MariaDB-Production-003545?logo=mariadb&logoColor=white) | 운영 데이터베이스 |
| ![H2 Database](https://img.shields.io/badge/H2_Database-In_Memory-003545?logo=h2&logoColor=white) | 개발/테스트용 인메모리 DB |

### External APIs

| 기술 (Technology) | 용도 (Usage) |
| :--- | :--- |
| ![Google Gemini](https://img.shields.io/badge/Google_Gemini-AI_Model-8E75B2?logo=google&logoColor=white) | AI 인수인계 요약 생성 |
| ![KFDA API](https://img.shields.io/badge/공공데이터포털-식약처_API-113366?logo=data) | 약품 정보 실시간 검색 |
| ![Google OAuth2](https://img.shields.io/badge/Google_OAuth2-Login-4285F4?logo=google&logoColor=white) | 소셜 로그인 (구글) |
| ![Kakao OAuth2](https://img.shields.io/badge/Kakao_OAuth2-Login-FFCD00?logo=kakao&logoColor=black) | 소셜 로그인 (카카오) |

### Infrastructure

| 기술 (Technology) | 용도 (Usage) |
| :--- | :--- |
| ![AWS EC2](https://img.shields.io/badge/AWS_EC2-t3.small-FF9900?logo=amazonec2&logoColor=white) | 백엔드 서버 호스팅 |
| ![AWS RDS](https://img.shields.io/badge/AWS_RDS-MariaDB-527FFF?logo=amazonrds&logoColor=white) | MariaDB 관리형 데이터베이스 |
| ![AWS S3](https://img.shields.io/badge/AWS_S3-Storage-569A31?logo=amazons3&logoColor=white) | 정적 파일 저장 (프로필 이미지 등) |
| ![AWS CloudFront](https://img.shields.io/badge/AWS_CloudFront-CDN-D05C42?logo=amazoncloudfront&logoColor=white) | 프론트엔드 CDN |
| ![AWS Route 53](https://img.shields.io/badge/AWS_Route_53-DNS-8C4FFF?logo=amazonroute53&logoColor=white) | 도메인 관리 |
| ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?logo=githubactions&logoColor=white) | CI/CD 파이프라인 |


---

## 시스템 아키텍처

### 메인 시스템 아키텍처 (Runtime)
```
사용자가 서비스를 이용할 때의 흐름
```
<img width="2770" height="1642" alt="image" src="https://github.com/user-attachments/assets/4ee8e29d-36bc-40a6-9616-79c92359417c" />

### 네크워크 및 보안체계
#### 보안 그룹 관계도
<img width="2475" height="696" alt="image" src="https://github.com/user-attachments/assets/674ec8ba-3727-446f-92b2-813d553fe83d" />

#### 보안 그룹 규칙 상세

| 보안 그룹 | 인바운드 규칙 | 소스 | 목적 |
|---------|------------|------|------|
| **mediflow-alb-sg** | HTTPS (443) | 0.0.0.0/0 | 전세계 사용자 접근 |
| **mediflow-alb-sg** | HTTP (80) | 0.0.0.0/0 | HTTPS 리다이렉션용 |
| **mediflow-backend-sg** | HTTP (9005) | mediflow-alb-sg | ALB → EC2 전달 |
| **mediflow-backend-sg** | SSH (22) | 내 IP | 관리자 접속 |
| **mediflow-rds-sg** | MySQL (3306) | mediflow-backend-sg | EC2 → RDS 연결 |
| **mediflow-rds-sg** | MySQL (3306) | 내 IP | 로컬 개발/관리 |

---

## 상세 문서

### 개발 가이드
- [개발자 가이드](https://github.com/MediFlow-EMR/mediflow-dev/blob/main/README.md) - 로컬 환경 설정
- [API 문서](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/6.API_DOCUMENTATION.md) - REST API 명세

### 시스템 설계
- [프로젝트 개요](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/1.PROJECT_OVERVIEW.md)
- [아키텍처 설계](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/4.ARCHITECTURE.md)
- [데이터베이스 설계](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/5.DATABASE_DESIGN.md)

### 법적 고려사항
- [법적 컴플라이언스](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/8.LEGAL_COMPLIANCE.md) - 의료법/개인정보보호법

---

## 향후 계획

- [향후 업데이트 계획](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/7.ROADMAP.md) 
