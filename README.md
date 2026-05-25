# Constitution KR

> 헌법재판소 결정례를 Git으로 관리합니다.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) [![data](https://img.shields.io/badge/data-Markdown-blue)](kr/) [![source](https://img.shields.io/badge/source-법제처_DRF_OpenAPI-orange)](https://open.law.go.kr)

헌법재판소가 선고한 **결정례** (위헌법률심판·헌법소원·권한쟁의·탄핵·정당해산) 를 Markdown + YAML frontmatter 로 변환하여 Git 저장소에서 관리합니다. 각 결정은 선고일자를 Git commit date 로 갖고, 사건명·심판유형·결정주문·이유를 메타·본문으로 보관합니다.

법령·행정규칙·판례·법령해석례에 이어, **헌법재판소 결정례**까지 Git 으로 추적해 헌법 적합성 판단의 흐름을 시각화합니다.

## 왜 필요한가?

헌법재판소 결정은 **법령의 유·무효를 결정하는 최상위 판단** 입니다. 위헌으로 결정된 조문은 효력을 상실하며, 이후 법령 개정의 근거가 됩니다.

```
국민투표법 제14조
  └─ 헌재 2023헌가XX (위헌 결정)
       └─ 국민투표법 개정 (조문 삭제)
```

## 빠른 시작

```bash
git clone https://github.com/wellsa-ai/constitution-kr.git
cd constitution-kr

# 특정 결정례 보기
cat kr/2024/2024헌가12.md

# 특정 법령 관련 위헌·합헌 결정 검색
grep -rl "국민투표법" kr/
```

## 구조

```
kr/{선고연도}/
  {사건번호}.md            # 결정례 본문 (주문·이유)
  ...
```

## 메타데이터 (YAML Frontmatter)

```yaml
---
사건명: "국민투표법 제14조 위헌제청"
사건번호: "2024헌가12"
심판유형: "위헌법률심판"
선고일자: "2024-06-15"
주문: "위헌"
관련법령:
  - "국민투표법 제14조"
재판관:
  - "○○○ 재판관 (다수의견)"
헌재결정례일련번호: "12345"
출처: "https://www.law.go.kr/헌재결정례/(2024헌가12)"
---
```

## 자동 업데이트

매일 [국가법령정보센터 DRF API](https://open.law.go.kr) 의 `target=cnstdc` 를 체크하여 신규·정정 결정례가 있으면 자동으로 커밋합니다.

- `pipeline/cron_update.sh` — 매일 06:00 KST
- `pipeline/cron_full_sweep.sh` — 매일 23:30 KST

## 관련 프로젝트

| 프로젝트 | 대상 | 설명 |
|---|---|---|
| [legalize-kr](https://github.com/legalize-kr/legalize-kr) | 법률·시행령 | 대한민국 법령 |
| [regulate-kr](https://github.com/wellsa-ai/regulate-kr) | 행정규칙·고시 | 전 부처 행정규칙 |
| [precedent-kr](https://github.com/wellsa-ai/precedent-kr) | 법원 판례 | 대한민국 법원 판례 |
| [interpretation-kr](https://github.com/wellsa-ai/interpretation-kr) | 법령해석례 | 법제처 법령해석례 |
| **constitution-kr** (이 저장소) | 헌재결정례 | 헌법재판소 결정례 |
| [localrule-kr](https://github.com/wellsa-ai/localrule-kr) | 자치법규 | 지자체 자치법규 |
| [treaty-kr](https://github.com/wellsa-ai/treaty-kr) | 조약 | 대한민국 조약 |

## 활용 사례

- **법령 검색 보강**: 법령 검색 결과에 위헌·합헌 결정 동시 노출
- **법학 연구**: 위헌 결정 추이·헌법재판부 의견 분석
- **시민 권리 검색**: 헌법 권리 관련 공식 헌재 판단 확인 (예: [MiniLex](https://minilex.wellsa.ai))

## 데이터 출처

모든 결정례 데이터는 [국가법령정보센터 DRF API](https://open.law.go.kr) 에서 가져옵니다. 결정례 원문은 대한민국 정부 공공저작물로 자유롭게 이용 가능합니다.

## 라이선스

- 결정례 원문: 공공저작물 (대한민국 정부)
- 저장소 구조·파이프라인 코드: MIT
