# 🐾 동물 카드 짝맞추기

교회 어린이 게임 세션을 위한 카드 뒤집기 기억력 게임입니다. TV 화면에 연결해 다 같이 즐길 수 있도록 만들어졌어요.

![Card Flip Game](icon-512.png)

## ✨ 주요 기능

- 🎮 **3가지 난이도** — 쉬움 (4×4) / 보통 (4×6) / 어려움 (6×6)
- 📺 **TV 화면 최적화** — 큰 카드, 큰 글씨로 멀리서도 잘 보임
- ⏱️ **타이머 & 이동 횟수** — 게임 진행 상황을 실시간 표시
- 🏆 **최고 기록 저장** — 난이도별로 브라우저에 자동 저장
- 🎵 **효과음** — Web Audio API 사용 (별도 음원 파일 불필요)
- 🎉 **승리 축하 색종이 효과**
- 📱 **PWA 지원** — 한 번 로드하면 인터넷 없이도 사용 가능
- ⌨️ **키보드 단축키** — `1`/`2`/`3` (난이도), `R` (다시하기)

## 📁 파일 구조

```
cardflip/
├── index.html          # 메인 페이지
├── style.css           # 스타일
├── app.js              # 게임 로직
├── manifest.json       # PWA 설정
├── service-worker.js   # 오프라인 캐싱
├── icon-192.png        # 앱 아이콘 (작은)
└── icon-512.png        # 앱 아이콘 (큰)
```

## 🚀 GitHub Pages에 배포하기

### 1단계: GitHub에 저장소 만들기

1. [GitHub](https://github.com)에 로그인
2. 우측 상단 `+` → **New repository** 클릭
3. 저장소 이름 입력 (예: `cardflip-game`)
4. **Public**으로 설정
5. **Create repository** 클릭

### 2단계: 파일 업로드

저장소 페이지에서:

1. **uploading an existing file** 링크 클릭
2. 이 폴더의 모든 파일을 드래그 앤 드롭
   - `index.html`, `style.css`, `app.js`
   - `manifest.json`, `service-worker.js`
   - `icon-192.png`, `icon-512.png`
3. **Commit changes** 클릭

### 3단계: GitHub Pages 활성화

1. 저장소 페이지에서 **Settings** 탭 클릭
2. 왼쪽 메뉴에서 **Pages** 클릭
3. **Source** 섹션에서:
   - Branch: `main` 선택
   - Folder: `/ (root)` 선택
4. **Save** 클릭
5. 1~2분 후 페이지 상단에 나타나는 URL이 게임 주소예요!
   - 예: `https://[사용자이름].github.io/cardflip-game/`

### 4단계: TV 연결 노트북에 설치 (PWA)

배포된 URL에 접속한 후:

**Chrome/Edge**:
- 주소창 오른쪽에 ⊕ 또는 설치 아이콘 클릭
- "설치" 버튼 클릭
- 데스크톱에 앱 아이콘 생김

**iPad/iPhone (Safari)**:
- 공유 버튼 → "홈 화면에 추가"

설치 후에는 인터넷이 없어도 작동해요!

## 🖥️ 로컬에서 사용하기

### 옵션 A: 단일 파일 버전 (가장 간단)

`index.html` 파일을 더블클릭하면 바로 실행됩니다. 인터넷이나 서버 필요 없음.

> ⚠️ 단일 파일 버전은 PWA 기능(설치, 완전 오프라인)이 없습니다. 폰트는 인터넷이 있을 때 로드되지만, 폰트 없이도 게임은 정상 작동해요.

### 옵션 B: 로컬 서버로 PWA 테스트

PWA 기능을 로컬에서 테스트하려면 간단한 웹 서버가 필요해요:

```bash
# Python이 설치되어 있다면
cd cardflip
python3 -m http.server 8000

# 브라우저에서 http://localhost:8000 접속
```

## ⌨️ 사용법

| 키 | 동작 |
|---|---|
| `1` | 쉬움 모드 시작 |
| `2` | 보통 모드 시작 |
| `3` | 어려움 모드 시작 |
| `R` | 다시하기 |
| `Esc` | 결과 창 닫기 |

마우스 또는 터치로 카드를 클릭하면 뒤집힙니다.

## 🎨 카드 내용 변경하기 (이모지 → 이미지)

추후 동물 이모지를 직접 만든 이미지로 바꾸고 싶으시면:

### 1. 이미지 파일 추가

`images/` 폴더를 만들고 동물 이미지 18장 추가:
```
images/
├── dog.png
├── cat.png
├── lion.png
...
```

### 2. `app.js` 수정

```javascript
// 기존 (이모지)
const ANIMAL_POOL = ['🐶', '🐱', '🦁', ...];

// 변경 (이미지)
const ANIMAL_POOL = [
  'images/dog.png',
  'images/cat.png',
  'images/lion.png',
  ...
];
```

### 3. `index.html`의 카드 렌더링 부분 수정

`renderGrid()` 함수에서:

```javascript
// 기존
<span>${card.content}</span>

// 변경
<img src="${card.content}" alt="동물">
```

### 4. CSS 약간 조정

`.card-front img` 스타일 추가:
```css
.card-front img {
  width: 75%;
  height: 75%;
  object-fit: contain;
}
```

## 🛠️ 기술 스택

- **순수 HTML/CSS/JavaScript** — 빌드 도구 없음, 의존성 없음
- **Web Audio API** — 효과음 (외부 음원 파일 불필요)
- **Canvas API** — 색종이 효과
- **localStorage** — 최고 기록 저장
- **Service Worker** — 오프라인 지원
- **Google Fonts** — Fredoka (영문/숫자) + Gaegu (한글)

## 📝 참고 사항

- 처음 한 번은 인터넷이 필요해요 (폰트 + 서비스 워커 캐싱)
- 한 번 캐싱된 후엔 완전 오프라인으로 작동
- 최고 기록은 브라우저별로 저장되므로 다른 기기로 옮겨가지 않음
- 브라우저 캐시를 지우면 최고 기록도 삭제됩니다

## 💝 만든 이유

교회 주일학교 어린이 게임 세션 중 하나로 사용할 목적으로 제작되었습니다. 유치부부터 초등 고학년까지 다양한 연령대의 아이들이 큰 TV 화면을 보며 다 같이 즐길 수 있도록 디자인했어요.

즐거운 시간 되세요! 🎉
