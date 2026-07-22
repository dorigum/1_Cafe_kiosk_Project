# Cafe Kiosk (카페 키오스크) — Console 주문 시스템

> **JDBC 연동 및 MVC 아키텍처 기반의 카페 주문 관리 키오스크 콘솔 프로그램**

<br>

## 📌 프로젝트 소개

**Cafe Kiosk**는 콘솔 환경에서 실행되는 직관적이고 견고한 카페 주문 관리 프로그램입니다. 사용자 친화적인 CLI 인터페이스를 통해 음료/디저트 주문, 장바구니 실시간 갱신, 주문 확정 및 회원 포인트 시스템과의 연동을 안정적으로 처리합니다.

---

## 🛠️ 주요 기능 (Key Features)

### 1. 카테고리 기반 메뉴 탐색
* **다양한 카테고리**: 인기 상품, 신상품, 커피, 논커피, 디저트 등 세분화된 메뉴 구조를 제공합니다.
* **실시간 조회**: 데이터베이스에서 즉각적으로 최신 메뉴 목록을 조회하여 화면에 인덱스 방식으로 노출합니다.

### 2. 옵션 및 수량 조절
* 메뉴 선택 시 샷 추가, 당도 조절, 핫/아이스 등 세부 옵션을 설정할 수 있습니다.
* 주문 수량을 손쉽게 입력하여 장바구니에 반영합니다.

### 3. 장바구니(Cart) 실시간 관리
* 장바구니 내 항목 추가, 수량 변경, 개별 항목 삭제, 장바구니 비우기 등 실시간 관리 기능을 지원합니다.
* 주문 확정 전 최종 금액 및 선택 옵션을 투명하게 요약해 보여줍니다.

### 4. 회원 포인트 연동 및 결제
* 주문 금액 결제 시 회원 포인트를 조회하여 복합 결제를 처리하거나, 신규 결제 금액의 일정 비율을 포인트로 자동 적립합니다.

---

## ⚙️ 기술 스택 (Tech Stack)

* **Language**: Java 17
* **Database**: Oracle DB / JDBC Connection
* **Design Pattern**: MVC Pattern (Model-View-Controller)
* **Build/Dev**: CLI Console App

---

## 📐 MVC 계층 구조 (Layer Directory)

```
src/
├── controller/     # 비즈니스 흐름 제어 및 View-Service 매핑 (MenuController 등)
├── model/          # 데이터 모델 및 DTO 객체 (OrderItem, Member 등)
├── service/        # 비즈니스 논리 구현 및 핵심 서비스 계층
├── repository/     # JDBC 연결 및 데이터베이스 SQL 쿼리 처리
├── util/           # 데이터 포맷 및 공통 헬퍼 클래스
├── exception/      # 공통 예외 처리 클래스
└── view/           # 손님용 화면 및 관리자용 콘솔 출력 화면 (OrderingView.java 등)
```

---

## 📂 프로젝트 구조 (Repository Structure)

```
1_Cafe_kiosk_Project/
├── src/                    # Java 소스 코드 (MVC 구조)
├── lib/                    # Oracle JDBC 드라이버 라이브러리
├── scripts/                # 데이터 적재 및 시드 생성 스크립트 (Python)
└── documents/              # 프로젝트 명세 문서 및 기록
    ├── PROJECT_LOG.md      # 문서 통합 인덱스
    └── info/               # 키오스크 주문 화면 상세 기획안 (OrderingView.md)
```
