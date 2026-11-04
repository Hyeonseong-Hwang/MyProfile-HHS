## 개인 소개 사이트

Hugo와 hugo-paper 테마로 만든 개인 소개 사이트입니다. 관심 분야와 활동(동아리 홈페이지 개선, 채팅 프로그램)을 소개합니다.

- **공개 사이트**: https://hyeonseong-hwang.github.io/MyProfile-HHS/
- **저장소**: https://github.com/Hyeonseong-Hwang/MyProfile-HHS
- **배포 방식**: `main` 브랜치에 push하면 GitHub Actions가 자동으로 빌드하고 GitHub Pages에 배포합니다.

## 사이트 구성

| 메뉴 / 화면 | 주소 | 원본 파일 |
|---|---|---|
| 홈 (프로필, 글 목록) | `/` | `site/content/_index.md`, `site/hugo.toml` |
| 소개 | `/about/` | `site/content/about.md` |
| 활동 › 홈페이지 만들기 | `/post/mkpage/` | `site/content/post/mkpage.md` |
| 활동 › 채팅 프로그램 | `/post/mkchat/` | `site/content/post/mkchat.md` |
| 연락 | `/contact/` | `site/content/contact.md` |
| 관심 분야 1 | `/post/myfirstinterest/` | `site/content/post/myfirstinterest.md` |
| 관심 분야 2 | `/post/mysecondinterest/` | `site/content/post/mysecondinterest.md` |
| 총정리 | `/post/summary/` | `site/content/post/summary.md` |

## 사용 도구와 버전

| 도구 | 버전 | 용도 |
|---|---|---|
| Hugo extended | 0.167.0 | 배포 빌드 (`.github/workflows/hugo-pages.yml`에 고정) |
| Hugo extended | 0.168.0 | 로컬 미리보기에서 동작 확인 (macOS, Homebrew 설치) |
| Git | 시스템 기본 | 버전 관리 |
| Python | 3.12 | 배포 워크플로의 빌드 보조 스크립트 실행 (GitHub Actions에서 자동 설치) |
| 수업 제공 스크립트 | `prepare_github_pages.py` 3.1 | 저장소 연결, `site/` 구성, 워크플로 생성 |

## 로컬에서 실행하기

### 1. Hugo 설치 (macOS)

```bash
brew install hugo
hugo version
```

Windows는 `winget install Hugo.Hugo.Extended`로 설치할 수 있습니다.

### 2. 저장소 받기

```bash
git clone https://github.com/Hyeonseong-Hwang/MyProfile-HHS.git
cd MyProfile-HHS
```

### 3. 미리보기 서버 실행

```bash
cd site
hugo server --config hugo.toml,pages.json --disableFastRender
```

브라우저에서 `http://localhost:1313/MyProfile-HHS/`를 엽니다. 파일을 저장하면 화면이 자동으로 새로고침됩니다. 서버는 `Ctrl + C`로 끕니다.

- `--config hugo.toml,pages.json`: 사이트 설정(`hugo.toml`)과 배포용 설정(`pages.json`)을 함께 읽습니다.
- `--disableFastRender`: 파일 이름 변경·삭제 후에도 화면이 정확히 다시 만들어지게 합니다.

### 4. 배포와 같은 방식으로 빌드만 해 보기

```bash
cd site
hugo --config hugo.toml,pages.json --destination /tmp/site-check --cleanDestinationDir
```

결과물은 저장소 밖(`/tmp/site-check`)에 만들어지므로 Git 기록에 영향을 주지 않습니다.
## 내용 수정 위치
바꾸고 싶은 것	수정할 파일
사이트 제목, 이름, 홈 소개 문구, 메뉴, GitHub·인스타그램 링크, 언어	site/hugo.toml
소개 페이지 (경력·학력)	site/content/about.md
연락처와 지도	site/content/contact.md
글 내용	site/content/post/*.md
이미지	site/static/images/ (글에서는 ../../images/파일이름으로 사용)
메뉴 드롭다운 모양과 동작	site/layouts/partials/header.html
홈 글 목록 카드 효과, 홈 소개 문구 링크 표시	site/layouts/_default/list.html

맨 위의 exampleSite/ 폴더와 site/themes/template/(테마 원본)은 수정하지 않습니다. 테마 화면을 바꿀 때는 site/layouts/에 같은 경로로 파일을 복사해 덮어씁니다.

## 수정 후 배포 확인 방법
수정한 파일만 골라서 커밋하고 main에 push합니다.
bash
   git add site/content/about.md
   git commit -m "소개 페이지 경력 내용 수정"
   git push origin main
GitHub 저장소의 Actions 탭에서 방금 커밋의 실행을 엽니다.
build와 deploy가 모두 초록 체크인지 확인합니다. 빨간 X면 실패한 단계를 열어 오류 내용을 확인합니다.
브라우저 시크릿 창에서 공개 사이트를 열어 변경 내용이 반영됐는지 확인합니다.

## 저장소에서 제외하는 파일

.gitignore로 아래 파일은 Git에 올리지 않습니다.

/site/public/, /public/: Hugo 빌드 결과물 (배포 때 Actions가 새로 만듦)
.DS_Store: macOS 시스템 파일
**/resources/_gen/, **/.hugo_build.lock, **/node_modules/: 빌드 도구의 임시 파일

## 출처와 이용 조건
자료	출처	이용 조건	사용 위치
hugo-paper 테마	https://github.com/nanxiaobei/hugo-paper (nanxiaobei)	MIT License, 원본 LICENSE 파일 유지	사이트 전체 디자인 (site/themes/template/)
Hugo	https://gohugo.io	Apache License 2.0	사이트 생성
지도	https://www.openstreetmap.org	© OpenStreetMap contributors, ODbL	연락 페이지 지도 (지도 안 출처 표시 유지)
배포 스크립트와 워크플로	수업 제공 (prepare_github_pages.py)	수업 자료	.github/, .github-pages.json, site/pages.json

사이트 맨 아래의 "powered by hugo", "hugo-paper" 링크는 테마 출처 고지이므로 유지합니다.

## 직접 제작 · 외부 자료 · AI 활용 구분
구분	내용
직접 제작	소개·관심 분야·활동 글의 내용, 프로필 및 활동 사진(직접 촬영·화면 캡처), 사이트 설정과 콘텐츠 구성, 화면·기능 점검
외부 자료	hugo-paper 테마, Hugo, OpenStreetMap 지도, 수업 제공 배포 스크립트,
AI 활용 (Claude)	Hugo 설정 방법과 배포 오류 원인 분석, 메뉴 드롭다운·글 카드 효과·소개 타임라인·연락 페이지의 HTML·CSS 코드 초안, 글 문장 다듬기

AI가 제안한 코드와 문장은 직접 적용해 본 뒤 로컬과 공개 사이트에서 동작을 확인하고, 맞지 않는 부분은 수정하거나 사용하지 않았습니다. 자세한 사례는 과제 보고서의 AI 활용 기록에 정리했습니다.