# 인수인계 — claude.ai 채팅 → Claude Code (2026-10-23)

## 1. 지금까지 한 일
| 순서 | 결과물 | 상태 |
| --- | --- | --- |
| 1 | PRD 작성 (`docs/PRD.md`, 원본은 claude.ai Doc) | 완료 |
| 2 | 웹 시안 `index.html` — 화면 7개, 결재란 진행판, 승인·잠금·변경요청, 검증 대시보드, 미리보기·의견 | 완료 (샘플 데이터) |
| 3 | OneFinger 디자인 적용, 화이트 톤 고정 | 완료 |
| 4 | P1 공고문 분석 실제 동작 (PDF·HWPX·DOCX·TXT → 요구사항·작성지시·감점/실격·사업개요, trace.csv·ins.csv 내려받기) | 완료. PDF·DOCX 검증, HWPX는 실제 파일로 미검증 |
| 5 | GitHub 저장소 생성 `yangyoungsun-rgb/proposal-workroom` (Private, main) | **비어 있음 — 아직 push 안 됨** |
| 6 | Vercel 계정 `yangyoungsun-3462` ↔ GitHub 연결 | Vercel이 저장소를 볼 수 있음. 프로젝트는 아직 없음 |

## 2. 막혔던 것 (이유)
- claude.ai 채팅에는 GitHub MCP가 없어 push 불가.
- claude.ai의 Vercel 연결은 읽기 권한만 있어 프로젝트 생성·배포가 403으로 거절됨.
- 그래서 Claude Code(로컬 git·CLI 사용 가능)로 넘김.

## 3. 다음 할 일 (순서대로)
1. **GitHub push**
   - `gh auth status` 또는 `git ls-remote https://github.com/yangyoungsun-rgb/proposal-workroom.git` 로 로그인 확인. 안 되어 있으면 사용자에게 `gh auth login` 을 직접 하도록 안내(토큰을 대신 입력하지 않는다).
   - 이 폴더에는 커밋 2건이 이미 있다(임시 작성자 noreply@example.com). 사용자의 git 이름·이메일 설정을 확인한 뒤 두 커밋의 작성자를 바꾸고 push:
     `git rebase --root --exec 'git commit --amend --no-edit --reset-author'` → `git remote add origin https://github.com/yangyoungsun-rgb/proposal-workroom.git` → 사용자 확인 후 `git push -u origin main`
   - GitHub 웹에서 이미 파일을 올렸다면(README 자동 생성 포함) `git pull --rebase origin main` 후 push. `--force` 는 사용자 확인 없이 쓰지 않는다.
2. **Vercel 배포** (둘 중 하나, 사용자에게 고르게 함)
   - A. Vercel 웹: Add New → Project → proposal-workroom Import → Deploy (빌드 설정 없음, 정적 파일)
   - B. CLI: 사용자가 `npx vercel login` 을 직접 → `npx vercel link` → `npx vercel --prod`
   - 배포 후 Deployment Protection(접근 보호) 켤지 사용자에게 확인.
3. **배포 확인**: 배포 주소 열기 → 홈 화면, 공고문 업로드(samples PDF) → 요구사항 13건·작성지시 21건 나오는지.
4. **이후 개발** (`docs/PRD.md` 10장 출시 단계 기준)
   - MVP: 사업·단계·승인·의견을 서버에 저장(현재는 새로고침하면 초기화), 파일 버전 저장, 실제 검증 도구(scan_text·consistency_check 등)를 서버 실행기에서 돌리기.
   - 열린 질문(사내 구축 vs 클라우드, Claude 연동 방식, 협력사 계정, 감사 기록 보관 기간)은 사용자 결정 필요.

## 4. 참고
- 사용자: 양영선 (핑거 D.A.S 본부 사업팀). 설명은 쉬운 말로.
- 스킬 원본(proposal-full-pipeline)은 사내 자산이라 이 저장소에 넣지 않음.
- claude.ai PRD 원본: https://claude.ai/artifact/7pepscJuuZJFiRcBMMQuJk
