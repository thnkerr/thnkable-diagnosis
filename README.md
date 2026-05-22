# 씽커블 학습 기질 진단 결과지

씽커블(Thnkable) 부모용 학습 기질 진단 도구의 정적 사이트입니다.
20문항 진단 → 4기질 × 3시기 = 12조합 중 하나의 결과지를 보여주고,
학부모 가이드 PDF 다운로드와 1:1 상담 신청으로 이어집니다.

## 파일 구조

```
.
├── index.html              # 진단 페이지 (인트로 + 20문항)
├── result.html             # 결과지 (9블록 + 동적 라우팅)
├── data/
│   └── results.json        # 12조합 카피 (운영팀 직접 편집)
├── assets/
│   ├── logo.png            # 다크그린+오렌지 (밝은 배경용)
│   └── logo-white.png      # 흰+오렌지 (다크그린 배경용)
└── pdfs/
    ├── parent_guide_5-7.pdf
    ├── parent_guide_1-3.pdf
    └── parent_guide_4-6.pdf
```

## 결과지 라우팅

```
/result.html?key={temperament}_{ageStage}&x={number}&y={number}
```

- `temperament`: `tooMuchTalker` · `proSotongRo` · `powerDeokhu` · `powerJ`
- `ageStage`: `5-7` · `1-3` · `4-6`
- `x`, `y`: -50 ~ +50 (기질 지도 좌표)

예: `/result.html?key=tooMuchTalker_5-7&x=30&y=25`

## 카피 운영

`data/results.json`을 GitHub에서 직접 편집·푸시하면 자동 재배포됩니다.
각 조합은 9블록 구조(상단카드 / 일상장면 / 답답함 / 기질지도 / 4가지모습 /
안 통하는 말·통하는 말 / 부모의 자리 / 이번 주 실천 / CTA).

## CTA

- **학부모 가이드 다운받기**: 시기별 PDF (`pdfs/parent_guide_{ageStage}.pdf`) 직접 다운로드
- **상담 신청하기**: Google Forms 새 탭 — `https://forms.gle/qgrBbRmctubvr6Bp7`

## 분석 (GA4)

`G-XXXXXXXXXX` 측정 ID를 `result.html` 상단에서 교체하면 활성화됩니다.
추적 이벤트: `result_view`, `scroll_block5_behaviors`, `scroll_block8_practice`,
`cta_pdf_download`, `cta_consult_click`, `share_image_save`, `share_native`, `share_link_copy`.

## 로컬 미리보기

```bash
python -m http.server 5173
```

또는 어떤 정적 파일 서버라도 OK.

## 배포

GitHub 저장소 연결 → Vercel · Cloudflare Pages 등에서 자동 빌드.
Framework Preset은 **Other / None** 선택 (정적 사이트, 빌드 명령 없음).
