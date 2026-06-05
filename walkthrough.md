# 햄스터 뽀모도로 타이머 & 주간 집중 시각화 개발 완료 보고서 🐹✨

대표님! 1인 기업가 대표님을 든든하게 보좌할 **'햄스터 뽀모도로 타이머'** 개발 및 **'주간 집중 시간 시각화(월~일)'** 기능 구현을 완수하였습니다!

본 개발에서는 대표님의 피드백을 받아 다음과 같은 사양으로 기능을 설계 및 완성하였습니다.
- **Tailwind CSS v3** 기반의 반응형 다크 톤 웹 환경
- **시간 커스텀 설정** (Focus/Break 시간 수동 입력 기능)
- 상태에 따라 애니메이션이 바뀌는 **귀여운 햄스터 마스코트** (대기/집중 코딩/휴식 잠자기)
- **주간 집중 리포트 차트** (월~일 요일별 누적 시간 바 그래프, `localStorage` 연동 및 체험 데이터 지원)
- **비프음 사운드 및 한국어 TTS 브리핑** ("대표님, 쉴 시간입니다!" 음성 안내)

---

## 📸 동작 및 UI 검증 결과

타이머 동작과 요일별 주간 집중 시간 시각화 카드의 동작 및 반응형 레이아웃의 검증 과정입니다.

### 1. 뽀모도로 타이머 핵심 동작 검증
````carousel
![기본 화면 및 대기 상태](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/main_page_1780628099445.png)
<!-- slide -->
![집중 모드 카운트다운 시작](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/countdown_started_1780628118097.png)
<!-- slide -->
![휴식 모드 자동 전환](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/break_session_transition_1780628262280.png)
<!-- slide -->
![모바일 뷰포트 반응형 화면](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/mobile_viewport_1780628269405.png)
<!-- slide -->
![전체 동작 검증 영상](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/pomodoro_verification_1780628074592.webp)
````

### 2. 주간 집중 리포트 시각화 동작 검증
````carousel
![리포트 초기 상태(데이터 없음)](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/no_data_chart_1780629269446.png)
<!-- slide -->
![체험용 데이터 채우기 결과](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/demo_data_chart_1780629278966.png)
<!-- slide -->
![모바일 상단 뷰포트(500x812)](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/mobile_top_500x812_1780629306811.png)
<!-- slide -->
![모바일 하단 차트(500x812)](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/mobile_chart_500x812_1780629309842.png)
<!-- slide -->
![차트 기능 동작 검증 영상](C:/Users/guddls/.gemini/antigravity-ide/brain/4e49efd1-ad7d-44ad-bbb8-f774b2fecaf9/weekly_chart_verification_1780629254655.webp)
````

---

## 🛠️ 추가 구현된 주요 내용 (주간 집중 리포트)

1. **요일별 막대그래프 시각화 (WeeklyChart.jsx)**
   - 월요일부터 일요일까지 요일별 집중 시간(분)을 둥근 그라데이션 막대로 표시합니다.
   - 막대마다 호버 시 요일별 **햄스터 테마 이모지** 및 해당 요일 집중 시간이 말풍선 툴팁으로 부드럽게 노출됩니다.
   - 1주간 집중한 총합 시간을 시간/분 포맷(예: "이번 주 총 5시간 40분 집중하셨습니다!")으로 자동 연산합니다.
2. **실시간 자동 누적 및 localStorage 연동 (App.jsx)**
   - 타이머 집중 세션이 끝날 때마다 자바스크립트 `Date` 객체로 현재 요일을 파악하여 자동으로 가산합니다.
   - 브라우저를 재부팅하거나 페이지를 나갔다 들어와도 `localStorage`를 통해 기록이 영구 보존됩니다.
3. **체험 데이터 및 초기화 관리**
   - 차트 초기 진입 시 빈 레이아웃의 허전함을 채워줄 수 있는 **체험용 데이터 채우기** 기능을 제공합니다.
   - 클릭 시 한 번에 예시 누적 데이터(월 45분, 화 90분...)를 채워 비주얼을 확인하고, 필요 시 원클릭으로 초기화(Reset)할 수 있습니다.

---

## 🧪 테스트 및 품질 검증

### 자동화 테스트 (Vitest & RTL)
- `TimerDisplay.test.jsx` 및 `WeeklyChart.test.jsx`를 작성하여 뽀모도로 시간 포맷팅, 세션 타입에 따른 뱃지 분기, 주간 합계 연산 함수 및 버튼 콜백 동작 등을 전부 단위 검증하였습니다.
- **테스트 결과**: **7개 케이스 전체 통과(Passed)**.

### 수동 브라우저 검증
- 로컬 개발 환경(`http://localhost:5173`) 상에서 체험 데이터 주입, 초기화 다이얼로그 확인, 집중 종료 시 실시간 가산 작동, 500px 모바일 레이아웃 뷰포트 정렬을 완료하였습니다.
