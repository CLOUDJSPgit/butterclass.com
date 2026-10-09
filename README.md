# 더버터 the BUTTER — butterclass.com

더버터(the BUTTER) 회사 소개 홈페이지. GitHub Pages로 배포한다.

## 파일 구성

| 파일 | 역할 |
|---|---|
| `index.html` | 홈페이지 본문(영문 기본, 한국어 전환 버튼). 브라우저가 한국어면 한국어로 열린다. `?lang=ko`, `?lang=en`으로 강제 지정 가능 |
| `404.html` | 없는 주소로 들어왔을 때 보이는 페이지 |
| `CNAME` | GitHub Pages 맞춤 도메인(`butterclass.com`) |
| `.nojekyll` | GitHub의 Jekyll 변환을 끈다 |
| `favicon-16.png`, `favicon-32.png`, `favicon.ico`, `apple-touch-icon.png` | 브라우저 탭·홈 화면 아이콘 (원본 버터 이미지 기반) |
| `img/` | 히어로 버터 이미지(`butter-drip.webp`), 헤더 로고(`logo-butter.webp`) |
| `fonts/` | 자체 호스팅 웹폰트(Archivo, Source Serif 4)와 SIL OFL 라이선스 |
| `robots.txt`, `sitemap.xml` | 검색엔진용 |

## 배포 순서

### 1. GitHub 저장소 만들기
1. github.com 로그인 → 오른쪽 위 `+` → **New repository**
2. Repository name: `butterclass.com` (아무 이름이나 가능)
3. **Public** 선택 (무료 계정은 공개 저장소에서만 Pages 사용 가능)
4. README 추가 체크는 하지 않고 **Create repository**

### 2. 파일 올리기
- 웹에서: 저장소 첫 화면의 **uploading an existing file** → 이 폴더 안의 파일과 `fonts` 폴더를 통째로 끌어다 놓기 → **Commit changes**
  - 주의: `.nojekyll`처럼 점으로 시작하는 파일은 끌어다 놓기에서 빠질 수 있다. 빠지면 **Add file → Create new file**로 이름만 `.nojekyll`로 만들어 커밋한다(내용은 비워 둔다).
- 터미널에서:
  ```bash
  git init && git add -A && git commit -m "the BUTTER homepage"
  git branch -M main
  git remote add origin https://github.com/<계정>/butterclass.com.git
  git push -u origin main
  ```

### 3. Pages 켜기
1. 저장소 **Settings → Pages**
2. Source: **Deploy from a branch** → Branch: `main`, 폴더 `/ (root)` → **Save**
3. Custom domain에 `butterclass.com`이 들어가 있는지 확인(`CNAME` 파일 덕에 자동으로 채워진다). 비어 있으면 입력하고 **Save**

### 4. 도메인 소유 인증(권장)
- GitHub 오른쪽 위 프로필 → **Settings → Pages → Add a domain** → `butterclass.com` 입력
- GitHub가 알려 주는 TXT 레코드(`_github-pages-challenge-<계정>.butterclass.com`)를 DNS에 추가 → **Verify**
- 남이 이 도메인을 자기 저장소에 붙이는 것을 막아 준다.

### 5. DNS 레코드 추가 (도메인을 산 곳의 DNS 관리 화면)
기존 Google Workspace 메일 레코드(MX, SPF용 TXT, DKIM용 TXT)는 **그대로 둔다.** 아래 레코드만 추가한다.

| 유형 | 호스트 | 값 |
|---|---|---|
| A | `@` | 185.199.108.153 |
| A | `@` | 185.199.109.153 |
| A | `@` | 185.199.110.153 |
| A | `@` | 185.199.111.153 |
| AAAA | `@` | 2606:50c0:8000::153 |
| AAAA | `@` | 2606:50c0:8001::153 |
| AAAA | `@` | 2606:50c0:8002::153 |
| AAAA | `@` | 2606:50c0:8003::153 |
| CNAME | `www` | `<계정>.github.io` (저장소 이름은 붙이지 않는다) |

- `@`에 이미 다른 A 레코드(도메인 업체의 주차 페이지 등)가 있으면 지운다.
- `*` 같은 와일드카드 레코드는 만들지 않는다.
- Cloudflare에서 관리한다면 처음에는 프록시를 끈 상태(회색 구름, DNS only)로 둔다. HTTPS 인증서가 발급된 뒤에 켜도 된다.

### 6. HTTPS
- DNS가 반영되면(보통 수십 분, 길면 24시간) **Settings → Pages → Enforce HTTPS**를 체크한다.

## 수정할 곳

- **연락 메일**: `contact@butterclass.com`으로 넣어 두었다. Google Workspace 관리 콘솔에서 이 주소를 실제 계정이나 별칭(alias)으로 만들어야 메일을 받는다. 다른 주소를 쓰려면 `index.html`에서 `contact@butterclass.com`을 모두 바꾼다(7곳).
- **회사 정보(하단)**: 사업자등록 후 `index.html` 맨 아래 `<!-- 사업자등록 후 ... -->` 주석을 풀고 대표, 사업자등록번호를 채운다. 주소(성심관 217호)는 이미 들어가 있으며, 사업자등록증 주소와 같아야 한다.
- **문구**: 영문은 `<span lang="en">`, 한국어는 `<span lang="ko">` 안에 짝으로 들어 있다. 한쪽을 고치면 다른 쪽도 함께 고친다.

## 출처
- GitHub Pages 맞춤 도메인 공식 문서: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
