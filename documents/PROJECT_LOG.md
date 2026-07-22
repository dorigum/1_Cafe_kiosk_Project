# Cafe Kiosk Project Log

카페 키오스크 프로젝트의 기획 사양 및 보조 개발 도구의 인덱스입니다.

## 📌 핵심 문서

- [키오스크 주문 화면 기획](info/OrderingView.md)
- [프로젝트 설명서 (README.md)](../README.md)

## 🛠️ 개발 보조 및 테스트 유틸리티 (src/)

데이터베이스 검증 및 목 데이터 생성을 위해 사용되는 일회성 자바/파이썬 도구입니다.

- **데이터 검증**: [CheckData.java](../src/CheckData.java) (DB 적재 데이터 점검)
- **테이블 조회**: [ListTables.java](../src/ListTables.java) (생성된 DB 테이블 목록 인쇄)
- **쿼리 테스트**: [TestQuery.java](../src/TestQuery.java) (JDBC 연동 SQL 쿼리 검증)
- **목 데이터 생성**: [generate_trend_order_seed.py](../scripts/generate_trend_order_seed.py) (주문 트렌드 생성 스크립트)

## ✍🏻 작성 기준

1. 기획안 및 아키텍처 관련 마크다운은 `documents/info/`에 아카이빙합니다.
2. 일회성 자바 테스트 유틸리티 코드는 `src/` 패키지 루트에 보존합니다.
