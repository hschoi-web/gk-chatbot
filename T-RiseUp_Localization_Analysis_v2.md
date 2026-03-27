# T-RiseUp 다국어 번역 분석 및 용어 표준화 보고서 v2

> **분석 대상:** translations_20260327_104608.csv (2,406행 · 68개 카테고리 · 4개 언어)  
> **분석일:** 2026.03.27  
> **지원 언어:** 한국어(KR) · 영어(EN) · 일본어(JP) · 태국어(TH)  
> **참조:** PRD_01_상세기획안.md · TRiseUp_API_제품_요구사항_정의서_PRD  
> **비고:** 키(key) 값은 수정 불가 제약 조건 적용

---

## 1. 현황 요약

### 1.1 이전 분석 대비 수정 반영 현황

이전 파일(03/26) 대비 30건의 필드 변경과 14건의 신규 키 추가가 확인되었다.

**수정 완료 항목:**

| 수정 유형 | 건수 | 대표 사례 |
|---------|------|---------|
| 오탈자 수정 | 3건 | Parnter→Partner, DIstance→Distance, Sevice→Service |
| 대소문자 통일 | 1건 | NO SHOW→NO-SHOW (status) |
| 용어 통일 | 1건 | No Show→No-Show (LI 카테고리) |
| 띄어쓰기 정비 | 4건 | 컨시어지요금→컨시어지 요금, 서비스레벨→서비스 레벨 등 |
| 미번역 보완 | 3건 | settlement/alert_clear, invoice_components, sender의 en↔kr 교정 |
| 빈 필드 채움 | 4건 | 기사1명/기사N명 en·jp·th 추가, CO/로딩실패 th 추가 |
| 신규 키 추가 | 14건 | settlement 인보이스 관련 (bulk_clear, invoice_ATTN 등) |

### 1.2 잔여 이슈 요약

| 이슈 유형 | 건수 | 비고 |
|---------|------|------|
| EN 컬럼 한국어 잔존 (미번역) | 21건 | NOTI·SS 카테고리 집중 |
| 4개 언어 모두 빈 값 | 8건 | 개발 중 미완성 항목 추정 |
| 동일 KR→상이 EN | 33건 (핵심 용어) | 맥락별 의도적 분기 vs 비일관 혼재 |
| 동일 EN→상이 KR | 14건 (핵심 용어) | 동일 |
| 영국식 철자 잔존 | 5건 | cancelled (UK) vs canceled (US) |
| JP 표기 불일치 | 2건 | Chauffeur·Concierge 영문 그대로 사용하는 경우 혼재 |

---

## 2. 미번역 항목 (EN 컬럼 한국어 잔존)

21건의 EN 컬럼에 한국어가 그대로 남아 있다. 대부분 알리고(Aligo) 연동 및 알림톡 관련 항목으로, 한국 전용 기능이라 영문 번역을 생략한 것으로 추정된다.

**한국 전용 기능 (번역 생략 의도 추정) — 14건:**

| 카테고리 | 키 | 현재 EN 값 | 번역 필요 여부 |
|--------|-----|---------|-----------|
| NOTI | 발신번호 | "발신번호" | 해외 사용 시 필요 |
| NOTI | 비용 | "비용" | 해외 사용 시 필요 |
| NOTI | 상태 | "상태" | 해외 사용 시 필요 |
| NOTI | 성공실패 | "성공/실패" | 해외 사용 시 필요 |
| NOTI | 전송건수 | "전송건수" | 해외 사용 시 필요 |
| NOTI | 전송내역 | "알림톡 전송내역" | 해외 사용 시 필요 |
| NOTI | 전송내용 | "전송내용" | 해외 사용 시 필요 |
| NOTI | 전송일 | "전송일" | 해외 사용 시 필요 |
| NOTI | 취소 | "예약취소" | 해외 사용 시 필요 |
| SS | 알리고기본발신번호 | "기본 발신번호" | 알리고 전용 |
| SS | 알리고기본발신번호안내 | "알리고 기본 발신번호와 동일하게..." | 알리고 전용 |
| SS | 알리고기본발신번호필수체크 | "기본 발신번호를 등록해 주세요." | 알리고 전용 |
| SS | 알리고기본채널 | "기본채널" | 알리고 전용 |
| SS | 알리고기본채널필수체크 | "기본채널을 등록해 주세요." | 알리고 전용 |

> ⚠ 알리고(Aligo) 관련 SS 카테고리 항목은 한국 전용 SMS/알림톡 서비스이므로 영문 번역 생략이 합리적일 수 있다. 다만 해외 OPS가 한국 시스템을 영문으로 사용하는 경우를 대비하여 최소한의 번역을 권장한다.

**범용 기능인데 미번역 — 7건 (번역 권장):**

| 카테고리 | 키 | 현재 EN 값 | 권장 EN | 권장 JP | 권장 TH |
|--------|-----|---------|--------|--------|--------|
| NB | 알림톡전송 | "알림톡 전송" | Send Notification | 通知送信 | ส่งการแจ้งเตือน |
| PT | 한국어 | "한국어" | Korean | 韓国語 | ภาษาเกาหลี |
| settlement | recipient_account_mail | "고객사 이메일" | Client E-mail | 顧客メール | อีเมลลูกค้า |
| SS | 알리고추가발신번호 | "추가 발신번호" | Additional Sender ID | 追加発信番号 | หมายเลขผู้ส่งเพิ่มเติม |
| SS | 알리고추가발신번호안내 | "알리고 발신번호와 동일하게..." | Enter the same as the Aligo Sender ID. | アリゴの発信番号と同じく入力 | กรอกเหมือนหมายเลขผู้ส่ง Aligo |
| SS | 알리고추가채널 | "추가채널" | Additional Channel | 追加チャンネル | ช่องทางเพิ่มเติม |
| sms | 템플릿만들기안내1 | (한·영 혼합 텍스트) | — (부분 한국어 제거 필요) | — | — |

---

## 3. 빈 번역 필드 (4개 언어 모두 누락)

8건의 키가 모든 언어에서 빈 값이다. 개발 중 또는 폐기 예정 항목으로 추정된다.

| 카테고리 | 키 | 추정 용도 |
|--------|-----|---------|
| BTN | 뒤로 | 뒤로가기 버튼 (Back) |
| confirm | 컨시어지취소2 | 컨시어지 취소 확인 메시지 |
| LI | 헤더 | 리스트 헤더 |
| PC | 요금2최대인원 | 요금 2단계 최대 인원 |
| PC | 요금3인당요금 | 요금 3단계 인당 요금 |
| PC | 요금3최대인원 | 요금 3단계 최대 인원 |
| PC | 요금4고정요금 | 요금 4단계 고정 요금 |
| ZO | 뒤로 | 존 설정 뒤로가기 |

---

## 4. 핵심 용어 다중 번역 현황

키 값 수정이 불가하므로, 동일 한국어가 맥락에 따라 다른 영어로 번역되는 현상을 **의도적 분기**와 **비일관 혼재**로 구분한다.

### 4.1 의도적 분기 (맥락별 다른 번역이 합리적)

아래 항목은 카테고리나 UI 위치에 따라 다른 영어 표현을 사용하는 것이 적절하다.

| 한국어 | EN 변형 | 분기 기준 |
|-------|--------|---------|
| 예약 취소 | "Cancel Booking" / "Canceled" / "Canceled Booking" | 액션 동사 vs 상태 라벨 vs 대시보드 |
| 배차완료 | "Assigned" / "Driver Assigned" | 간결 라벨 vs 상세 라벨 |
| 배차필요 | "Unassigned" / "Driver Unassigned" / "Dispatch required" | 간결 라벨 vs 상세 라벨 vs 알림 메시지 |
| 결제금액 | "Payment" / "Paid Amount" / "Amount to Charge" | 라벨 vs 이미 지불 vs 결제 예정 |
| 정산 | "Invoice" / "Settlement" | 인보이스 발행 맥락 vs 정산 처리 맥락 |
| 파트너 | "Partner" / "Partners" | 단수 vs 복수 |
| 협력사 | "Affiliate" / "Affiliates" / "AFFILIATE" | 단수 vs 복수 vs 시스템값 |

### 4.2 비일관 혼재 (통일 권장)

아래 항목은 동일 맥락에서 표현이 달라 통일이 필요하다.

| 한국어 | 현재 EN 변형들 | 권장 통일 | 비고 |
|-------|-----------|---------|------|
| 기본요금 | "Base Rate" / "Basic Rate" | **Base Rate** | PRD·요금 카테고리 기준 |
| 추가요금 | "Surcharge" / "Additional Charge" / "Additionals" | **Surcharge** | PRD 기준 |
| 봉사료 | "Service charge" / "Service Charge" | **Service Charge** | Title Case 통일 |
| 예약접수 | "Save" / "Waiting" | 맥락별 유지 | Save=버튼, Waiting=상태 |
| 정산완료 | "Settle" / "Settled" | **Settled** (상태), **Settle** (동작) | 일관 분리 |
| 인보이스 번호 | "Invoice No." / "INVOICE NO." | 맥락별 유지 | 일반 UI vs 인보이스 PDF 헤더 |
| 신규예약 | "New" / "New Booking" | **New Booking** | "New"만으로는 모호 |
| 예약공유 | "Copy link" / "Copy Link" | **Copy Link** | Title Case |
| 예약복사 | "Copy Booking" / "Booking Copy" | **Copy Booking** | 동사+목적어 형식 |
| 종료존(B) | "Finish Zone(B)" / "Finish Zone (B)" | **Finish Zone (B)** | 괄호 앞 공백 통일 |

### 4.3 역방향 불일치 (동일 EN → 상이 KR)

하나의 영어 용어가 여러 한국어로 번역되어, 같은 화면에 다른 한국어가 노출될 수 있다.

| English | 한국어 변형들 | 권장 통일 |
|---------|---------|---------|
| Completed | 운행 완료 · 종료 · 완료 · 예약완료 · 서비스완료 · 완료목록 | 맥락별 유지 (상태 vs 라벨 vs 필터) |
| Canceled | 취소 · 예약 취소 · 예약취소 · 취소목록 | 맥락별 유지 |
| Dispatch | 배차 · 배차하기 · 운행 현황 · 예약관리 | **배차** (명사), 나머지 맥락별 유지 |
| Invoice | 정산 · 인보이스 | **인보이스** (문서), **정산** (프로세스) |
| Payment | 결제 · 결제현황 · 총요금 · 결제내역 · 금액 · 결제금액 | 맥락별 유지 (UI 위치 다름) |
| Unassigned | 배차필요 · 배차없음 · 배정없음 · 필요 · (미배차) · (미배정) | **배차 필요** (일반), **(미배차)** (괄호 표기) |

---

## 5. Reservation vs Booking 사용 패턴

현재 파일에서 "예약" 관련 항목의 EN 번역에 Reservation과 Booking이 혼용되고 있다. 분석 결과, 암묵적인 사용 패턴이 존재한다.

| 맥락 | 사용 용어 | 예시 |
|------|---------|------|
| 예약 상태·현황 조회 | **Reservation** | Reservation, New Reservation, R.Status |
| 예약 객체에 대한 액션 | **Booking** | Cancel Booking, Copy Booking, Delete Booking, Close Booking |
| 요금 체계 | **Reservation** | Distance(Reservation), Distance Rate(Reservation) |
| 예약 접근 권한 | **Booking** | Booking access, Booking Info Visibility Settings |
| 알림 메시지 | **Reservation** | "The reservation has been cancelled." |

> **현행 패턴 정리:** "상태/조회" = Reservation, "액션/관리" = Booking으로 분기되어 있다. 이 패턴을 **명시적 규칙으로 채택**하면 현행 번역을 대부분 유지하면서 일관성을 확보할 수 있다.

---

## 6. 정산(Settlement) vs 인보이스(Invoice) 용어 구분

"정산"의 영어 번역이 맥락에 따라 Invoice와 Settlement으로 갈린다.

| 카테고리/맥락 | EN 번역 | 건수 | 설명 |
|-----------|--------|------|------|
| booking·CO·LC·NB·SS | **Invoice** | 6건 | 예약 완료 후 다음 단계 상태로서의 "정산" |
| SB·settlement | **Settlement** | 8건+ | 정산 관리 화면, 정산 상태 |

> **현행 패턴 정리:** 예약 흐름에서 상태명 = Invoice, 정산 관리 모듈 내부 = Settlement. 이 분기도 의도적으로 보이므로, **Invoice = 인보이스 발행 단계, Settlement = 정산 처리/완료 프로세스**로 구분하여 유지한다.

---

## 7. 상태값(status) 매핑 테이블

### 7.1 운행 상태 (status 카테고리)

| Key (수정불가) | EN | KR | JP | TH |
|-------------|-----|-----|-----|-----|
| NEW | NEW | 신규 | 新規 | ใหม่ |
| SCHEDULED | SCHEDULED | 예정 | 予定 | กำหนดไว้ |
| EN_ROUTE | EN ROUTE | 이동 | 移動 | ระหว่างทาง |
| ON_STANDBY | ON STANDBY | 대기 | 待機 | รอให้บริการผู้โดยสาร |
| IN_PROGRESS | IN PROGRESS | 진행 | 進行 | กำลังดำเนินการ |
| DROP_OFF | DROP OFF | 하차 | 下車 | ส่ง |
| DONE | DONE | 종료 | 終了 | เสร็จสิ้น |
| NO_SHOW | NO-SHOW | 노쇼 | ノーショー | ไม่ปรากฏตัว |
| ASSIGNED | Assigned | 확정 | 確定 | ยืนยัน |
| UNASSIGNED | Unassigned | 필요 | 必要 | ไม่ได้กำหนด |
| PENDING | Pending | 요청 | 要請 | คำขอ |
| CANCEL | CANCELED | 취소 | キャンセル | ยกเลิก |
| CANCELED | CANCELED | 취소 | キャンセル | ยกเลิก |
| COMPLETING | Completing | 예약진행 | 予約進行中 | กำลังดำเนินการจอง |
| COMPLETED | Completed | 예약완료 | 予約完了 | การจองเสร็จสิ้น |
| CLOSED | Closed | 예약마감 | 予約終了 | ปิดการจอง |
| UPDATE | UPDATE | 업데이트 | アップデート | ปรับปรุง |

### 7.2 예약 상태 (reservationStatus 카테고리)

| Key (수정불가) | EN | KR | JP | TH |
|-------------|-----|-----|-----|-----|
| NEW | New | 신규예약 | 新規予約 | การจองใหม่ |
| ACCEPTED | Accepted | 예약확정 | 予約確定 | การจองแน่นอน |
| COMPLETING | Completing | 예약진행 | 予約進行中 | กำลังดำเนินการจอง |
| COMPLETED | Completed | 서비스완료 | サービス完了 | การจองสิ้น |
| CANCELED | Canceled | 예약취소 | 予約キャンセル | การจองถูกยกเลิก |
| CLOSED | Closed | 예약마감 | 予約終了 | ปิดการจอง |
| DELETE | Deleted | 예약삭제 | 予約削除 | การจองถูกลบ |
| DELETED | Deleted | 예약삭제 | 予約削除 | การจองถูกลบ |

---

## 8. 서비스 유형 번역 매핑

카테고리에 따라 EN이 ALL CAPS(PC) vs Title Case(common·SS)로 분기되어 있다. PC 카테고리는 시스템 내부 코드용이므로 현행 유지한다.

| Key | EN (common/SS) | EN (PC) | KR | JP | TH |
|-----|---------------|---------|-----|-----|-----|
| CHAUFFEUR | Chauffeur | CHAUFFEUR | 쇼퍼 | ショーファー | พนักงานขับรถ |
| CONCIERGE | Concierge | CONCIERGE | 컨시어지 | コンシェルジュ | เจ้าหน้าที่ดูแลลูกค้า |
| TRANSFER | Transfer | TRANSFER | 편도 | 片道 | เที่ยวเดียว |
| HOURLY | Hourly | HOURLY | 시간대절 | 時間貸し切り | รายชั่วโมง |
| DAILY | Daily | DAILY | 1일대절 | 一日貸し切り | รายวัน |
| ARRIVAL | Arrival | ARRIVAL | 도착/입국 | 到着 | มาถึง |
| DEPARTURE | Departure | DEPARTURE | 출발/출국 | 出発 | ออกเดินทาง |
| TRANSIT | Transit | TRANSIT | 환승 | 乗り継ぎ | จุดแวะ |
| PROTOCOL | Protocol | PROTOCOL | 수행 | 遂行 | มาตรการ/การดำเนินการ |

> ⚠ **JP 불일치:** booking 카테고리에서 Chauffeur→"Chauffeur"(영문 그대로), Concierge→"Concierge"(영문 그대로)로 되어 있으나, SS 카테고리에서는 각각 "ショーファー", "コンシェルジュ"로 카타카나 표기. **카타카나로 통일 권장.**

---

## 9. 영국식/미국식 철자 잔존

5건의 "cancelled" (영국식)이 남아 있다. 시스템 전체가 "canceled" (미국식)을 기준으로 하므로 통일이 필요하다.

| 카테고리 | 키 | 현재 EN | 수정안 |
|--------|-----|--------|------|
| aligo | 예약취소성공 | "Successfully cancelled." | "Successfully canceled." |
| aligo | 예약취소실패 | "Failed to cancelled the reservation..." | "Failed to cancel the reservation..." |
| cancellation | 취소확인 | "The reservation has been cancelled." | "The reservation has been canceled." |
| cancellation | 취소확정알림 | "The reservation has been cancelled" | "The reservation has been canceled" |
| common | 배차요청취소 | "Your request has been cancelled." | "Your request has been canceled." |

> 참고: aligo/예약취소실패의 "Failed to cancelled"는 문법 오류이기도 하다 (cancelled → cancel).

---

## 10. 표준 용어집 (Glossary)

### 10.1 브랜드 고유명사 (모든 언어 동일)

| 용어 | 표기 규칙 |
|------|---------|
| T-RiseUp | 하이픈 포함, RiseUp 대문자 |
| RIDEUS | 전체 대문자 |
| PMS / TMS / TIS | 약어, 대문자 유지 |
| DISPATCH · CONCIERGE · PARTNERS · BOOKING | 채널명, 대문자 유지 |
| GNET | 외부 연동 네트워크, 대문자 유지 |

### 10.2 사용자 역할

| KR (표준) | EN | JP | TH |
|---------|-----|-----|-----|
| 어드민 | Admin | アドミン | ผู้ดูแลระบบ |
| 매니저 | Manager | マネージャー | ผู้จัดการ |
| 스태프 | Staff | スタッフ | พนักงาน |
| 기사 | Driver | ドライバー | พนักงานขับรถ |
| 컨시어지 | Concierge | コンシェルジュ | เจ้าหน้าที่ดูแลลูกค้า |
| 협력사 | Affiliate | 協力会社 | บริษัทในเครือ |
| 파트너 | Partner | パートナー | คู่ค้า |
| 법인고객 | Corporate Client | 法人顧客 | ลูกค้าองค์กร |
| 승객 | Passenger | 乗客 | ผู้โดยสาร |

### 10.3 요금 용어

| KR (표준) | EN | JP | TH |
|---------|-----|-----|-----|
| 기본 요금 | Base Rate | 基本料金 | อัตราค่าบริการพื้นฐาน |
| 추가 요금 | Surcharge | 追加料金 | ค่าบริการเพิ่มเติม |
| 봉사료 | Service Charge | サービスチャージ | ค่าบริการ |
| 세금 | Tax | 税金 | ภาษี |
| 팁 | Gratuity | チップ | ทิป |
| 할인 | Discount | 割引 | ส่วนลด |

### 10.4 차량 등급

| KR | EN | JP | TH |
|----|-----|-----|-----|
| 스탠다드 | Standard | スタンダード | คลาสมาตรฐาน |
| 프리미엄 | Premium | プレミアム | พรีเมี่ยม |
| 비즈니스 | Business | ビジネス | ชั้นธุรกิจ |
| 이코노미 | Economy | エコノミー | ชั้นประหยัด |
| 퍼스트클래스 | First Class | ファーストクラス | ชั้นหนึ่ง |
| 세단 | Sedan | セダン | ซีดาน |
| SUV | SUV | SUV | SUV |
| MPV | MPV | MPV | MPV |
| VAN | VAN | バン | รถตู้ |

---

## 11. 번역 규칙

### R-01. 고유명사 처리

서비스 브랜드명(T-RiseUp, RIDEUS, PMS, TMS, TIS), 채널명(DISPATCH, CONCIERGE, PARTNERS, BOOKING), 외부 연동명(GNET, Aligo)은 모든 언어에서 영문 그대로 표기한다.

### R-02. EN 대소문자 규칙

| 용도 | 형식 | 예시 |
|------|------|------|
| status 카테고리 (시스템 코드) | UPPER CASE | NEW, SCHEDULED, EN ROUTE, NO-SHOW |
| reservationStatus (UI 상태) | Title Case | New, Accepted, Canceled |
| PC 카테고리 (요금 코드) | UPPER CASE | TRANSFER, HOURLY, CHAUFFEUR |
| common·SS (UI 라벨) | Title Case | Transfer, Hourly, Chauffeur |
| 버튼 라벨 | Title Case | Cancel Booking, Save, Confirm |
| 알림·안내 메시지 | Sentence case | "The reservation has been canceled." |

### R-03. 영어 철자

미국식 영어(American English) 통일: canceled (not cancelled), color (not colour).

### R-04. 한국어 띄어쓰기

복합명사의 KR 표시값은 띄어쓰기한다. 키(key)는 변경하지 않으므로 기존 붙여쓰기 유지.

| key (변경 불가) | kr 표시값 (띄어쓰기 적용) |
|-------------|-------------------|
| 기본요금 | 기본 요금 |
| 컨시어지요금 | 컨시어지 요금 |
| 서비스레벨 | 서비스 레벨 |
| 직접입력 | 직접 입력 |

### R-05. Reservation vs Booking 분기 규칙

| 맥락 | EN 용어 | 예시 |
|------|--------|------|
| 예약 상태·현황·조회·통계 | **Reservation** | New Reservation, R.Status, Reservation Count |
| 예약 객체에 대한 액션·관리 | **Booking** | Cancel Booking, Copy Booking, Booking Details |
| 알림 메시지 내 예약 언급 | **reservation** (소문자) | "The reservation has been canceled." |

### R-06. Invoice vs Settlement 분기 규칙

| 맥락 | EN 용어 | 설명 |
|------|--------|------|
| 예약 흐름 내 정산 상태 라벨 | **Invoice** | 예약→완료→정산(Invoice) 단계명 |
| 정산 모듈(settlement) 내부 | **Settlement** | Settled, Unsettled, Settlement Details |
| 인보이스 문서 자체 | **Invoice** | Invoice No., Invoice Components |

### R-07. JP 번역 규칙

1. 외래어는 카타카나: Chauffeur→"ショーファー", Concierge→"コンシェルジュ". 영문 그대로 쓰지 않는다.
2. UI 라벨은 명사 종지형: 予約管理, 配車状況
3. 안내 메시지는 です/ます체: "予約を保存しました。"

### R-08. TH 번역 규칙

1. ครับ/ค่ะ(존칭) 생략하고 중립적 표현 사용.
2. 영어 약어(GPS, QR, API, SUV, VIP)는 영문 유지.
3. 아라비아 숫자 사용 (태국 숫자 ๐๑๒ 사용 금지).

### R-09. 톤앤매너

T-RiseUp은 전문적이고 신뢰감 있는 B2B 모빌리티 SaaS이다.

| 구분 | 권장 | 지양 |
|------|------|------|
| 전반 | 간결하고 명확 | 구어체, 이모지, 감탄사 |
| 성공 메시지 | "저장되었습니다." | "저장 완료!!" |
| 오류 메시지 | "등록에 실패했습니다. 다시 시도해 주세요." | "등록이 안 됐어요" |
| 버튼 | 동사 종지형 ("저장", "삭제", "확인") | 서술형 ("저장합니다") |

---

## 12. 자동 번역 제안기 로직

한국어 용어 입력 시 번역을 제안하는 파이프라인.

```
입력: kr_input (한국어 용어), type (status | label | button | message)

1. 용어집 정확 매칭 → 있으면 즉시 반환
2. 고유명사 검출 (R-01) → T-RiseUp, RIDEUS 등 분리 후 나머지만 번역
3. 유형별 EN 포맷 적용 (R-02):
   - status → UPPER CASE
   - label·button → Title Case
   - message → Sentence case
4. 맥락 분기 적용:
   - 예약 관련 → R-05 (Reservation vs Booking)
   - 정산 관련 → R-06 (Invoice vs Settlement)
5. 언어별 규칙:
   - EN: R-03 미국식 철자
   - KR: R-04 띄어쓰기
   - JP: R-07 카타카나·경어
   - TH: R-08 존칭 생략·숫자
6. 검증:
   - EN에 한국어 문자 없는지
   - JP에 영문 그대로 들어가지 않았는지 (고유명사 제외)
   - 기존 키와 중복 없는지
```

**적용 예시:**

| 입력 (KR) | 유형 | EN | JP | TH |
|---------|------|-----|-----|-----|
| 배차 요청 알림 | message | Dispatch request notification | 配車リクエスト通知 | การแจ้งเตือนคำขอจัดรถ |
| RIDEUS Booking 결제 완료 | status | RIDEUS Booking PAID | RIDEUS Booking 支払済 | RIDEUS Booking จ่ายแล้ว |
| 일괄 정산 | button | Batch Settle | 一括精算 | หักบัญชีทั้งหมด |
| 인보이스 발송 | button | Send Invoice | インボイス送信 | ส่งใบแจ้งหนี้ |

---

## 13. 카테고리 약어 참조표

현재 약어로 된 카테고리명의 추정 매핑이다. 신규 키 추가 시 올바른 카테고리 배정에 활용한다.

| 약어 | 추정 풀네임 | 주요 내용 |
|------|---------|---------|
| AF | Affiliate | 협력사 관리 |
| AG | Agent | 에이전트 관리 |
| AL | Alliance | 얼라이언스/제휴사 |
| BTN | Button | 공통 버튼 라벨 |
| CM | Confirmation Message | 확인·경고 메시지 |
| CO | Common Options | 공통 옵션·드롭다운 값 |
| CP | Company Profile | 회사 프로필·설정 |
| CU | Customer | 고객(개인) 관리 |
| LC | Log/Completion | 운행 기록·완료 처리 |
| LI | List | 리스트 뷰 항목 |
| LM | Limit | 한도·금액 관련 |
| MA | Map | 실시간 지도·관제 |
| MAP | Map (extended) | 지도 POI·차량 위치 |
| NB | Navigation/Booking | 예약 화면 주요 UI |
| NOTI | Notification | 알림톡·알림 관리 |
| PC | Price/Copy rates | 요금 설정·복사 |
| PT | Portal/Theme | 포털 UI·개인 설정 |
| SB | Sidebar | 사이드바 메뉴·필터 |
| SC | Schedule | 스케줄·시간대 |
| SF | Staff | 기사·인력 관리 |
| SS | System Settings | 시스템 설정 |
| SU | Service User | 서비스 사용자(승객) |
| VC | Vehicle | 차량 관리 |
| ZO | Zone | 존(구간) 설정 |
| ZZ | Miscellaneous | 기타·공통 에러 |

---

*끝.*
