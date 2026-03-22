<div align="center">

# Project Review Guide

**AI 기반 PR 리뷰 + 기획 검토 체계**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

3명의 AI 봇 리뷰어와 Claude Code의 기획 리뷰를 결합하여,
**코드 품질**과 **서비스 방향성**을 동시에 검증하는 리뷰 가이드입니다.

</div>

---

## 왜 필요한가?

일반적인 AI 코드 리뷰 봇은 **코드 레벨**만 봅니다:
- "이 함수에 에러 핸들링이 없습니다"
- "0 나누기 위험이 있습니다"

하지만 실제로 중요한 건 **서비스 레벨** 검토입니다:
- "이 기능이 PRD에 있는 건가?"
- "타겟 유저에게 이 UX가 적절한가?"
- "이번 스프린트 목표와 맞는 작업인가?"

이 가이드는 **두 레벨을 모두 커버**합니다.

---

## 리뷰 체계 구조

```
PR 생성
  │
  ├─ [코드 리뷰] 봇 3명 자동 실행
  │   ├─ Gemini Code Assist — Google AI 리뷰
  │   ├─ CodeRabbit — 변경 요약 + 코드 리뷰
  │   └─ GitHub Copilot — Copilot 리뷰
  │
  ├─ [기획 리뷰] Claude Code 리뷰 종합
  │   ├─ 봇 리뷰 종합 (동의/충돌/채택/기각)
  │   ├─ PRD 대조 — 기능이 기획과 일치하는지
  │   ├─ 서비스 방향성 — 타겟 유저/핵심 가치와 부합하는지
  │   └─ PRD 업데이트 필요 여부 판단
  │
  ├─ [토론] CodeRabbit (최대 1회전)
  │   ├─ @coderabbitai 멘션으로 질문
  │   ├─ 봇 응답 확인 → 최종 판단
  │   └─ 추가 질문 없이 머지
  │
  └─ 머지
```

---

## 빠르게 시작하기

### 1. 템플릿 파일 복사

```bash
# 새 프로젝트 루트에서
cp templates/.coderabbit.yaml .coderabbit.yaml
cp templates/.github/workflows/label-pr.yml .github/workflows/label-pr.yml
cp templates/.github/labeler.yml .github/labeler.yml
```

### 2. CLAUDE.md에 리뷰 규칙 추가

`guides/claude-md-template.md`의 Issue/PR/리뷰 섹션을 프로젝트 CLAUDE.md에 복사합니다.

---

## 가이드 문서

| 문서 | 설명 |
|------|------|
| [코드 리뷰 가이드](guides/code-review.md) | 봇 3명 설정 + 코드 레벨 리뷰 규칙 |
| [기획 리뷰 가이드](guides/product-review.md) | PRD 대조 + 서비스 방향성 검토 |
| [리뷰 토론 절차](guides/review-discussion.md) | 1회전 토론 규칙 + 무한 루프 방지 |
| [PRD 동기화 가이드](guides/prd-sync.md) | PRD 드리프트 방지 규칙 |
| [CLAUDE.md 템플릿](guides/claude-md-template.md) | 새 프로젝트용 리뷰 규칙 템플릿 |

## 템플릿 파일

| 파일 | 설명 |
|------|------|
| [.coderabbit.yaml](templates/.coderabbit.yaml) | CodeRabbit 한국어 설정 |
| [label-pr.yml](templates/.github/workflows/label-pr.yml) | Copilot + 자동 라벨링 |
| [labeler.yml](templates/.github/labeler.yml) | 경로 기반 라벨 규칙 |

---

## 봇별 역할과 한계

| 봇 | 잘하는 것 | 못하는 것 | 토론 가능 |
|----|----------|----------|:---------:|
| Gemini Code Assist | 전체 코드 품질 리뷰 | 서비스 맥락 이해 | ❌ |
| CodeRabbit | 변경 요약 + 리뷰 | 비즈니스 로직 검증 | ✅ `@coderabbitai` |
| Copilot | 인라인 코드 제안 | 아키텍처 판단 | ❌ |
| **Claude Code** | **기획 리뷰 + 리뷰 종합** | 실시간 자동 트리거 | **중재자** |

---

## 비용

| 항목 | 비용 |
|------|------|
| Gemini Code Assist | 무료 (GitHub App) |
| CodeRabbit | 무료 (GitHub App) |
| Copilot | GitHub 구독에 포함 |
| Claude Code | Claude Max 구독 |

**추가 API 키 불필요. 모든 봇이 무료로 작동합니다.**

---

## License

[MIT](LICENSE)
