# Cafe Kiosk Project Log

카페 키오스크 프로젝트의 통합 기획 설계 명세서, 개발 기록(수정 로그) 및 트러블슈팅 색인 문서입니다.

---

## 📌 핵심 문서

### 1. 요구사항 및 기획 (info/)
- [요구사항 정의 및 기능 명세서](info/Project_Specification.md) (정화 버전)
- [키오스크 주문 화면 기획](info/OrderingView.md)
- [관리자 기능 설계서](info/카페%20키오스크_관리자%20기능%20관리%20명세서.md) (정화 버전)
- [관리자 기능 흐름도 (AdminFlow.md)](info/AdminFlow.md)
- [프로젝트 발표 자료](info/Presentation_Materials.md)
- [팀 공동 작업 메모](info/팀플%20작업%20메모.md)
- [프로젝트 설명서 (README.md)](../README.md)

### 2. 데이터베이스 설계 및 초기화 SQL (info/)
- [데이터베이스 스키마 정의서 (DDL.sql)](info/DDL.sql)
- [초기 데이터 적재 스크립트 (DML.sql)](info/DML.sql)
- [관리자 계정 생성 쿼리 (admin.sql)](info/admin.sql)

---

## 🛠️ 개발 기록 & 수정 로그 (project-log/)
명세서에서 추출/분리된 일자별 상세 개발 일지입니다.

- 🗓️ [2026-03-18 개발 기록](project-log/2026-03-18.md) (보안 정책 및 콘솔 텍스트 튜닝)
- 🗓️ [2026-03-17 개발 기록](project-log/2026-03-17.md) (매출 시각화 고도화, CSV 내보내기, BI 분석)
- 🗓️ [2026-03-16 개발 기록](project-log/2026-03-16.md) (옵션 템플릿 방식, 오버라이딩, 회원정보 가입일자 추가, 옵션 E2E 추적)
- 🗓️ [2026-03-15 개발 기록](project-log/2026-03-15.md) (포인트 변동 내역, Singleton Admin 제한)
- 🗓️ [2026-03-13 개발 기록](project-log/2026-03-13.md) (지능형 옵션 자동 매핑, 주문 취소 포인트 롤백 트랜잭션)
- 🗓️ [2026-03-12 개발 기록](project-log/2026-03-12.md) (MVC 패턴 고도화, UNIQUE 제약 조건 추가)
- 🗓️ [2026-03-11 개발 기록](project-log/2026-03-11.md) (dbinfo.properties 도입, JDBC 세팅 및 UTF-8 강제)

---

## 🚨 장애 색인 & 해결 이력 (Troubleshooting)
- 🛠️ [TROUBLESHOOTING.md](TROUBLESHOOTING.md) (DB 예약어 충돌, 주문자 식별 오류, dbInfo.properties 조회 오류 등)

---

## 🏗️ 배포 및 가상 환경 (guides/)
- [Docker Compose 설정 (docker-compose.yml)](guides/docker-compose.yml) (컨테이너 설정)
