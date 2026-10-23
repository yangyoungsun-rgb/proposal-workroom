# CLAUDE.md — 제안 작업실 (proposal-workroom)

이 파일은 Claude Code가 이 저장소에서 작업을 시작할 때 먼저 읽는 안내서입니다.
처음 들어왔다면 `docs/HANDOFF.md`(지금까지의 경과와 다음 할 일)를 이어서 읽으세요.

## 무엇인가
공공·금융 제안서 작업을 proposal-full-pipeline 스킬의 P1~P8 단계로 관리하는 웹 서비스의 **시안**.
요구사항 전체는 `docs/PRD.md`.

## 구조
- `index.html` — 화면 + 로직 전부 들어 있는 단일 파일. 빌드 도구 없음. 브라우저로 바로 연다.
- `samples/샘플_제안요청서.pdf` — 가상 RFP(시험용). 실제 고객 자료 아님.
- `docs/PRD.md` — 제품 요구사항, `docs/HANDOFF.md` — 인수인계.

## index.html 안의 구역
- `<style>`: OneFinger 스타일(남색 사이드바, 흰 카드, Pretendard). **화이트 톤 고정**(다크 모드 넣지 말 것).
- `PHASES`, `S`(상태), `V.*`(화면 7개: list·board·work·preview·verify·inbox·settings).
- "RFP 분석 엔진" 구역: 스킬의 `trace_matrix.py extract`, `instructions.py extract` 규칙을 JS로 옮긴 것.
  PDF(pdf.js)·HWPX(JSZip)·DOCX(mammoth)·TXT 판독. 결과는 `S.an[사업ID]`.
- P1 분석만 실제 동작, 나머지 화면은 샘플 데이터.

## 지켜야 할 것
- 화면 문구는 쉬운 우리말. "핫버튼"이라는 말은 쓰지 않는다("발주사가 제일 걱정하는 것").
- 새로 만드는 엑셀 파일 기본 글꼴은 "맑은 고딕".
- 외부 스크립트는 cdnjs 고정 버전만(pdf.js 3.11.174, jszip 3.10.1, mammoth 1.6.0). 버전 올릴 때는 공개 후 2주 지난 것.
- 업로드 파일은 브라우저 안에서만 처리. 외부로 보내는 코드 추가 금지.
- 실제 고객 공고문·제안서·평가본을 커밋하지 않는다. 저장소는 Private 유지.
- 토큰·비밀번호를 코드나 커밋에 넣지 않는다. GitHub/Vercel 로그인은 사용자가 직접 한다.
- push·배포·저장소 설정 변경 전에는 사용자에게 확인을 받는다.
- 추출 규칙을 바꾸면 스킬 원본 규칙과 결과를 비교한다(샘플 RFP 기준 요구사항 13건, 작성 지시 21건, 명칭 상이 2건 SER-002·SFR-002, ID 확인 1건 ZZZ-901, 감점·실격 5건).

## 빠른 확인
```bash
python3 -m http.server 8000   # http://localhost:8000 열고 '공고문 올려서 시작' → samples PDF 업로드
```
