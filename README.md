# matholic-site

MATHOLIC 팀이 만드는 여러 웹페이지를 한 저장소에서 관리하고, GitHub + Netlify로 자동 배포합니다.

## 사이트 구조

- 프로젝트마다 폴더를 하나씩 만들고, 그 안에 `index.html`을 둡니다.
  - 예: `dapunee/index.html` → 실제 주소는 `https://<사이트주소>.netlify.app/dapunee/`
- 루트(`index.html`)는 MATHOLIC 브랜드 소개 화면입니다. 프로젝트 목록은 여기에 넣지 않습니다(고객이 들어와도 다른 프로젝트가 보이면 안 되기 때문입니다).
- 전체 프로젝트 목록은 `success_team_list/index.html`에 따로 있고, 팀만 아는 `https://<사이트주소>.netlify.app/success_team_list/` 로 확인합니다. 이 주소는 고객에게 공유하지 마세요. 새 프로젝트를 추가하면 `success_team_list/index.html`에 링크를 한 줄 추가해주세요(루트 `index.html`은 건드리지 않습니다).
- (2026-08-28) `success_team_list/index.html`은 이제 브랜드 톤(다크 퍼플 그라데이션)에 맞춰 디자인되어 있고, 프로젝트/도구/튜토리얼 세 섹션으로 나뉩니다. 각 섹션의 목록은 파일 안 `<script>`의 `PROJECTS`, `TUTORIALS` 배열에 있으므로, 새 프로젝트나 튜토리얼을 추가할 때는 그 배열에 한 줄(`{ title, path }`)만 추가하면 됩니다. 튜토리얼 빌더가 만드는 페이지는 이제 `tutorials/<폴더이름>/index.html`처럼 `tutorials/` 하위에 모아서 저장하고, 목록 주소는 `/tutorials/<폴더이름>/`이 됩니다(일반 프로젝트처럼 저장소 루트에 바로 폴더를 만들지 않습니다). `TUTORIALS` 배열이 많아질 걸 감안해 검색창도 붙어 있습니다.
- GitHub 저장소(`successmatholic/my-site`)에 새 커밋이 올라가면 Netlify가 몇 초 안에 자동으로 재배포합니다. 사람이 Netlify를 직접 건드릴 일은 없습니다.

## 새 프로젝트 추가하는 법

### 방법 A — 클로드에게 요청 (추천)
자기 컴퓨터를 클로드(Cowork) 세션에 연결한 상태에서, "이 HTML 파일을 `프로젝트이름` 폴더로 배포해줘"라고 요청하면 클로드가 폴더 생성, 파일 저장, `success_team_list/index.html` 링크 추가, git commit/push까지 처리합니다.

### 방법 B — 직접 하기
1. `matholic-site` 폴더(저장소를 복제해 둔 로컬 폴더) 안에 새 폴더를 만들고 `index.html`을 저장합니다.
2. `success_team_list/index.html`의 목록(`<ul>` 안)에 새 프로젝트 링크를 한 줄 추가합니다. (루트 `index.html`은 그대로 둡니다.)
3. 터미널에서:
   ```
   git add -A
   git commit -m "Add 프로젝트이름"
   git push origin main
   ```

## 새 팀원 온보딩

1. **컴퓨터 연결**: 자기 Claude(Cowork) 세션에서 데스크톱 앱의 "Add folder"로 로컬 폴더를 하나 연결합니다(예: `matholic-site`).
2. **저장소 복제**: 클로드에게 "https://github.com/successmatholic/my-site 저장소를 이 폴더에 복제해줘"라고 요청합니다.
3. **GitHub 토큰**: 회사 비밀번호 관리 도구에 저장된 공용 토큰("my-site 자동배포용")을 확인합니다. 새로 만들 필요는 없습니다(공용 계정이라 팀 전체가 같은 토큰을 씁니다).
4. **git 인증 설정**: 클로드에게 "이 토큰으로 이 컴퓨터에서 push 인증을 설정해줘"라고 하면서 토큰을 알려줍니다(이 저장소에서만 쓰이고, 이 컴퓨터 로컬에만 저장됩니다). 커밋 작성자 이름/이메일도 본인 것으로 설정해달라고 하세요.
5. 이후로는 방법 A대로 "이 페이지 배포해줘"라고만 하면 자동으로 처리됩니다.

## 참고

- 토큰은 비밀번호와 동일하게 취급하세요. 대화 로그나 파일에 평문으로 남기지 마세요(회사 비밀번호 관리 도구에만 보관).
- 클로드가 클라우드에서 직접 GitHub/Netlify API를 호출하는 방식은 보안 제한으로 동작하지 않습니다. 반드시 "컴퓨터가 연결된 상태"에서 요청해야 자동 배포가 됩니다.
