# 프리셋 시스템

합본 자동화 도구는 프로젝트별 설정을 **프리셋(프로파일)** 으로 관리한다.
각 프리셋은 `hapbon-auto/profiles/<id>/` 폴더 + `hapbon/profiles/<id>/` 문서 폴더 한 쌍으로 구성.

---

## 프리셋 목록

| ID | 이름 | 녹음 | 옵티컬 | 탭명 방식 | 상태 |
|----|------|------|--------|-----------|------|
| `default` | Default (범용) | KR | EN | standard | ✅ 사용 가능 |
| `reverse1999` | 리버스1999 | KR | EN | reverse1999 | ✅ 사용 가능 |
| `muhandae` | 무한대 | KR | CN | original | 🚧 개발 예정 |

---

## 프리셋 구조

### 코드 (hapbon-auto)
```
profiles/
  <id>/
    profile.json         ← 기본 설정 (녹음언어, 탭명방식 등)
    classify_system.txt  ← Gemini 분류 프롬프트 (프리셋 전용)
```

### 문서 (hapbon)
```
profiles/
  <id>/
    README.md            ← 프리셋 개요 및 핵심 특이사항
    functions/
      column_inference.md    ← 컬럼 탐지 규칙
      classification_guide.md ← 타입 분류 가이드
    types/
      Type_메인.md        ← 타입별 처리 규칙
      Type_캐릭터음성.md
      Type_전투.md
      Type_PV.md
      ...
    output/
      template_spec.md   ← 합본 출력 규칙, 탭명 예시
```

---

## 실행 방법

### 인터랙티브 모드 (권장)
```bash
python main.py --source <폴더> --output <경로.xlsx>
```

실행하면 프리셋 선택 메뉴가 표시됨:
```
=======================================================
  합본 자동화 — 프로젝트 선택
=======================================================
  1. Default (범용)
  2. 리버스1999 (Reverse: 1999)
  3. 무한대 (기획 중) ⚠ (개발 예정)
=======================================================
선택 (번호): 2

  프로파일: 리버스1999 (Reverse: 1999)
프로젝트명 (Enter = '리버스1999'): 리버스1999
차수 (예: 3.7차, Enter = 생략): 3.7차
녹음 언어 KR/JP/EN (Enter = KR): 
옵티컬 언어 EN/CN/NONE (Enter = EN): 
```

### CLI 완전 지정 모드 (자동화용)
```bash
python main.py --source <폴더> --output <경로.xlsx> --profile reverse1999 --project "리버스1999" --round "3.7차" --optical EN --record KR
```

---

## profile.json 설정 항목

```json
{
  "id": "...",                        // 고유 ID
  "display_name": "...",              // 메뉴 표시명
  "description": "...",              // 설명
  "defaults": {
    "record": "KR",                   // 기본 녹음 언어
    "optical": "EN"                   // 기본 옵티컬 언어
  },
  "functional_emotion_prefix": true,  // [功能] 감정 접두어 on/off
  "tab_naming": "standard"           // 탭명 생성 방식
}
```

### tab_naming 옵션

| 값 | 설명 | 예시 |
|----|------|------|
| `standard` | 파일명/시트명 기반 | `이글_음성_` |
| `reverse1999` | `캐릭터명 (유형)` 형식 | `이글 (음성)`, `노티카 (스킨)` |
| `original` | 원본 시트명 그대로 유지 | `무한대 스크립트 ACT2` |

---

## 새 프리셋 추가 방법

**코드:**
1. `hapbon-auto/profiles/<id>/` 폴더 생성
2. `profile.json` 작성
3. `classify_system.txt` 작성 (가장 비슷한 기존 프리셋 복사 후 커스텀)
4. `profile.py`의 `_PROFILE_ORDER` 리스트에 추가
5. 필요 시 `profile.py`에 전용 `make_sheet_name_<id>()` 함수 추가
6. `main.py`의 `_resolve_sheet_name()`에 라우팅 추가

**문서:**
1. `hapbon/profiles/<id>/` 폴더 생성 (가장 비슷한 기존 프리셋 복사)
2. 각 문서를 프로젝트 특성에 맞게 커스터마이징
