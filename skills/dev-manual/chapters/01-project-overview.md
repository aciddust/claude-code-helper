# 챕터 1: 프로젝트 개요

## 프로젝트

- **이름**: claude-code-helper
- **설명**: Claude Code를 이용한 개발 환경 초기화 템플릿
- **기술 스택**: Bash, YAML, Markdown
- **패키지 매니저**: 없음 (스크립트 기반)

## 핵심 기능

1. `/setup` 매니저로 프로젝트 초기화
2. Hook 시스템으로 개발 프로세스 강제 (계획 → 승인 → 구현 루프)
3. 자동 품질 검사 및 서브에이전트 위임

## 디렉토리 구조

```bash
claude-template/            # git root
├── .claude-plugin/
│   └── plugin.json         # 플러그인 메타데이터
├── agents/                 # 서브에이전트 3개 (qa/test/planning)
│   ├── planning-agent.agent.md
│   ├── qa-agent.agent.md
│   └── test-agent.agent.md
├── commands/               # 커맨드 2개 (setup/plan-manager)
│   ├── plan-manager.md
│   └── setup.md
├── hooks/                  # Hook 스크립트 & 설정
│   ├── config.yml          # 중앙 설정 (커스터마이징 포인트)
│   ├── hooks.json          # Hook 등록
│   ├── lib/                # 매칭 엔진
│   │   ├── config-parser.sh
│   │   └── matcher.sh
│   ├── change-logger.sh
│   ├── checklist-tracker.sh
│   ├── completion-checker.sh
│   ├── plan-guard.sh
│   ├── post-tool-check.sh
│   ├── pre-prompt-check.sh
│   └── subagent-report-check.sh
├── skills/
│   └── dev-manual/         # 개발 매뉴얼 스킬
│       ├── SKILL.md
│       └── chapters/       # 챕터 6개 (01~06)
├── README.md
├── .claudeignore
└── .gitignore
```

## 핵심 규칙

1. **파일 하나에 하나의 역할** — Hook 스크립트는 단일 이벤트만 처리
2. **config.yml이 모든 동작을 제어** — 스크립트 직접 수정 불필요
3. **매칭 엔진 4조건**: 키워드, 의도, 작업 위치, 파일 내용
