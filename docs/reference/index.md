---
layout: default
title: 레퍼런스
nav_order: 14
has_children: true
---


# 참조 (Reference)

> **관련 소스 파일**
> * [README.ja.md](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/README.ja.md)
> * [README.ko.md](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/README.ko.md)
> * [README.md](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/README.md)
> * [README.zh-cn.md](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/README.zh-cn.md)
> * [assets/oh-my-opencode.schema.json](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/assets/oh-my-opencode.schema.json)
> * [src/config/schema.ts](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts)
> * [src/hooks/index.ts](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/hooks/index.ts)
> * [src/index.ts](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/index.ts)
> * [src/shared/config-path.ts](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/shared/config-path.ts)

이 섹션은 oh-my-opencode의 모든 설정 가능한 측면에 대한 포괄적인 참조 문서를 제공합니다. 플러그인에서 사용 가능한 설정 옵션, 에이전트(Agent), 도구(Tool) 및 훅(Hook)을 찾아볼 수 있는 가이드 역할을 합니다.

**범위**: 이 페이지는 참조 자료의 개요와 일반적인 설정 작업을 위한 빠른 액세스 테이블을 제공합니다. 특정 구성 요소에 대한 자세한 문서는 다음을 참조하십시오.

* 설정 옵션: [Configuration Schema Reference](/code-yeongyu/oh-my-opencode/12.1-build-system)를 참조하십시오.
* 에이전트 사양: [Agent Reference](/code-yeongyu/oh-my-opencode/12.2-cicd-pipeline)를 참조하십시오.
* 도구 기능: [Tool Reference](/code-yeongyu/oh-my-opencode/12.3-release-process)를 참조하십시오.
* 훅 동작: [Hook Reference](/code-yeongyu/oh-my-opencode/12.4-dependency-management)를 참조하십시오.

## 설정 시스템 개요 (Configuration System Overview)

oh-my-opencode 플러그인은 검증, 마이그레이션 및 IDE 지원을 포함하는 계층적 JSON 기반 설정 시스템을 사용합니다.

### 설정 로딩 흐름 (Configuration Loading Flow)

**다이어그램: 설정 파일 로딩 및 검증**

```

```

**출처**: [src/index.ts L125-L217](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/index.ts#L125-L217)

 [src/shared/jsonc.ts L10-L30](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/shared/jsonc.ts#L10-L30)

 [src/shared/deep-merge.ts L1-L20](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/shared/deep-merge.ts#L1-L20)

 [src/config/schema.ts L178-L204](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L178-L204)

### 설정 파일 구조 (Configuration File Structure)

설정 시스템은 프로젝트 레벨 설정이 사용자 레벨 설정을 덮어쓰는 2단계 계층 구조를 사용합니다.

| 우선순위 | 위치 (Linux/macOS) | 위치 (Windows) |
| --- | --- | --- |
| 1 | `.opencode/oh-my-opencode.json(c)` | `.opencode/oh-my-opencode.json(c)` |
| 2 | `~/.config/opencode/oh-my-opencode.json(c)` | `~/.config/opencode/oh-my-opencode.json(c)` 또는 `%APPDATA%/opencode/oh-my-opencode.json(c)` |

**JSONC 지원**: `.json` 및 `.jsonc`(주석이 포함된 JSON) 형식을 모두 지원합니다. 두 파일이 모두 존재할 경우 `.jsonc` 파일이 우선권을 갖습니다.

**출처**: [src/index.ts L189-L217](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/index.ts#L189-L217)

 [src/shared/config-path.ts L1-L48](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/shared/config-path.ts#L1-L48)

 [src/shared/jsonc.ts L10-L30](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/shared/jsonc.ts#L10-L30)

### 설정 스키마 구조 (Configuration Schema Structure)

**다이어그램: OhMyOpenCodeConfig 타입 구조**

```

```

**출처**: [src/config/schema.ts L178-L204](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L178-L204)

 [src/mcp/types.ts L1-L5](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/mcp/types.ts#L1-L5)

### 최상위 설정 옵션 (Top-Level Configuration Options)

| 속성 | 타입 | 설명 | 기본값 | 참조 |
| --- | --- | --- | --- | --- |
| `disabled_mcps` | `McpName[]` | 비활성화할 MCP 서버 | `[]` | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `disabled_agents` | `AgentName[]` | 비활성화할 내장 에이전트 | `[]` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `disabled_hooks` | `HookName[]` | 비활성화할 훅 | `[]` | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `disabled_commands` | `BuiltinCommandName[]` | 비활성화할 내장 명령 | `[]` | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `agents` | `AgentOverrides` | 에이전트 설정 오버라이드 | `{}` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `claude_code` | `ClaudeCodeConfig` | Claude Code 호환성 토글 | `{}` | [#9](/code-yeongyu/oh-my-opencode/9-claude-code-compatibility) |
| `google_auth` | `boolean` | 내장 Google 인증 활성화 | `false` | [#2.2](../getting-started/Authentication-Setup.md) |
| `sisyphus_agent` | `SisyphusAgentConfig` | Sisyphus 오케스트레이터 설정 | `{}` | [#4.1](/code-yeongyu/oh-my-opencode/4.1-sisyphus-orchestrator) |
| `comment_checker` | `CommentCheckerConfig` | 주석 검사기(Comment checker) 커스터마이징 | `{}` | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `experimental` | `ExperimentalConfig` | 실험적 기능 플래그 | `{}` | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `auto_update` | `boolean` | 자동 업데이트 활성화 | `true` | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |

**출처**: [src/config/schema.ts L178-L204](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L178-L204)

## 시스템 구성 요소 빠른 참조 (System Components Quick Reference)

### 내장 MCP (Built-in MCPs)

**다이어그램: MCP 등록 및 설정**

```

```

**출처**: [src/index.ts L519-L528](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/index.ts#L519-L528)

 [src/mcp/index.ts L1-L40](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/mcp/index.ts#L1-L40)

 [src/mcp/types.ts L1-L5](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/mcp/types.ts#L1-L5)

| MCP 이름 | 용도 | 제공되는 도구 | 사용처 | 설정 함수 |
| --- | --- | --- | --- | --- |
| `websearch_exa` | 2025년 이후 필터가 적용된 웹 검색 | `search` | librarian | `createBuiltinMcps()` |
| `context7` | 공식 문서 조회 | `resolve-library-id`, `get-docs` | librarian | `createBuiltinMcps()` |
| `grep_app` | GitHub 코드 검색 | `search` | librarian, explore | `createBuiltinMcps()` |

**출처**: [src/mcp/index.ts L1-L40](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/mcp/index.ts#L1-L40)

 [src/mcp/types.ts L1-L5](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/mcp/types.ts#L1-L5)

### 내장 에이전트 (Built-in Agents)

**다이어그램: 에이전트 생성 및 설정 흐름**

```

```

**출처**: [src/index.ts L62-L94](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/index.ts#L62-L94)

 [src/index.ts L404-L486](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/index.ts#L404-L486)

 [src/agents/index.ts L1-L350](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/agents/index.ts#L1-L350)

 [src/features/claude-code-agent-loader.ts L1-L100](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/features/claude-code-agent-loader.ts#L1-L100)

| 에이전트 이름 | 기본 모델 | 모드 | 쓰기 권한 | 생성 주체 | 참조 |
| --- | --- | --- | --- | --- | --- |
| `Sisyphus` | `anthropic/claude-opus-4-5` | primary | 예 | `createBuiltinAgents()` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `Planner-Sisyphus` | `anthropic/claude-opus-4-5` | subagent | 아니요 | `createBuiltinAgents()` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `OpenCode-Builder` | `config.agent.build`에서 가져옴 | subagent | 예 | 런타임 | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `oracle` | `openai/gpt-5.2` | subagent | 아니요 (LSP 전용) | `createBuiltinAgents()` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `librarian` | `anthropic/claude-sonnet-4-5` | subagent | 아니요 | `createBuiltinAgents()` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `explore` | `opencode/grok-code` | subagent | 아니요 | `createBuiltinAgents()` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `frontend-ui-ux-engineer` | `google/gemini-3-pro-high` | subagent | 예 | `createBuiltinAgents()` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `document-writer` | `google/gemini-3-flash` | subagent | 예 | `createBuiltinAgents()` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `multimodal-looker` | `google/gemini-3-flash` | subagent | 아니요 | `createBuiltinAgents()` | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `build` | OpenCode 설정에서 가져옴 | primary/subagent | 예 | OpenCode | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |
| `plan` | OpenCode 설정에서 가져옴 | primary/subagent | 아니요 | OpenCode | [#13.2](/code-yeongyu/oh-my-opencode/13.2-agent-reference) |

**출처**: [src/agents/index.ts L1-L350](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/agents/index.ts#L1-L350)

 [src/index.ts L404-L486](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/index.ts#L404-L486)

### 내장 훅 (Built-in Hooks)

**다이어그램: 훅 초기화 및 이벤트 디스패치**

```

```

**출처**: [src/index.ts L219-L332](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/index.ts#L219-L332)

 [src/hooks/index.ts L1-L25](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/hooks/index.ts#L1-L25)

 [src/config/schema.ts L45-L68](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L45-L68)

| 훅 이름 | 생성 함수 | 주요 이벤트 | 용도 | 참조 |
| --- | --- | --- | --- | --- |
| `todo-continuation-enforcer` | `createTodoContinuationEnforcer()` | `session.idle` | 계속 진행 프롬프트 자동 주입 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `context-window-monitor` | `createContextWindowMonitorHook()` | `message.updated` | 토큰 사용량 추적, 70% 도달 시 경고 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `session-recovery` | `createSessionRecoveryHook()` | `session.error` | 중단 + 수정 + 재개 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `session-notification` | `createSessionNotification()` | `session.idle` | OS 알림 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `comment-checker` | `createCommentCheckerHooks()` | `tool.execute.after` | 주석에 대한 경고 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `tool-output-truncator` | `createToolOutputTruncatorHook()` | `tool.execute.after` | 동적 텍스트 자르기(Truncation) | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `directory-agents-injector` | `createDirectoryAgentsInjectorHook()` | `tool.execute.before` | AGENTS.md 주입 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `directory-readme-injector` | `createDirectoryReadmeInjectorHook()` | `tool.execute.before` | README.md 주입 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `empty-task-response-detector` | `createEmptyTaskResponseDetectorHook()` | `tool.execute.after` | 빈 작업 출력 감지 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `think-mode` | `createThinkModeHook()` | `chat.message` | 생각 모드(Thinking mode)로 전환 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `anthropic-context-window-limit-recovery` | `createAnthropicContextWindowLimitRecoveryHook()` | `session.error` | 한도 도달 시 자동 압축 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `preemptive-compaction` | `createPreemptiveCompactionHook()` | `message.updated` | 80% 도달 시 선제적 압축 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `rules-injector` | `createRulesInjectorHook()` | `tool.execute.before` | .claude/rules/ 주입 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `background-notification` | `createBackgroundNotificationHook()` | `session.idle` | 백그라운드 작업 알림 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `auto-update-checker` | `createAutoUpdateCheckerHook()` | `session.created` | npm 업데이트 확인 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `startup-toast` | (`auto-update-checker`의 일부) | `session.created` | 버전 토스트 알림 표시 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `keyword-detector` | `createKeywordDetectorHook()` | `chat.message` | ultrawork/search 감지 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `agent-usage-reminder` | `createAgentUsageReminderHook()` | `chat.message` | 에이전트 사용 권장 알림 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `non-interactive-env` | `createNonInteractiveEnvHook()` | `tool.execute.before` | CI 환경 변수 설정 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `interactive-bash-session` | `createInteractiveBashSessionHook()` | 다수 | tmux 세션 추적 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `empty-message-sanitizer` | `createEmptyMessageSanitizerHook()` | `experimental.chat.messages.transform` | 빈 메시지 제거 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |
| `thinking-block-validator` | `createThinkingBlockValidatorHook()` | `experimental.chat.messages.transform` | 생각 블록(Thinking blocks) 검증 | [#13.4](/code-yeongyu/oh-my-opencode/13.4-hook-reference) |

**출처**: [src/index.ts L238-L332](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/index.ts#L238-L332)

 [src/hooks/index.ts L1-L25](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/hooks/index.ts#L1-L25)

 [src/config/schema.ts L45-L68](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L45-L68)

## 에이전트 설정 구조 (Agent Configuration Structure)

**다이어그램: AgentOverrideConfigSchema 타입 계층 구조**

```

```

**출처**: [src/config/schema.ts L4-L103](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L4-L103)

### 에이전트 오버라이드 속성 (Agent Override Properties)

| 속성 | 타입 | 제약 조건 | 설명 |
| --- | --- | --- | --- |
| `model` | `string` | - | LLM 모델 식별자 (예: `"anthropic/claude-opus-4-5"`) |
| `temperature` | `number` | `0.0 - 2.0` | 창의성 제어를 위한 샘플링 온도 |
| `top_p` | `number` | `0.0 - 1.0` | 핵 샘플링(Nucleus sampling) 파라미터 |
| `prompt` | `string` | - | 전체 교체용 시스템 프롬프트 |
| `prompt_append` | `string` | - | 기본 시스템 프롬프트 뒤에 추가할 내용 |
| `tools` | `Record<string, boolean>` | - | 도구별 활성화/비활성화 (예: `{ "edit": false }`) |
| `disable` | `boolean` | - | 에이전트를 완전히 비활성화 |
| `description` | `string` | - | UI에 표시되는 에이전트 설명 |
| `mode` | `enum` | `'subagent' \| 'primary' \| 'all'` | 에이전트 작동 모드 |
| `color` | `string` | Hex 색상 패턴 | UI 색상 (예: `"#00CED1"`) |
| `permission` | `object` | 아래 참조 | 세밀한 권한 제어 |

**출처**: [src/config/schema.ts L74-L89](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L74-L89)

### 권한 시스템 (Permission System)

권한 시스템은 세 가지 수준의 액세스 제어를 제공합니다.

| 권한 수준 | 동작 |
| --- | --- |
| `ask` | 매번 사용자에게 승인 요청 |
| `allow` | 요청 없이 항상 허용 |
| `deny` | 작업을 항상 거부 |

`bash` 권한은 다음과 같이 세부적으로 지정할 수 있습니다.

* 단일 권한 문자열: `"ask"`, `"allow"`, 또는 `"deny"`
* 명령별 매핑: `{ "npm": "allow", "rm": "ask", "git": "allow" }`

**출처**: [assets/oh-my-opencode.schema.json L115-L176](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/assets/oh-my-opencode.schema.json#L115-L176)

## 실험적 기능 (Experimental Features)

**다이어그램: ExperimentalConfigSchema 구조**

```

```

**출처**: [src/config/schema.ts L127-L176](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L127-L176)

| 기능 | 타입 | 기본값 | 설명 | 참조 |
| --- | --- | --- | --- | --- |
| `aggressive_truncation` | `boolean` | `undefined` | 더 공격적인 도구 출력 자르기 | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `auto_resume` | `boolean` | `undefined` | 복구 후 자동으로 재개 | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `preemptive_compaction` | `boolean` | `undefined` | 하드 한도 도달 전 압축 트리거 | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `preemptive_compaction_threshold` | `number` | `undefined` | 압축을 트리거할 백분율 (0.5-0.95) | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `truncate_all_tool_outputs` | `boolean` | `true` | 화이트리스트뿐만 아니라 모든 도구에 자르기 적용 | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `dcp_for_compaction` | `boolean` | `undefined` | 요약 전 DCP 사용 | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |
| `dynamic_context_pruning` | `object` | 스키마 참조 | 전략을 사용한 고급 컨텍스트 정리 | [#13.1](/code-yeongyu/oh-my-opencode/13.1-configuration-schema-reference) |

**출처**: [src/config/schema.ts L163-L176](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L163-L176)

### 동적 컨텍스트 정리 설정 (Dynamic Context Pruning Configuration)

`dynamic_context_pruning` 실험적 기능은 여러 정리 전략을 통해 고급 컨텍스트 관리를 제공합니다.

| DCP 속성 | 타입 | 기본값 | 설명 |
| --- | --- | --- | --- |
| `enabled` | `boolean` | `false` | 동적 컨텍스트 정리 활성화 |
| `notification` | `'off' \| 'minimal' \| 'detailed'` | `'detailed'` | 알림 상세 수준 |
| `turn_protection.enabled` | `boolean` | `true` | 최근 도구 출력 보호 |
| `turn_protection.turns` | `number` | `3` | 보호할 최근 턴(Turn) 수 |
| `protected_tools` | `string[]` | `['task', 'todowrite', ...]` | 절대 정리되지 않는 도구 |
| `strategies.deduplication.enabled` | `boolean` | `true` | 중복 도구 호출 제거 |
| `strategies.supersede_writes.enabled` | `boolean` | `true` | 파일이 이후에 읽히면 쓰기 기록 정리 |
| `strategies.supersede_writes.aggressive` | `boolean` | `false` | 이후에 '어떤' 읽기라도 있으면 모든 쓰기 정리 |
| `strategies.purge_errors.enabled` | `boolean` | `true` | N턴 후 에러가 발생한 도구 입력 정리 |
| `strategies.purge_errors.turns` | `number` | `5` | 에러 정리 전 대기 턴 수 |

**출처**: [src/config/schema.ts L127-L161](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L127-L161)

## 버전 관리 및 자동 업데이트 (Version Management and Auto-Update)

**다이어그램: 자동 업데이트 시스템 아키텍처**

```

```

**출처**: [src/hooks/auto-update-checker/checker.ts L15-L264](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/hooks/auto-update-checker/checker.ts#L15-L264)

 [src/hooks/auto-update-checker/cache.ts L49-L93](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/hooks/auto-update-checker/cache.ts#L49-L93)

 [src/hooks/auto-update-checker/constants.ts L13-L41](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/hooks/auto-update-checker/constants.ts#L13-L41)

### 버전 감지 상수 (Version Detection Constants)

자동 업데이트 시스템은 상수에 정의된 플랫폼별 경로를 사용합니다.

**OPENCODE_CONFIG_PATHS** (순서대로 확인):

```

```

**OPENCODE_CACHE_DIR**:

* Linux/macOS: `~/.cache/opencode/`
* Windows: `%LOCALAPPDATA%/opencode/`

**출처**: [src/hooks/auto-update-checker/constants.ts L13-L41](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/hooks/auto-update-checker/constants.ts#L13-L41)

### 캐시 디렉터리 (Cache Directories)

| 용도 | 위치 (Linux/macOS) | 위치 (Windows) |
| --- | --- | --- |
| 플러그인 캐시 | `~/.cache/opencode/` | `%LOCALAPPDATA%/opencode/` |
| 설치된 패키지 | `~/.cache/opencode/node_modules/` | `%LOCALAPPDATA%/opencode/node_modules/` |
| 버전 추적 | `~/.cache/opencode/version` | `%LOCALAPPDATA%/opencode/version` |

**출처**: [src/hooks/auto-update-checker/constants.ts L13-L27](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/hooks/auto-update-checker/constants.ts#L13-L27)

## 설정 스키마 생성 (Configuration Schema Generation)

**다이어그램: 스키마 빌드 파이프라인**

```

```

**출처**: [script/build-schema.ts L1-L29](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/script/build-schema.ts#L1-L29)

 [src/config/schema.ts L178-L204](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/config/schema.ts#L178-L204)

 [assets/oh-my-opencode.schema.json L1-L10](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/assets/oh-my-opencode.schema.json#L1-L10)

### 스키마 참조 사용법 (Schema Reference Usage)

설정 파일은 IDE 지원을 위해 스키마를 참조합니다.

```

```

스키마는 다음 기능을 제공합니다.

* 모든 설정 속성에 대한 자동 완성
* 열거형 값(에이전트 이름, 훅 이름 등) 검증
* 숫자, 불리언, 문자열에 대한 타입 체크
* 색상, 모델 식별자 등에 대한 패턴 검증

**출처**: [assets/oh-my-opencode.schema.json L1-L10](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/assets/oh-my-opencode.schema.json#L1-L10)

 [README.md L709-L713](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/README.md#L709-L713)

## 탐색 가이드 (Navigation Guide)

이 참조 섹션은 네 개의 주요 하위 섹션으로 구성되어 있습니다.

1. **[Configuration Schema Reference](/code-yeongyu/oh-my-opencode/12.1-build-system)**: 예시 및 검증 규칙을 포함한 모든 설정 옵션에 대한 전체 문서
2. **[Agent Reference](/code-yeongyu/oh-my-opencode/12.2-cicd-pipeline)**: 기본 모델, 기능 및 사용 사례를 포함한 각 에이전트의 세부 사양
3. **[Tool Reference](/code-yeongyu/oh-my-opencode/12.3-release-process)**: 인자(Arguments), 권한 및 사용 예시를 포함한 모든 도구의 종합 목록
4. **[Hook Reference](/code-yeongyu/oh-my-opencode/12.4-dependency-management)**: 트리거 조건, 용도 및 설정 옵션을 포함한 전체 훅 카탈로그

이러한 구성 요소들이 어떻게 함께 작동하는지에 대한 개념적 정보는 다음을 참조하십시오.

* 에이전트 시스템 아키텍처: [#4](../agents/)
* 도구 시스템 개요: [#5](../tools/)
* 훅 시스템 아키텍처: [#7](../reliability/)
* 설정 시스템: [#3.2](/code-yeongyu/oh-my-opencode/3.2-configuration-system)
