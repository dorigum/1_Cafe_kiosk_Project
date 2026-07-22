# Cafe Kiosk Project Log

카페 키오스크 프로젝트의 통합 기획 설계 명세서 및 개발 유틸리티의 색인 문서입니다.

## 📌 핵심 문서

### 1. 요구사항 및 기획 (info/)
- [요구사항 정의 및 기능 명세서](info/Project_Specification.md)
- [키오스크 주문 화면 기획](info/OrderingView.md)
- [관리자 기능 설계서](info/카페%20키오스크_관리자%20기능%20관리%20명세서.md)
- [관리자 기능 흐름도 (AdminFlow.md)](info/AdminFlow.md)
- [프로젝트 발표 자료](info/Presentation_Materials.md)
- [팀 공동 작업 메모](info/팀플%20작업%20메모.md)
- [프로젝트 설명서 (README.md)](../README.md)

### 2. 데이터베이스 설계 및 초기화 SQL (info/)
- [데이터베이스 스키마 정의서 (DDL.sql)](info/DDL.sql)
- [초기 데이터 적재 스크립트 (DML.sql)](info/DML.sql)
- [관리자 계정 생성 쿼리 (admin.sql)](info/admin.sql)

### 3. 개발 보조 및 테스트 유틸리티 (src/ & guides/)
- **데이터 검증**: [CheckData.java](../src/CheckData.java) (DB 데이터 점검)
- **테이블 조회**: [ListTables.java](../src/ListTables.java) (생성 테이블 확인)
- **쿼리 테스트**: [TestQuery.java](../src/TestQuery.java) (JDBC 쿼리 검증)
- **목 데이터 생성**: [generate_trend_order_seed.py](../scripts/generate_trend_order_seed.py) (주문 목데이터)
- **가상 Docker 실행**: [Docker Compose 설정](guides/docker-compose.yml) (컨테이너 설정)

## ✍🏻 작성 기준

1. 기획/설계안 및 SQL 스크립트는 모두 `documents/info/`에 아카이빙합니다.
2. 배포 설정 및 가이드는 `documents/guides/`에서 통합 관리합니다.
