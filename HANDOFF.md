# 합본 제작 자동화 — 새 대화 인계 문서

새 대화창 시작 시 이 파일과 함께 필요한 MD 파일들을 첨부하면 이전 작업을 이어서 진행할 수 있다.

---

## 첨부할 파일 목록

필수:
- `PROJECT.md`
- `functions/classification_guide.md`
- `functions/column_inference.md`

작업 내용에 따라 추가:
- `functions/type_management.md` (타입 추가/수정 작업 시)
- `output/template_spec.md` (합본 조립 작업 시)
- `types/Type_XXX.md` (해당 타입 처리 작업 시)

---

## 프로젝트 현황

### 확정된 구조

```
/합본자동화/
├── PROJECT.md
├── HANDOFF.md
├── functions/
│   ├── classification_guide.md
│   ├── column_inference.md
│   └── type_management.md
├── types/
│   ├── Type_메인.md
│   ├── Type_PV.md
│   ├── Type_전투.md
│   ├── Type_캐릭터음성.md
│   ├── Type_짧은음성.md
│   ├── Type_무한대.md
│   └── Type_명방캐릭터.md
└── output/
    └── template_spec.md
```

### 진행 상황

- [x] 프로젝트 아키텍처 확정
- [x] 타입 7종 도출 및 확정
- [x] PROJECT.md 작성 (Gemini 2.5 Flash, 비용 추정 포함)
- [x] functions/classification_guide.md 작성 (헤더 탐색 규칙 + 분류 우선순위 포함)
- [x] functions/column_inference.md 작성
- [x] functions/type_management.md 작성 (골격)
- [x] output/template_spec.md 작성
- [x] types/Type_메인.md 작성
- [x] types/Type_PV.md 작성
- [x] types/Type_전투.md 작성
- [x] types/Type_캐릭터음성.md 작성
- [x] types/Type_짧은음성.md 작성
- [x] types/Type_명방캐릭터.md 작성
- [x] types/Type_무한대.md 작성 (초안 — 샘플 합본 검토 후 보완 필요)
- [x] 타입 분류 시뮬레이션 100% 통과 (34/34 시트)
- [ ] Type_무한대.md 최종 보완 (샘플 합본 검토 후)
- [ ] Python 코드 작성
- [ ] 실제 파일로 테스트
- [ ] PyInstaller .exe 패키징

---

## 분석 완료된 파일 목록

### 리버스1999 (3.5차수)
| 파일명 | 타입 |
|--------|------|
| 3_5_메인스토리_活动3_5-1920-_绿松石蛇俱乐部__20260304.xlsx | Type_메인 |
| 3_5_스킨_음성.xlsx | Type_캐릭터음성 |
| 보스_및_전투_3_5boss战斗对话_普通战中对话_20260303.xlsx | Type_전투 |
| 로렌츠_버터플라이_3_5洛伦兹蝴蝶角色语音_251230.xlsx | Type_캐릭터음성 |
| 로렌츠_버터플라이_3_5洛伦兹蝴蝶角色PV_251230.xlsx | Type_PV |
| 로렌츠_버터플라이_스킬_3_5洛伦兹蝴蝶技能PV_250120.xlsx | Type_PV |
| 로렌츠_버터플라이_3_5洛伦兹蝴蝶角色故事_260309.xlsx | Type_메인(终稿) + Type_짧은음성(짧은 음성) |

### 프로젝트AP
| 파일명 | 타입 |
|--------|------|
| 챕터1_파트3_v1_01.xlsx | Type_메인 (파트3, 파트3_하우징 부분) / 나머지 스킵 |

### 아크나이츠(명일방주)
| 파일명 | 타입 |
|--------|------|
| char_1050_첸SP.xlsx | Type_명방캐릭터(설정) + Type_캐릭터음성(대사) + Type_PV(PV) |
| char_2027_왕.xlsx | Type_명방캐릭터(설정) + Type_캐릭터음성(대사) + Type_PV(PV) |
| char_4056_티티.xlsx | Type_명방캐릭터(설정) + Type_캐릭터음성(대사) + Type_PV(PV_티티→티티_PV) |
| char_2023_링_스킨.xlsx | Type_명방캐릭터(설정) + Type_캐릭터음성(대사) |

### 레벨인피니티
| 파일명 | 타입 |
|--------|------|
| 260203_L50_KR_recording_requirements_.xlsx | Type_무한대 |

### Regolith
| 파일명 | 타입 |
|--------|------|
| Regolith_REGOLITH_VO_-__OUTSOURCE__ADR_1_Korean_2025-07-28_15-41-52.xlsx | Type_메인 |

---

## 다음 할 일

1. Type_무한대.md 최종 보완 — 샘플 합본 파일 받아서 검토
2. Python 코드 작성 시작
3. 실제 파일 통합 테스트
