# 202130118 송태경
# 2025-12-03 강의
## 기말고사

# 2025-11-26 강의
## WebP 파일 특징
### 파일 크기가 작아 로딩 속도 개선
### 무손실/손실 압축, 투명도(Alpha), 애니메이션 지원
### 저장 공간 절약 + 전송 속도 증가
### 고품질 이미지를 효율적으로 표현

## 핵심 성능 최적화 기법
### 이미지 최적화 (Image Optimization)
### Next.js의  컴포넌트는 웹 성능 측정 지표(Core Web Vitals) 개선을 위한 핵심 요소입니다.

## 주요 기능: 
### 크기 및 형식 최적화: 사용자 디바이스에 적합한 크기의 이미지를 자동으로 생성 및 제공하며, 압축률이 우수한 WebP 형식 등으로 변환하여 파일 크기를 최소화합니다.
### CLS(Cumulative Layout Shift) 방지: 이미지의 width와 height를 예약하여 로딩 중 레이아웃이 밀리는 현상을 원천적으로 방지합니다.
###  Lazy Loading: 뷰포트 내에 들어오기 직전까지 이미지 로드를 지연시켜 초기 페이지 로드 속도를 향상시킵니다. 
### 사용 권장 방식: 이미지 파일을 import 하는 방식은 빌드 시점에 크기를 알 수 있어 width/height 지정 없이도 자동 최적화가 적용되는 권장 방식입니다.
### public 폴더 사용 시에는 반드시 크기를 명시해야 합니다.
# 2025-11-19 강의
## 테일윈드 CSS
### 테일윈드 CSS사용자 정의 디자인을 구축하기 위한 저수준 유틸리티 클래스를 제공하는 유틸리티 중심 CSS 프레임워크입니다.
## Tailwind CSS 설치:
> pnpm add -D tailwindcss @tailwindcss/postcss
<br> 
## 파일 에 PostCSS 플러그인을 추가합니다 <br>
> postcss.config.mjs.<br>
export default {<br>
  plugins: {<br>
    '@tailwindcss/postcss': {},<br>
     },<br>
}
<br>
## 글로벌 CSS 파일에 Tailwind를 가져옵니다.
> @import 'tailwindcss';
<br>

- 루트 레이아웃에 CSS 파일을 가져옵니다.<br>
 > import './globals.css'
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
<br>
## 이제 애플리케이션에서 Tailwind의 유틸리티 클래스를 사용할 수 있습니다.
> export default function Page() {
  return (
    <br>main className="flex min-h-screen flex-col <br>items-center justify-between p-24">
      <br> h1 className="text-4xl font-bold">Welcome to Next.<br>js!</h1>
    <br> /main>
 <br> )
<br>}

## CSS 모듈
### CSS 모듈은 고유한 클래스 이름을 생성하여 CSS의 로컬 범위를 지정합니다. 이를 통해 이름 충돌 걱정 없이 여러 파일에서 동일한 클래스를 사용할 수 있습니다.

### CSS 모듈을 사용하려면 확장자가 있는 새 파일을 만들고<br> 디렉토리 .module.css내의 모든 구성 요소로 가져오세요

## 글로벌 CSS

### 글로벌 CSS를 사용하면 애플리케이션 전체에 스타일을 적용할 수 있습니다.

#### 파일을 만들고 app/global.css루트 레이아웃으로 가져와서 애플리케이션의 모든 경로 에 스타일을 적용합니다.

 > 전역 스타일은 디렉터리 내의 모든 레이아웃, 페이지 또는 컴포넌트로 가져올 수 있습니다 <br>app. 하지만 Next.js는 Suspense와 통합하기 위해 React의 내장 스타일시트 지원을 사용하기 때문에,<br> 현재 경로 간 이동 시 충돌을 일으킬 수 있는 스타일시트가 제거되지 않습니다.<br> Tailwind의 기본 스타일처럼 진정한 전역 CSS에는 전역 스타일을, 컴포넌트 스타일에는 Tailwind CSS를 , <br>그리고 필요에 따라 사용자 지정 범위 CSS에는<br> CSS Modules를 사용하는 것이 좋습니다.
 
 
 ## 외부 스타일시트
- 외부 패키지에서 게시된 스타일시트는 공동 배치된 구성 요소를 포함하여 디렉토리의 어느 곳으로나 가져올 수 있습니다
> import 'bootstrap/dist/css/bootstrap.css'
 <br>export default function RootLayout({
  <br>children,
<br>}: {
  <br>children: React.ReactNode
<br>}) {
  <br>return (
    <br> html lang="en">
      <br> body className="container">{children}</body>
    <br></html>
  )
}
# 2025-11-12 강의
## 스트리밍 (Streaming)

### 개념 요약
### 스트리밍은 페이지 HTML을 한 번에 모두 렌더링하지 않고, 작은 조각 단위로 잘라 순차적으로 전송하는 방식입니다.
### 초기 화면을 더 빨리 띄워서 사용자에게 콘텐츠를 빠르게 보여 줄 수 있음.
## 전제 조건
### cacheComponents_config 옵션이 활성화되어 있다고 가정.
### Next.js 15 Canary 버전부터 본격 지원.
### latest는 안정(stable) 버전, canary는 최신 개발(dev) 버전.
## 특징
### 서버 컴포넌트에서 async/await을 사용하면 Next.js는 해당 부분을 동적 렌더링(Server Rendering) 대상으로 판단함.
### 요청이 들어올 때 서버에서 데이터를 가져와 그 결과를 기준으로 렌더링을 수행.
### 데이터 응답이 느리면 전체 화면이 늦게 나올 수 있으므로, 이럴 때 스트리밍을 사용하면 부분적으로 먼저 보여 줄 수 있어 유리함.

## 스켈레톤 vs 스피너

## 스켈레톤 (Skeleton)
### 최종 콘텐츠의 레이아웃이나 구조를 회색 블록 등으로 먼저 보여주는 방식.
### 스피너 (Spinner)
### 단순히 “로딩 중”임을 알려주는 회전 아이콘 형태의 표시.
### 게시글 목록, 카드, 썸네일처럼 레이아웃이 중요한 화면에서는 스켈레톤이 사용자 경험 측면에서 더 좋을 때가 많음.
### 데이터 Fetch 패턴

## 순차적 Fetch (Sequential Fetch)
### 컴포넌트 트리 상에서 상위 → 하위 순서로 데이터를 가져올 때 발생.
### 예: Playlists를 가져오려면 먼저 Artist의 artistID가 필요해서, Artist 데이터를 전부 받은 뒤에야 Playlists fetch를 시작할 수 있는 경우.
### 이런 식으로 요청들 사이에 의존성이 존재함.
### 병렬 Fetch (Parallel Fetch)
### 하나의 경로 안에서 여러 데이터 요청을 동시에 진행하는 패턴.
### 기본적으로 레이아웃(Layout)과 페이지(Page)는 병렬로 렌더링됨.
### 한 컴포넌트 안에서 여러 await를 순서대로 쓰면 직렬 실행이 될 수 있으므로, 병렬 처리를 위해 Promise.all을 활용할 수 있음.
# 2025-11-05 강의
## 대림 테크페어 준비

# 2025-10-29 강의
## Context Provider (컨텍스트 제공자) <br>
 ### Props 없이도 전역 상태(theme, 언어 등)를 트리 전체에 공유할 수 있다.<br>
### Provider를 Server Component에서 감싸면, 하위 Client Component들이 동일한 Context를 사용할 수 있다.

## CSS 적용 (Attribute Selector) <br>
### html[data-theme='light'] 형식으로 테마를 구분한다.<br>
### 클래스보다 충돌이 적고 전역 테마 관리에 적합하다.<br>

## useEffect Hook 설명
### HTML 문서 전체에 theme를 적용하는 전형적인 패턴이다.<br>
### typeof window !== "undefined" 조건을 넣어 SSR 환경에서도 안전하게 실행되도록 한다.<br>
## Provider 구성 시 주의<br>
### ThemeProvider는 <html> 대신 {children}만 감싸야 한다.<br>
### Provider는 트리에서 한 번만 사용하는 것이 좋다 → 불필요한 렌더링 방지.<br>
### 이렇게 하면 Server Component의 정적 부분을 최적화하기 쉬워진다.<br>
## 환경 변수 노출 방지<br>
### JS 모듈은 server와 client가 공유될 수 있으므로 주의해야 한다.<br>
### 서버 전용 코드(process.env)는 client에서 접근하지 않도록 분리한다.<br>

## 데이터 가져오기 (Fetching Data)
### 서버 컴포넌트에서 데이터를 가져오는 방법: <br>
### fetch API 사용<br>
### ORM 또는 데이터베이스 직접 접근<br>
#### fetch 사용 시 컴포넌트를 비동기 함수(async) 로 선언해야 한다.<br>
# 2025-10-22 강의
## Next.js 핵심 개념 요약: SC/CC Interleaving & Context
### Server/Client Component Interleaving
Interleaving은 **Server Component (SC)**와 **Client Component (CC)**를 혼합하여 성능과 상호작용성을 모두 확보하는 핵심 전략입니다. Server Component (SC): 서버에서 데이터 패칭 및 초기 렌더링을 담당하여 정적 HTML을 생성합니다. 역할: 초기 로딩 속도 최적화.

Client Component (CC): 브라우저에서 **상호작용성(useState, onClick 등)**을 담당하며, 하이드레이션이 일어나는 부분입니다. 작동 방식: SC가 만든 정적 HTML을 CC의 children 자리에 삽입하고, CC만 클라이언트에서 JavaScript로 연결됩니다.

## 2. Context Provider 사용 전략
### Context는 상태를 관리하므로 반드시 Client Component여야 합니다 ("use client" 필수).

전략: Client Component인 Context Provider를 **Server Component인 Root Layout (layout.tsx)**이 감싸도록 구성합니다. 결과: Provider가 앱의 최상단에서 렌더링되므로, 하위에 있는 모든 Client Component와 Server Component가 전역 Context를 공유할 수 있게 됩니다.

## 3. CSS 적용: 속성 선택자
### Context의 상태(State)에 따라 전역적인 테마를 변경할 때, CSS **속성 선택자 (Attribute Selector)**를 사용합니다.<br> 원리: Context Provider에서 태그에 data-theme="light"나 data-theme="dark"와 같은 속성을 설정합니다. <br> 활용: CSS에서 html[data-theme='dark']와 같이 속성값을 직접 선택하여 스타일을 지정합니다.<br> 이는 클래스 충돌 없이 전역 테마 관리를 용이하게 합니다.

# 2025-10-17 강의

## 병결

# 2025-10-15 강의

## 시험

# 2025-10-08 강의

## 휴일

# 2025-10-01 강의
## Next.js 네비게이션 & 전환 정리 (App Router)
- 1-4. Client-side transitions (클라이언트 측 전환)
- 일반적으로 서버 렌더링 페이지로 이동하면 전체 페이지가 로드
- → 이로 인해 state가 삭제되고, 스크롤 위치가 재설정되며, 상호작용이 차단

- Next.js의 <Link> 컴포넌트를 사용하면 클라이언트 측 전환을 통해 이를 방지

- 페이지를 다시 로딩하는 대신, 다음과 같은 방법으로 콘텐츠를 동적으로 업데이트
- 공유 레이아웃과 UI를 유지
- 현재 페이지를 미리 가져오기(prefetching) → 로딩 상태 또는 사용 가능한 경우 새 페이지로 빠르게 전환
- 핵심 포인트
- 클라이언트 측 전환은 서버에서 렌더링된 앱을 클라이언트에서 렌더링된 앱처럼 느껴지게 하는 요소
- 프리페칭 + 스트리밍과 함께 사용하면 동적 경로에서도 빠른 전환이 가능

# 2025-09-24 강의

## 외조모상으로 인한 수업 미참석 

# 2025-09-17 강의

## 용어 정의
- route(라우트): 경로. routing(라우팅): 경로를 찾아가는 과정.
- path: URL 경로 문자열.
- directory / folder: 라우팅 맥락에서 폴더는 URL 세그먼트에 대응.
- segment: 라우팅과 매핑되는 폴더(경로의 한 구간).

## 브랜치 생성

- git checkout -b <브랜치이름>
- git switch -c <브랜치이름>
-  git branch <브랜치이름>

## git switch

- 브랜치 이동
- git switch feature/login
- 브랜치 생성 + 이동
- git switch -c feature/signup

- 	checkout은 다기능이지만 복잡하고 실수 위험이 있음
- 	switch는 브랜치 전용 명령어라서 더 직관적이고 안전함
- 	최신 Git 환경에서는 switch 사용을 권장

# 2025-09-10 강의

## 프로젝트 구성
- 1. 컴포넌트 계층 (Component Hierarchy)
- Next.js는 특정 파일의 컴포넌트를 정해진 계층 구조로 렌더링합니다:

- layout.js → 공통 레이아웃
- template.js → 재렌더링 레이아웃
- error.js → React 에러 경계
- loading.js → React suspense 경계 (로딩 UI)
- not-found.js → 404 페이지
- page.js 또는 중첩된 layout.js → 실제 페이지 콘텐츠
- 중첩 라우트: 자식 라우트의 컴포넌트는 부모 레이아웃 안에 재귀적으로 렌더링됨.

## 2. Colocation (파일 동위 배치)
- app 디렉토리 안에서 폴더 구조 = 라우트 구조
- 공개 라우트 조건: page.js 또는 route.js 존재 시만 접근 가능
- 장점: route segment 안에 관련 파일을 안전하게 배치 가능 (라우트로 자동 노출되지 않음)
- 선택 사항: app 밖에 프로젝트 파일을 둬도 됨

## 3. Private 폴더
- _folderName으로 폴더 이름 시작 → 라우팅 제외

- 용도:UI 로직과 라우팅 로직 분리
- 내부 파일 일관성 유지
- 코드 에디터에서 정리/그룹화
- 미래 Next.js 파일 규칙 충돌 방지
- 참고:앱 밖에서도 _ 접두사로 "비공개" 표시 가능
- URL 세그먼트 시작 시 %5F 사용 가능 (%5FfolderName)

# 2025-09-03 강의

## 자동 생성되는 항목
 - 강의에서는 프로젝트를 자동으로 생성해서 사용
 - 다음은 프로젝트를 자동 생성할 때 자동으로 생성되는 항목이다.
 
 ## Core Web Vitals
  - LCP : 뷰포트 내에서 가장 큰 페이지 요소를 표시하는 데 걸리는 시간
  - FID : 사용자가 웹페이지와 상호작용을 시도하는 첫 번째 순간부터 웹페이지가 응답하는 시간.
  - CLS : 방문자에게 콘텐츠가 얼마나 불안정한 지 측정한 값이다. 페이지에서 갑자기 발생하는 레이아웃의 변경이 얼마나 일어나는지를 측정한다.

## alias 문자 및 경로
 - alias 문자를 선택하면 tsconfig.js 에 자동으로 저장 된다.

## HaRrd link vs Symbolic link(soft link)
 - pnpm의 특징 중에 하드 링크를 사용해서 디스크 공간을 효율적으로 사용할 수 있다고 한다. 탐색기에서 npm과 pnpm 프로젝트 node_module의 용량을 확인

 ## 하드 링크(Hard link)
  - 우리가 "파일"이라고 부르는 것은 두 부분으로 나뉘어 있다.
  1.Directory Enty : 파일 이름과 해당 inode 번호를 매길 정보가 있는 특수한 파일.
  2. inode : 파일 또는 디렉토리에 대한 모든 메타데이터를 저장하는 구조체 (권한,소유자,크기,데이터 블록,위치 등)








