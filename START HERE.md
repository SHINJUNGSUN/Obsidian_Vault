---
tags: [meta]
pinned: true
---
# 🏠 Vault Guide

## 📂 구조
| 폴더 | 용도 | Graph View |
|------|------|-----------|
| **MOC/** | 기술 주제별 허브 | ✅ 허브 노드 |
| **Knowledge/** | 원자적 지식 노트 | ✅ 핵심 노드 |
| **+Inbox/** | 빠른 메모 | ❌ 제외 |
| **+TIL/** | 일일 학습 기록 | ❌ 제외 |
| **+Templates/** | 노트 템플릿 | ❌ 제외 |
| **+Archive/** | 보관 | ❌ 제외 |

## 🔍 Graph View 필터
```
-path:+Inbox -path:+TIL -path:+Templates -path:+Archive
```

## 🔄 워크플로우
1. **+TIL**에 오늘 배운 것 기록
2. 핵심 개념 → **Knowledge** 노트로 분리
3. Knowledge 노트에 `[[링크]]` 추가
4. 해당 **MOC**에 링크 등록
5. **Graph View**에서 지식 연결 확인!

## 🏷️ 태그 규칙
- `moc` — MOC 허브 노트
- `til` — TIL 노트
- `debug` — 트러블슈팅
- 기술: `java` `spring` `react-native` `mysql` `redis` `kafka` `ddd` `iot` `ble`
