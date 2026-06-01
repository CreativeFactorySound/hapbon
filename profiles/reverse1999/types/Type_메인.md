# Type_메인 — 리버스:1999 전용 (타인의 슬픔 형태)

> base: `profiles/default/types/Type_메인.md`

---

## 대상 파일

- `타인의 슬픔 X.X차...` — 메인 스토리 대본 (행 수 많음, 1000~2000행)
- `올로그 X.X차...` — 파트별 요약/부속 대본 (행 수 적음, 50~150행)

---

## 헤더 구조

```
[0]大纲简述  [1]调整日期  [2]调整类型  [3]序号  [4]步骤
[5]配音对象  [6]KR(캐릭터명)  [7]对象  [8]KR(직책)
[9]对话文本  [10]KR(대사)  ...  [N]配音备注  [N+1]KR(감정)  [N+2]BGM  [N+3]语音命名
```

헤더 행: row1 내외 (row0은 PART 설명 행)

---

## 컬럼 매핑

```python
cls = {
    "header_row": 1,          # PART 설명 행 제외
    "col_step_type": 4,       # 步骤
    "col_char_cn": 5,         # 配音对象
    "col_char_rec": 6,        # KR (캐릭터명)
    # col[7] 对象, col[8] KR(직책) → 매핑 제외
    "col_dialogue_cn": 9,     # 对话文本
    "col_dialogue_rec": 10,   # KR (대사) ← 핵심
    "col_emotion_cn": N,      # 配音备注
    "col_emotion_rec": N+1,   # KR (감정)
    "col_filename": N+3,      # 语音命名 (가장 오른쪽)
    "skip_step_values": ["画面", "特效"],
}
```

> 실제 열 번호는 차수마다 다를 수 있어 Gemini가 동적으로 탐지.

---

## 행 처리 규칙

### 스킵 행
| 조건 | 처리 |
|------|------|
| 步骤 = `画面` 또는 `特效` | skip_step_values → 스킵 |
| 配音备注/语音命名에 `无需录制` 포함 | _SKIP_ROW_KEYWORDS → 스킵 |
| KR 대사에 `더빙 불필요` 포함 | _SKIP_ROW_KEYWORDS → 스킵 |
| 완전 빈 행 | 스킵 |

### 포함 행
| 조건 | 처리 |
|------|------|
| 步骤 = `旁白` | 캐릭터명 = `내레이션` 으로 정규화 |
| 步骤 = `头像对话`, `spine对话` | 정상 포함 |
| 캐릭터명이 `???` | processor가 _valid_char()로 필터 |

---

## 감정 표시

- `[功能]` 접두어 OFF (profile: `functional_emotion_prefix: false`)
- `emotion = emotion_rec or emotion_cn or ""`
- KR 감정이 있으면 KR만 표시, 없으면 CN 감정으로 폴백

---

## 옵티컬

- optical=EN → 영어 대사 열 (없으면 dialogue_cn로 폴백)
- 리버스1999 메인 대본은 EN 열이 따로 없는 경우가 많음 → `optlical(원문)` 에 CN 대사 표시
