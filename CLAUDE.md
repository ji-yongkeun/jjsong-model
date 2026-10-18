# jjsong-model

시니어 모델 Jeongjae Song의 포트폴리오 웹사이트 (정적 사이트, Vercel 배포).

## 프로젝트 규칙
- 프로젝트명: jjsong-model (GitHub 저장소, Vercel 프로젝트명 동일)
- 파일 구조: index.html 한 개(HTML/CSS/JS 모두 포함) + images/ 폴더
- 빌드 도구, 프레임워크, npm 의존성 사용 금지 (Vercel 정적 배포)
- 배경 #FFFFFF, 텍스트 #333333, 포인트 컬러 #E07A5F (가는 선, 버튼, 호버에만)
- 제목 글꼴 Playfair Display, 본문 글꼴 Pretendard 또는 Noto Sans KR
- 전체 분위기: 하이엔드 매거진 미니멀 + 쾌활하고 밝고 따뜻한 느낌
- 모든 이미지 경로는 images/ 기준 상대경로, alt 텍스트 필수
- 이미지 파일이 없어도 깨지지 않게 회색 placeholder 처리 (onerror)
- 수정할 때마다 반응형(모바일 768px 이하)을 항상 확인
- Profile에는 Height, Size, Shoe 세 가지만 표시 (가슴·허리·엉덩이, 몸무게 등은 넣지 않음)
- 개인 연락처(이메일/전화)는 CONFIG 한 곳에서만 관리하고, HTML 본문·메타태그에 평문으로 쓰지 않는다
- 사이트는 기본적으로 noindex (검색 노출 방지). 제거할 때는 주석 위치를 안내한다
- 참고 레이아웃: reference/magazine-sample.png (비대칭 매거진 콜라주 느낌)
