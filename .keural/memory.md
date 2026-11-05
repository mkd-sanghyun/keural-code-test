# Project Memory

## 검증 도구
- 이 환경에는 JS 엔진(node/deno/bun 등)이 **없다**. JS 검증은 `pip install quickjs` 후 `python3 -c "import quickjs"` 로 수행한다 (설치 위치: /tmp, 커밋 금지).
- `quickjs` 로 HTML 내 `<script>` 블록을 추출해 계산 로직 검증 + 스텁 DOM(`document`/`window`/`canvas 2d ctx`)으로 앱 레이어까지 실행 검증 가능.
- `Float64Array` 는 `JSON.stringify` 로 직렬화되지 않으므로 `Array.prototype.slice.call(arr)` 로 변환해야 한다.

## Gotcha: 캔버스 무한 확대 루프
- 캔버스 `width`/`height` 속성을 JS로 설정하면 CSS 레이아웃 크기가 변해 `getBoundingClientRect()` 값이 커진다 → 렌더마다 캔버스가 계속 커지는 무한 확대 루프.
- 해결: 캔버스 높이를 CSS로 고정(`height: 360px;`)하고 JS에서는 백버퍼 크기만 갱신.

## 구조 규칙
- `index.html` 은 `<script id="core">`(DOM 비의존 계산) + `<script id="app">`(렌더링/이벤트) 2블록으로 분리. core 는 테스트 가능하도록 DOM 참조 금지.
