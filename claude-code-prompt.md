# Claude Code에 붙여넣을 프롬프트 (jjsong-model)

사용 방법
1. 프로젝트 폴더에 `CLAUDE.md`를 둡니다.
2. 샘플 이미지를 `reference/magazine-sample.png`로 저장합니다.
3. `claude` 실행 후 Shift+Tab으로 Plan 모드를 켜고, 아래 코드블록 내용을 붙여넣습니다.
4. 계획을 확인하고 승인하면 코딩이 시작됩니다.

---

```text
현재 폴더(jjsong-model)에 시니어 모델 "Jeongjae Song"의 포트폴리오 웹사이트를 만들어줘.
CLAUDE.md의 규칙을 따르고, index.html 파일 하나에 HTML/CSS/JS를 모두 넣어줘.
레이아웃 참고용 이미지는 reference/magazine-sample.png 에 있으니 먼저 확인해줘.
먼저 구현 계획을 보여주고, 내가 승인하면 코딩해줘.

[디자인 컨셉]
- 하이엔드 패션 매거진(Vogue) 스타일, 넓은 여백, 미니멀하고 세련되게
- 전체 분위기: 쾌활하고 밝고 따뜻한 느낌의 시니어 모델. 고급스러운 미니멀함은 유지하되
  차갑거나 무겁지 않게, 환하고 생기 있게 표현해줘
- 배경 #FFFFFF, 텍스트 #333333
- 제목: Playfair Display (Google Fonts), 본문: 깔끔한 sans-serif (Pretendard 또는 Noto Sans KR)
- 포인트 컬러 #E07A5F (따뜻한 코랄)를 가는 구분선, 버튼, 호버에만 사용
- 섹션 진입 시 부드러운 페이드인 (IntersectionObserver, 0.8초), 호버 시 살짝 확대(1.03배)
- 애니메이션은 부드럽고 경쾌하게

[이미지 규칙]
- 모든 이미지는 images/ 폴더의 상대경로 사용:
  hero.jpg, profile.jpg, look1.jpg ~ look6.jpg
- 파일이 아직 없으므로 이미지 로드 실패 시 연한 회색(#EEE) 박스에 파일명을
  표시하는 placeholder로 대체되게 해줘 (onerror 처리)
- 모든 img에 alt 텍스트, 첫 화면 외 이미지는 loading="lazy"

[섹션 구성]
1. Hero
 - 100vh 세로형 대표 사진 배경 (object-fit: cover, 얼굴이 잘리지 않게 object-position 조정)
 - 중앙에 'Jeongjae Song'을 잡지 표지 타이틀처럼 아주 크고 우아하게
   (흰색, 글자 가독성을 위한 은은한 어두운 그라데이션 오버레이)
 - 그 아래 작고 간결하게 'Senior Model' (넓은 자간, 대문자)
 - 그 아래 이탤릭 Playfair Display로 작은 한 줄 소개 (CONFIG.tagline 사용)

2. Profile
 - 왼쪽: 세로형 흑백 프로필 사진 1장 (CSS grayscale)
 - 오른쪽: 아래 딱 세 줄만, 타이포그래피 포스터처럼 여백을 살려 배치
   (라벨은 작은 대문자 sans-serif + 넓은 자간, 값은 큰 Playfair Display)
     Height — 160cm
     Size — M (55)
     Shoe — 235mm
 - 가슴·허리·엉덩이, 몸무게 등 다른 정보는 절대 넣지 말 것

3. Lookbook
 - 제목 'Lookbook', 사진 6장
 - 참고 이미지처럼 높이가 서로 다른 비대칭 그리드 (세로형 큰 사진 1장 + 중간·작은 사진 조합)
 - 사진 사이 간격은 넉넉하게 (데스크톱 약 40px), 미술관 같은 느낌
 - 사진 클릭 시 라이트박스로 크게 보기, ESC 또는 바깥 클릭으로 닫기

4. Contact
 - 제목 'Contact', 아래에 짧은 문구: "Let's work together"
 - 버튼 2개: [Email] [Call] — 각각 mailto:, tel: 링크
 - 이메일 주소와 전화번호는 HTML 본문에 평문으로 쓰지 말고, JS에서 문자열을 나눠 조립해서
   봇이 HTML에서 바로 긁기 어렵게 해줘
 - 데스크톱에서는 버튼 옆에 이메일 주소만 작게 텍스트로 표시 (전화번호는 화면에 표시하지 않음)
 - CONFIG.phone이 빈 문자열이면 Call 버튼을 숨겨줘
 - 아래 CONFIG 객체를 <script> 최상단에 두고 한 곳만 수정하면 되게 해줘

const CONFIG = {
  name: "Jeongjae Song",
  nameKo: "송정재",   // 한글 이름이 다르면 수정
  tagline: "Bright, warm and full of life",
  email: "sjj0119@naver.com",
  phone: "010-2105-4031"   // 비우면 Call 버튼 숨김
};

[반응형]
- 768px 이하: 모든 사진과 글자가 세로 한 열로 자연스럽게 배치
- Hero 타이틀은 clamp()로 화면 폭에 맞게 크기 조절
- Profile은 사진 위, 정보 아래로 쌓기. Lookbook은 1열

[기타]
- <title>: Jeongjae Song — Senior Model
- 메타 description, Open Graph 태그(og:title, og:description, og:image=images/hero.jpg) 포함
- og:description은 "Jeongjae Song — Senior Model" 정도로만 하고 연락처는 넣지 말 것
- <meta name="robots" content="noindex, nofollow"> 포함 (검색 노출 방지, 나중에 제거할 수 있게 주석 표시)
- 이름·이메일·수치처럼 내가 수정할 값은 파일 상단 주석으로 위치를 표시
- 완료 후 수정이 필요한 위치 목록과 로컬 미리보기 방법을 알려줘
```
