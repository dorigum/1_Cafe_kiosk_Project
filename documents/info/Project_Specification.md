# ☕ 카페 키오스크 프로젝트 명세서 (Cafe Kiosk Project)

## 1. 프로젝트 개요
- **목표**: MVC 패턴을 적용한 콘솔 기반 카페 키오스크 시스템 구축 (Layered Architecture)
- **주요 기능**: 회원/비회원 주문 서비스 및 관리자 모드 (상품/카테고리/회원/매출 관리)
- **개발 환경**: Java 18 (OpenJDK), **MySQL 8.0**, JDBC (mysql-connector-j-9.6.0)
---
## 2. 주요 기능 요구사항 (진행 현황)

### 👤 사용자(회원/비회원) 기능
- [x] **회원 로그인**: 휴대폰 번호/비밀번호 인증 (`MemberRepository` 연동)
- [x] **회원가입 보너스**: 신규 회원가입 시 **1,000 포인트 자동 적립** 로직 구현 (신규)
- [x] **주문 내역 조회**: JOIN 쿼리를 통한 상세 내역 확인
- [x] **포인트 내역 확인**: 본인의 포인트 적립 및 차감 히스토리(사유 포함) 조회 기능 (신규)
- [x] 상품 선택 및 장바구니 담기
- [x] 결제 처리 및 포인트 적립

### 🛠️ 관리자(Admin) 통합 관리 시스템
- [x] **카테고리 관리 (CRUD)**: 카테고리 추가, 목록 조회, 삭제
- [x] **메뉴 및 옵션 관리 (CRUD)**: 
    - **메뉴 정보 관리**: 카테고리별 상품 등록, 조회, 삭제
    - **메뉴 옵션 관리**: 옵션 그룹(온도, 사이즈 등) 및 세부 옵션(ICE, Regular 등) 관리 기능 추가
    - **카테고리별 옵션 설정**: 각 카테고리에 기본 적용될 옵션 그룹 매핑 설정 기능 추가
- [x] **회원 관리 및 보안**: 
    - 가입된 전체 회원 목록 조회 및 특정 회원 삭제
    - **포인트 수정 고도화**: 특정 회원에게 포인트 지급/차감 시 **수정 사유**를 필수 입력하도록 개선 (신규)
    - **등급(Role) 관리**: 일반 회원(USER)과 관리자(ADMIN) 등급 변경 기능 추가 (신규)
    - **1인 관리자 체제**: 시스템 안정성을 위해 관리자는 **단 1명만 존재**할 수 있도록 제한 로직 구현 (신규)
    - **관리자 보호 로직**: 관리자 계정은 포인트 수정 및 직접 삭제가 불가능하도록 안전 장치 마련 (신규)
- [x] **매출 통계 및 분석**:
    - 누적 총 매출액 집계
    - **카테고리별 매출 분석** (Coffee, Tea 등)
    - **인기 메뉴 Top 3** 선정 (판매량 기준)
    - **일별 매출 추이 시각화** (최근 7일 막대 그래프)
    - **기간별 상세 조회**: 날짜 범위 지정을 통한 매출액 및 **객단가(AVG)** 분석 (신규)
    - **시간대별 매출 분석**: 하루 중 주문 집중 시간대(피크타임) 파악 (신규)
    - **우수 회원 기여도 분석**: 누적 결제액 기준 상위 **VVIP 회원** 추출 (신규)
- [x] **주문 관리**: 전체 주문 목록 확인 및 **결제 취소(CANCELLED)** 처리
---
## 3. 시스템 아키텍처 (Layered Architecture)
- **Model**: `Menu`, `Member`, `Order`, `MenuOption`, `OptionGroup`, `PointHistory` (신규)
- **View**: `StartView` (진입점), `MenuView` (메인 루프), `EndView` (출력 전담), `FailView` (에러 전담), `OrderingView` (주문 전담)
- **Controller**: `AdminController`, `MenuController`, `MemberController`
- **Service**: `AdminService`, `MemberService`, `MenuService`
- **Repository**: `MenuRepository`, `MemberRepository`, `CategoryRepository`, `OrderRepository`, `MenuOptionRepository`, `OptionGroupRepository`
- **Configuration**: `dbInfo.properties` (파일명 대소문자 수정 및 소스 폴더 경로 최적화)
---
## 4. 데이터 설계 (MySQL 테이블 구조)
| 구분 | 테이블명 | 설명 |
| :--- | :--- | :--- |
| **Category** | CATEGORY | 상품 분류 (Coffee, Tea, Dessert 등) |
| **Menu** | MENU | 상품명, 가격, 설명, 품절 여부 |
| **MenuOption** | MENU_OPTION | 세부 메뉴 옵션 (HOT, ICE, Regular, Large 등) |
| **OptionGroup** | OPTION_GROUP | 옵션 그룹 (온도, 사이즈, 카페인유무 등) |
| **CategoryOption** | CATEGORY_OPTION_GROUP | 카테고리별 기본 적용 옵션 그룹 매핑 |
| **Mapping** | MENU_OPTION_GROUP | 메뉴별 적용 가능한 옵션 그룹 매핑 |
| **Member** | MEMBER | 회원 정보, 휴대폰 번호(Unique), 포인트, 역할(ADMIN/USER) |
| **PointHistory** | POINT_HISTORY | 포인트 변동 내역 및 사유 기록 테이블 (신규) |
| **Order** | ORDERS | 주문 총액, 사용/적립 포인트, 주문 상태, 주문 일시 |
| **OrderItem** | ORDER_ITEM | 주문 상세(수량, 단가), 메뉴/카테고리명 스냅샷 포함 |
| **OrderItemOption**| ORDER_ITEM_OPTION | 주문 시점에 선택된 세부 옵션 기록 |
| **Wishlist** | WISHLIST | 회원의 찜 목록 |

---
## 5. 변경 이력 및 개발 일지
- 전체 개발 히스토리 및 수정 로그는 표준화 규격에 따라 [PROJECT_LOG.md](../PROJECT_LOG.md) 및 [project-log/](../project-log/) 디렉터리 하위에 날짜별 파일로 독립하여 관리합니다.

## 6. 개발 및 협업 가이드 (실행 전 확인)
1.  **MySQL 설정**: `resources/DDL.sql` -> `resources/DML.sql` -> `resources/admin.sql` 순서로 실행
2.  **DB 접속 정보**: `resources/dbInfo.properties` 파일에서 본인의 MySQL 계정/비번 수정
3.  **라이브러리**: `lib/mysql-connector-j-9.6.0.jar`가 Build Path에 포함되어 있는지 확인
4.  **인코딩**: 이클립스 실행 설정(Run Configurations)에서 **Encoding을 UTF-8**로 지정 필수
---
## 7. 협업을 위한 변경사항 및 개발 규칙
- **최신 DDL 반영 및 테이블 구조 최적화**:
  - `ORDERITEM` → `ORDER_ITEM`, `OPTIONGROUP` → `OPTION_GROUP` 등 테이블명 명명 규칙 통일 (Snake Case)
  - `ORDER_ITEM` 테이블에 `menu_name_snapshot`, `category_name_snapshot` 컬럼 추가하여 데이터 정합성 강화 (메뉴명 변경 시에도 과거 주문 내역 보존)
  - `ORDERS` 테이블의 `ordered_at` → `order_date` 컬럼명 변경
- **데이터베이스 운영 규칙 (중요)**:
  - **DDL/DML 관리**: 신규 테이블(`POINT_HISTORY`, `CATEGORY_OPTION_GROUP` 등)이나 초기 옵션 데이터 추가 시 반드시 `resources/admin.sql`에 기록하여 팀원들과 공유한다.
  - **자동 테이블 생성**: `MemberRepositoryImpl`에 포함된 테이블 자동 생성 로직을 확인하고, 원격 DB 환경 변경 시 이를 먼저 실행하도록 한다.
- **설정 및 보안 규칙**:
  - **민감 정보 보호**: `dbInfo.properties` 파일은 개인별 DB 접속 정보를 담고 있으므로 절대 깃허브에 Push하지 않는다. (이미 `.gitignore`에 등록 완료)
  - **파일명 정규화**: 파일 로딩 시 대소문자를 구분하는 환경(Linux 등)을 고려하여 `dbInfo.properties`와 같이 대소문자를 정확히 일치시킨다.
- **개발 표준**:
  - **인코딩**: 한글 깨짐 방지를 위해 모든 소스 파일과 이클립스 실행 환경, 데이터베이스 연결 문자열에 **UTF-8** 인코딩을 강제 적용한다.
  - **브랜치 전략 및 소통 규칙 (필독)**:
  - **작업 브랜치**: 개인 작업은 각자의 `feature/` 브랜치에서 진행 후 PR(Pull Request)을 통해 병합한다.
  - **Develop 커밋 시점**: `develop` 브랜치에는 개별 기능 단위로 구현 및 테스트가 완벽히 완료되었을 때만 작업 내역을 커밋/푸시하는 것을 권장한다.
  - **의견 조율 필수**: `develop` 브랜치에 직접 커밋하거나 푸시해야 할 상황이 발생할 경우, **반드시** 사전에 팀원들과 충분한 의견 조율을 거친 후 실행한다.
