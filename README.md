# keural-code-test

## sin(x) + cos(y) 그래프

`index.html` — 브라우저에서 열면 바로 동작하는 단일 HTML 파일입니다. 외부 의존성·빌드 없음.

### 사용법

브라우저에서 `index.html`을 열거나, 저장 후 로컬 서버로 띄웁니다.

```bash
python3 -m http.server 8000
```

접속: http://localhost:8000

### 기능

- `x`, `y` 값 입력 → `sin(x) + cos(y)` 값을 즉시 계산해 표시 (라디안/도 단위 선택)
- **곡선 차트**: 고정된 `y`에 대해 `sin(x) + cos(y)` 곡선. 기준 `sin(x)`(점선)와 이동량 `cos(y)`(수평선)를 함께 표시
- **히트맵**: x-y 평면 위 `sin(x) + cos(y)` 분포를 색으로 표현 (값 범위 -2 ~ 2)
- 표시 구간(시작/끝) 지정, 프리셋 버튼, 초기화 지원
- 입력값이 표시 구간 밖이면 구간을 자동으로 확장

### 구조

- `<script id="core">` — DOM 비의존 계산 로직 (`Core.fxy`, `Core.curvePoints`, `Core.heatMatrix`, `Core.axisWindow`, `Core.heatColor`)
- `<script id="app">` — 캔버스 렌더링 및 이벤트 처리
