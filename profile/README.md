# MediFlow EMR

> 간호사의 실무 경험으로 설계한 AI 기반 인수인계 EMR 연계 모듈

## 현재 구현 상태 (2026-10-11)

- 랜딩·로그인·메인·상세 화면은 라이트 기본값의 저장형 다크모드와 모바일 배치를 제공합니다. 공통 포커스·움직임과 reduced-motion을 적용했습니다.
- 환자 검색·병실·안전정보, 간호기록 내용·기간·카테고리·작성자·중요 여부, 인수인계 내용/작성자·기간·근무조·수기/AI·상태를 필터링합니다. 다중 선택은 같은 항목 안에서 OR, 항목 사이에서 AND이며 조회된 목록에 적용합니다.
- 간호기록·인수인계·오더·투약·V/S·섭취배설·검사결과는 최신순/오래된순을 선택합니다. 환자 목록은 KTAS 우선순위를 유지합니다.
- 상단 날짜·근무조로 과거 담당 환자와 부서 요약, 새 인수인계의 대상 근무조를 전환합니다. 환자 기본정보·최근 V/S는 현재 값이며 임상 탭의 기간 필터는 별도입니다.
- 수기·AI 초안을 서버에 임시저장하고 다시 열어 수정·승인합니다. 승인 후 작성자 수정, 원본 AI·수정본·버전별 스냅샷 보존을 지원합니다. 초안은 작성자 전용, 승인본·이력은 같은 부서 조회입니다.
- 운영은 Flyway → Hibernate validate → 헬스 체크 순서입니다. 기존 DB의 최초 기준선·백업·실패 대응은 [DB 전환 안내](https://github.com/MediFlow-EMR/mediflow-dev/blob/main/deploy/database/README.md)를 따릅니다. 로컬 MariaDB 보존은 `local` 프로필, 격리된 자동 테스트는 H2입니다.
- 최신 API는 [swagger.yaml](https://github.com/MediFlow-EMR/mediflow-dev/blob/main/swagger.yaml) 1.3.2, DB는 18개 JPA 엔티티입니다. 소개 GIF는 2026.10.11 운영 화면 기준입니다.

모든 환자 데이터는 가상인 포트폴리오 PoC입니다. 실제 병원 EMR/OCS 연계·전자서명·의료기관 인증은 향후 검증 범위이며, 임상 효과나 시간 절감률을 실제 의료기관에서 측정하지 않았습니다.

![Google Gemini](https://img.shields.io/badge/Google_Gemini-AI_Model-8E75B2?logo=google&logoColor=white)
[![AWS](https://img.shields.io/badge/AWS-Cloud-FF9900?logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5.6-6DB33F?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-19.2.3-61DAFB?logo=react&logoColor=black)](https://react.dev)
[![MariaDB](https://img.shields.io/badge/MariaDB-10.11-003545?logo=mariadb&logoColor=white)](https://mariadb.org)


---

## 프로젝트 소개

**MediFlow EMR**은 간호사의 실무 경험을 바탕으로 설계된 전자의무기록 시스템입니다.

### 핵심 가치

- **One-View Dashboard**: 환자 정보를 한 화면에서 통합 조회
- **AI 인수인계**: Google Gemini 기반 자동 요약으로 인수인계 시간 단축
- **실무 중심 설계**: 간호사가 직접 겪은 불편함을 기술로 해결

### 주요 지표

- **초기 개발 기록**: 7일 (기획 1일 + 개발 4일 + 배포 2일). 이후 기능·안정성 개선은 2026.10.11까지 반영했습니다.
- **배포**: S3/CloudFront 프론트엔드, EC2/Nginx 백엔드, RDS MariaDB
- **목표**: 인수인계 준비 과정의 시간·누락 감소. 초기 목표 수치(30–60분 → 5–10분)는 실제 성과 측정값이 아닙니다.

---

## 배포 URL

- **프론트엔드**: [https://www.mediflow-emr.cloud](https://www.mediflow-emr.cloud)
- **백엔드 API**: [https://api.mediflow-emr.cloud](https://api.mediflow-emr.cloud)
- **API 문서**: [API 문서](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/6.API_DOCUMENTATION.md)

---
## 기능 명세

- [기능 명세서](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/3.FEATURES.md)

## 기능 시연

2026.10.11 배포 사이트의 가상 계정으로 촬영한 최신 PC 화면입니다. GIF별 동작 범위와 파일 검증값은 [캡처 정보](../assets/demos/manifest.json), 저장·권한·동시 수정 검증 결과는 [품질 검증 기록](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/10.QUALITY_AND_VALIDATION.md)에 정리했습니다.

### 1. 로그인

- **이메일 로그인**

![이메일 로그인과 데모 체험](https://raw.githubusercontent.com/MediFlow-EMR/mediflow-dev/644421f36b15e6dc6bb47614c52f20612ee7e661/frontend/public/assets/login.gif)

- **Google, Kakao 소셜 로그인**

Google/Kakao OAuth2 구현을 유지합니다. 이번 최신 GIF는 이메일 데모 계정으로 촬영했으며 소셜 로그인 성공을 새로 촬영한 영상은 포함하지 않습니다.

---

### 2. 환자 정보 관리

- **대시보드 - 내 담당 환자 조회**
- **상단 날짜·근무조로 과거 담당 환자 전환, 병실 등 다중 필터**
- **바이탈 사인 등록 및 차트**
- **섭취배설량(I/O) 기록**

![PC 가로형 대시보드·날짜·근무조·병실 다중 필터](https://raw.githubusercontent.com/MediFlow-EMR/mediflow-dev/644421f36b15e6dc6bb47614c52f20612ee7e661/frontend/public/assets/patientdashboard.gif)

---

### 3. 간호 기록

- **간호기록 작성(리치 텍스트 에디터 - 형광펜/글자색)**
- **간호기록 조회 및 수정**
- **기간·카테고리·작성자 다중 필터 및 날짜 정렬**

![간호기록 카테고리·작성자 다중 필터와 기간 달력](https://raw.githubusercontent.com/MediFlow-EMR/mediflow-dev/644421f36b15e6dc6bb47614c52f20612ee7e661/frontend/public/assets/nursingrecord.gif)

---

### 4. 투약 관리

- **의료 오더 조회**
- **약품 검색 (식약처 API)**
- **투약 기록 등록 및 조회**
- **오더·투약 날짜 정렬 및 약품 상세 조회**

![오더 날짜 정렬과 약품 정보 조회](https://raw.githubusercontent.com/MediFlow-EMR/mediflow-dev/644421f36b15e6dc6bb47614c52f20612ee7e661/frontend/public/assets/ordertab.gif)

---

### 5. AI 인수인계

최신 PC 영상은 수기 초안 임시저장·재조회·승인·작성자 수정·버전 이력과 실제 Gemini 초안 생성·편집·원본 비교·임시저장을 보여줍니다.

- **AI 인수인계 요약 생성**
- **인수인계 검토 및 저장**
- **수기·AI 초안 임시저장·재조회·승인, 승인 후 작성자 수정 및 버전 이력**
- **근무조·작성 방식·상태 다중 필터와 최신순/오래된순 정렬**

![수기 초안 저장·승인·수정 이력과 실제 AI 초안 편집](https://raw.githubusercontent.com/MediFlow-EMR/mediflow-dev/644421f36b15e6dc6bb47614c52f20612ee7e661/frontend/public/assets/aihandover.gif)
---

## 핵심 기능

| 기능 | 기술 구현 | 효과 |
|-----|----------|------|
| **One-View Dashboard** | React 컴포넌트 모듈화 + 데이터 aggregation | 5+ 페이지 → 1개 화면 통합 |
| **AI 인수인계** | Gemini API 기반 의료 기록 요약 | 초안 생성·검토 지원 (시간 절감률 미측정) |
| **리치 텍스트 에디터** | HTML 저장 + Plain Text AI 처리 | 직관적 간호기록 작성 |
| **식약처 API 연동** | 실시간 약품 정보 조회 | 투약 안전성 향상 |

---

## 기술 스택

### Frontend
| 기술 (Technology) | 용도 (Usage) |
| :--- | :--- |
| ![React](https://img.shields.io/badge/React-19.2.3-61DAFB?logo=react&logoColor=black) | UI 컴포넌트 라이브러리 |
| ![Vite](https://img.shields.io/badge/Vite-7.3.7-646CFF?logo=vite&logoColor=white) | 빌드 도구 및 개발 서버 (HMR 지원) |
| ![React Router](https://img.shields.io/badge/React_Router-7.18.4-CA4245?logo=reactrouter&logoColor=white) | 클라이언트 사이드 라우팅 |
| ![Zustand](https://img.shields.io/badge/Zustand-5.0.8-443E38?logo=react&logoColor=white) | 경량 상태 관리 |
| ![Axios](https://img.shields.io/badge/Axios-1.20.0-5A29E4?logo=axios&logoColor=white) | HTTP 클라이언트 (API 통신) |
| ![Recharts](https://img.shields.io/badge/Recharts-3.5.0-22B5BF?style=flat) | 바이탈 사인 시계열 차트 |


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
| ![H2 Database](https://img.shields.io/badge/H2_Database-In_Memory-003545?logo=h2&logoColor=white) | 격리된 자동 테스트용 인메모리 DB (로컬은 MariaDB) |

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
| ![AWS EC2](https://img.shields.io/badge/AWS_EC2-Backend-FF9900?logo=amazonec2&logoColor=white) | 백엔드 서버 호스팅 |
| ![AWS RDS](https://img.shields.io/badge/AWS_RDS-MariaDB-527FFF?logo=amazonrds&logoColor=white) | MariaDB 관리형 데이터베이스 |
| ![AWS S3](https://img.shields.io/badge/AWS_S3-Storage-569A31?logo=amazons3&logoColor=white) | 프론트엔드 정적 파일·비공개 배포 아티팩트·약품 캐시 저장 |
| ![AWS CloudFront](https://img.shields.io/badge/AWS_CloudFront-CDN-D05C42?logo=amazoncloudfront&logoColor=white) | 프론트엔드 CDN |
| ![AWS Route 53](https://img.shields.io/badge/AWS_Route_53-DNS-8C4FFF?logo=amazonroute53&logoColor=white) | 도메인 관리 |
| ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?logo=githubactions&logoColor=white) | CI/CD 파이프라인 |


---

## 시스템 아키텍처

### 메인 시스템 아키텍처 (Runtime)

기존 그림은 ALB를 포함한 초기 설계도입니다. 현재 배포는 CloudFront/S3 → 브라우저 → API 도메인 → EC2 Nginx/Spring Boot → RDS이며, OIDC·S3·SSM으로 배포합니다. [현재 아키텍처](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/4.ARCHITECTURE.md)를 함께 확인하세요.
```
사용자가 서비스를 이용할 때의 흐름
```
<img width="2770" height="1642" alt="image" src="https://github.com/user-attachments/assets/4ee8e29d-36bc-40a6-9616-79c92359417c" />

### 네크워크 및 보안체계
#### 보안 그룹 관계도

아래 그림은 초기 ALB 설계 관계도입니다. 현재 배포 가이드의 규칙은 아래 표와 같습니다.
<img width="2475" height="696" alt="image" src="https://github.com/user-attachments/assets/674ec8ba-3727-446f-92b2-813d553fe83d" />

#### 보안 그룹 규칙 상세

| 보안 그룹 | 인바운드 규칙 | 소스 | 목적 |
|---------|------------|------|------|
| **mediflow-ec2-sg** | HTTPS (443), HTTP (80) | 0.0.0.0/0 | Nginx HTTPS 및 리다이렉션 |
| **mediflow-ec2-sg** | 9005 외부 비공개 | EC2 내부 | Nginx → Spring Boot |
| **mediflow-rds-sg** | MariaDB (3306) | mediflow-ec2-sg | EC2 → RDS 연결 |

관리 접속·배포는 Systems Manager를 사용하며 SSH·RDS의 외부 공개는 필요하지 않습니다. 실제 AWS 규칙 확인은 [배포 가이드](https://github.com/MediFlow-EMR/mediflow-dev/blob/main/deploy/aws/README.md)를 따릅니다.

---

## 상세 문서

### 개발 가이드
- [개발자 가이드](https://github.com/MediFlow-EMR/mediflow-dev/blob/main/README.md) - 로컬 환경 설정
- [API 문서](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/6.API_DOCUMENTATION.md) - REST API 명세 ([Swagger 1.3.2](https://github.com/MediFlow-EMR/mediflow-dev/blob/main/swagger.yaml))
- [검증 결과](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/10.QUALITY_AND_VALIDATION.md) - 실제 검증 범위와 남은 한계

### 시스템 설계
- [프로젝트 개요](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/1.PROJECT_OVERVIEW.md)
- [아키텍처 설계](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/4.ARCHITECTURE.md)
- [데이터베이스 설계](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/5.DATABASE_DESIGN.md)

### 법적 고려사항
- [법적 컴플라이언스](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/8.LEGAL_COMPLIANCE.md) - 의료법/개인정보보호법

---

## 향후 계획

- [향후 업데이트 계획](https://github.com/MediFlow-EMR/MediFlow-docs/blob/main/7.ROADMAP.md)
