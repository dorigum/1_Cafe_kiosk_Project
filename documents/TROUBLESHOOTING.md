# Cafe Kiosk Troubleshooting Guide

카페 키오스크 개발 및 운영 중에 발생한 주요 인프라, 데이터베이스, 비즈니스 에러 해결 사례의 인덱스입니다.

---

## 🗄️ 데이터베이스 및 예약어 충돌

### 🚨 [이슈 1] 예약어(Reservation Keyword) 충돌로 인한 테이블 생성 불가
* **현상**: SQL 스크립트 실행 또는 테이블 직접 쿼리 시 구문 오류 발생 및 `OPTION` 테이블 생성 실패.
* **원인**: `OPTION`은 DBMS(MySQL/Oracle) 내의 예약어로 테이블명으로 직접 명명이 불가능함.
* **해결**:
  1. 테이블명을 `MENU_OPTION`으로 전면 변경하여 충돌을 회피함.
  2. 관련 자바 모델 객체를 `Option.java`에서 `MenuOption.java`로 리팩토링하고 DAO의 SQL 쿼리를 수정하여 데이터 접근 안전성 확보.

### 🚨 [이슈 2] 회원 주문 시 주문자가 '비회원'으로 오조인되는 오류
* **현상**: 회원이 로그인한 상태에서 정상 결제했으나 주문 테이블 조회 시 주문자가 '비회원'으로 인덱싱됨.
* **원인**: JDBC 조인 시 컬럼을 명시적으로 매핑하지 않고 생략했거나 회원 고유번호(ID) 추출 DTO 세팅 시 예외 누락.
* **해결**: `OrderRepositoryImpl` 내의 SELECT 쿼리에 명시적인 회원 매핑(`member_id`) 컬럼 조인을 선언하고, 주문 트랜잭션 도중 세션 회원 정보를 세터로 확실히 전달하여 오류를 방지함.

---

## ⚙️ 애플리케이션 및 환경 설정

### 🚨 [이슈 3] dbInfo.properties 파일 로드 오류 (DBUtil Connection Null)
* **현상**: 서버 기동 시 데이터베이스 연결이 실패하며 `NullPointerException` 발생.
* **원인**: 로컬 빌드 경로(`bin/`)와 리소스 소스 경로(`src/`) 내 `dbInfo.properties` 파일의 대소문자 명명 불일치 및 스트림 조회 오류.
* **해결**:
  1. 파일 이름을 `dbInfo.properties`로 대소문자를 정교하게 통일함.
  2. `DBUtil`의 `getResourceAsStream` 호출 시 경로를 루트 위치(`/dbInfo.properties`)로 정합하여 리눅스/윈도우 빌드 플랫폼 환경에 모두 대응함.

### 🚨 [이슈 4] 옵션 그룹 중복 출력 및 등록 버그
* **현상**: 메뉴판 조회 또는 특정 메뉴 정보 출력 시 동일한 옵션 그룹 정보가 중복 노출되는 레이아웃 훼손 현상.
* **원인**: `OptionGroupRepositoryImpl.findAll`의 조인 쿼리에서 적절한 `GROUP BY` 또는 `DISTINCT` 제어 장치가 생략됨.
* **해결**: 레포지토리 단의 조회 쿼리에 중복 방지용 엔티티 조인 규칙 및 `GROUP BY` 구문을 추가하여 데이터 단일성을 제공함.

---
*Updated at_2026.07.23*
