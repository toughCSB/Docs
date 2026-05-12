# Docs

`toughCSB/Docs`는 Obsidian의 [MarkTL HTML Exporter](https://github.com/reallygood83/marktl)로 만든 HTML 문서를 GitHub Pages에 공개하기 위한 게시용 저장소입니다.

Obsidian 노트는 MarkTL에서 HTML로 변환되고, 이 저장소의 `main` 브랜치에 업로드된 뒤 GitHub Pages URL로 공개됩니다. 댓글은 Giscus를 통해 GitHub Discussions에 저장합니다.

## 공개 주소

GitHub Pages가 활성화되면 기본 주소는 보통 아래 형태입니다.

```text
https://toughcsb.github.io/Docs
```

MarkTL의 `Publish path`를 `marktl`로 설정하면 공개 문서는 아래 경로에 생성됩니다.

```text
https://toughcsb.github.io/Docs/marktl/<slug>/
https://toughcsb.github.io/Docs/marktl/s/<short-id>/
```

MarkTL은 export 후 짧은 공유 링크를 기본으로 복사할 수 있습니다.

```text
https://toughcsb.github.io/Docs/marktl/s/<short-id>/
```

아카이브 홈과 인덱스도 함께 관리됩니다.

```text
https://toughcsb.github.io/Docs/marktl/
https://toughcsb.github.io/Docs/marktl/index.json
```

## GitHub Pages 설정

이 저장소에서 다음 설정을 사용합니다.

```text
Repository: toughCSB/Docs
Branch: main
Pages source: Deploy from a branch
Pages branch: main
Pages folder: /(root)
```

GitHub 저장소 화면에서 설정 위치는 다음과 같습니다.

```text
Settings -> Pages -> Build and deployment
```

## MarkTL 설치

Obsidian에서 BRAT를 통해 MarkTL을 설치합니다.

1. Obsidian `Settings -> Community plugins`에서 BRAT 설치 및 활성화
2. BRAT settings 열기
3. `Add Beta plugin` 선택
4. 아래 저장소 URL 입력

```text
https://github.com/reallygood83/marktl
```

5. Obsidian community plugin 목록에서 `MarkTL HTML Exporter` 활성화

## MarkTL 권장 설정

이 저장소에 발행할 때 MarkTL 설정값은 아래와 같습니다.

```text
Share target: GitHub Pages link
Preview/export: Trusted interactive preview
Reader feedback: Giscus GitHub comments
Copy share link by default: On
GitHub repository: toughCSB/Docs
GitHub branch: main
GitHub Pages base URL: https://toughcsb.github.io/Docs
Publish path: marktl
```

`Trusted interactive preview`를 사용해야 MarkTL의 인터랙티브 컨트롤과 Giscus 댓글 스크립트가 동작합니다. Sanitized export에서는 Giscus가 비활성화됩니다.

## GitHub 토큰

MarkTL이 이 저장소에 HTML 파일을 업로드하려면 fine-grained personal access token이 필요합니다.

권장 권한은 아래 하나뿐입니다.

```text
Repository access: Only select repositories
Selected repository: toughCSB/Docs
Repository permissions: Contents -> Read and write
```

토큰은 MarkTL 설정의 `GitHub token` 칸에만 입력합니다. README, 노트, 이슈, 채팅, 커밋에 토큰을 남기지 않습니다.

## Giscus 댓글 설정

MarkTL은 Giscus 기반 `Reader feedback` 섹션을 HTML 하단에 붙일 수 있습니다. 댓글과 reaction은 GitHub Discussions에 저장됩니다.

1. `toughCSB/Docs` 저장소에서 `Settings -> Features -> Discussions` 활성화
2. https://github.com/apps/giscus 에서 Giscus GitHub App을 이 저장소에 설치
3. https://giscus.app 에서 repository에 아래 값 입력

```text
toughCSB/Docs
```

4. Page ↔ Discussion mapping은 `pathname` 선택
5. Discussion category는 `General` 또는 `Announcements` 선택
6. 생성된 script block에서 아래 값을 MarkTL 설정으로 복사

```text
Giscus repository: toughCSB/Docs
Giscus repo ID: data-repo-id 값
Giscus category: General 또는 Announcements
Giscus category ID: data-category-id 값
Giscus mapping: pathname
Giscus theme: preferred_color_scheme
```

이미 발행한 HTML은 Giscus 설정을 바꿔도 자동으로 수정되지 않습니다. 설정을 바꾼 뒤에는 같은 노트를 다시 export해야 합니다.

## 테스트 절차

1. Obsidian에서 테스트 Markdown 노트 열기
2. MarkTL 명령 실행: `Export active note to HTML...`
3. Share target이 `GitHub Pages link`인지 확인
4. Export 실행
5. 결과 모달에서 아래 항목 확인

```text
Short public link
Archive link
Comment status
```

6. public link 열기
7. 페이지가 로드되는지 확인
8. `Sign in with GitHub` 버튼과 Giscus 댓글 박스가 보이는지 확인

GitHub Pages 첫 배포는 몇 분 걸릴 수 있습니다.

## 문제 해결

```text
BRAT 설치 실패
-> MarkTL 저장소 URL, BRAT 설치 상태, MarkTL manifest/release 파일 확인

Export 시 401 또는 403
-> GitHub token의 repository access와 Contents read/write 권한 확인

Export 성공 후 public link 404
-> GitHub Pages source, branch, base URL, Publish path 확인

/marktl/ 아카이브는 보이지만 특정 문서가 404
-> export 결과의 slug 또는 short-id 경로 확인

페이지는 보이지만 댓글이 없음
-> Giscus App 설치, Discussions 활성화, repo ID, category ID, Trusted preview/export 확인

Sign in with GitHub 버튼이 없음
-> Giscus script가 export HTML에 포함되지 않은 상태일 가능성이 높으므로 MarkTL Giscus 설정 후 재-export
```

## 참고

- MarkTL: https://github.com/reallygood83/marktl
- Giscus: https://giscus.app
- Giscus GitHub App: https://github.com/apps/giscus
- GitHub Pages settings: `Settings -> Pages`
