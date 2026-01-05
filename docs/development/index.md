---
layout: default
title: 개발 (Development)
nav_order: 13
has_children: true
---


# 개발 가이드

> **관련 소스 파일**
> * [.github/workflows/ci.yml](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml)
> * [.github/workflows/publish.yml](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/publish.yml)
> * [bun.lock](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/bun.lock)
> * [package.json](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json)
> * [script/generate-changelog.ts](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/script/generate-changelog.ts)
> * [script/publish.ts](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/script/publish.ts)
> * [src/cli/config-manager.ts](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/cli/config-manager.ts)
> * [src/shared/jsonc-parser.test.ts](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/shared/jsonc-parser.test.ts)
> * [src/shared/jsonc-parser.ts](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/shared/jsonc-parser.ts)

이 문서는 oh-my-opencode 기여자들을 위한 개발 워크플로우, 빌드 시스템 및 기여 프로세스에 대한 개요를 제공합니다. 로컬 개발 환경 설정, 빌드 파이프라인 아키텍처, 테스트 절차, 그리고 코드 변경 사항이 릴리스(Release)로 게시되는 과정을 다룹니다.

특정 주제에 대한 자세한 정보는 다음을 참조하십시오:

* 빌드 시스템 설정 및 TypeScript 컴파일: [Build System](/code-yeongyu/oh-my-opencode/11.1-experimental-features)
* 지속적 통합(CI) 워크플로우 및 자동화된 테스트: [CI/CD Pipeline](/code-yeongyu/oh-my-opencode/11.2-keyword-modes)
* 게시 워크플로우 및 버전 관리: [Release Process](/code-yeongyu/oh-my-opencode/11.3-model-configuration)
* 의존성 근거 및 관리: [Dependency Management](/code-yeongyu/oh-my-opencode/11.4-parallel-execution-patterns)

---

## 사전 요구 사항 (Prerequisites)

이 프로젝트에는 다음과 같은 도구가 필요합니다:

| 도구 | 용도 | 버전 |
| --- | --- | --- |
| Bun | 런타임 및 패키지 매니저 | 최신 버전 |
| TypeScript | 타입 체크 | ^5.7.3 |
| Git | 버전 관리 | 제한 없음 |
| Node.js | npm 게시 (CI 전용) | 24+ |

**플랫폼 지원**: 이 프로젝트는 macOS, Linux, Windows에서 빌드됩니다. `bun install` 실행 시 현재 플랫폼에 맞는 네이티브 의존성(Native dependencies)이 자동으로 설치됩니다.

**소스**: [package.json L1-L70](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L1-L70)

---

## 개발 워크플로우 개요

```

```

**소스**: [package.json L22-L28](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L22-L28)

 [.github/workflows/ci.yml L1-L135](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L1-L135)

 [.github/workflows/publish.yml L1-L141](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/publish.yml#L1-L141)

---

## 빌드 시스템 아키텍처

빌드 시스템은 Bun을 기본 빌드 도구로 사용하며, 타입 생성을 위한 TypeScript와 커스텀 스키마 빌더를 활용합니다.

```

```

**주요 빌드 명령어**:

| 명령어 | 스크립트 | 용도 |
| --- | --- | --- |
| `bun run build` | 모든 빌드 단계 실행 | 전체 컴파일 파이프라인 |
| `bun run clean` | `rm -rf dist` | 빌드 결과물 삭제 |
| `bun run typecheck` | `tsc --noEmit` | 타입 체크만 수행 |
| `bun run prepublishOnly` | `clean && build` | 게시 전 후크(Pre-publish hook) |

**외부 의존성**: 빌드 시 네이티브 바이너리가 번들링되는 것을 방지하기 위해 `@ast-grep/napi`를 외부화(Externalize)합니다. 플랫폼별 바이너리는 런타임에 선택적 의존성(Optional dependencies)을 통해 해결됩니다.

**소스**: [package.json L22-L28](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L22-L28)

 [package.json L50-L69](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L50-L69)

---

## 프로젝트 파일 구조

```

```

**소스**: [package.json L1-L70](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L1-L70)

 [.github/workflows/ci.yml L1-L135](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L1-L135)

 [.github/workflows/publish.yml L1-L141](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/publish.yml#L1-L141)

---

## 테스트 전략

이 프로젝트는 단위 테스트를 위해 Bun의 내장 테스트 러너를 사용합니다.

**테스트 실행**:

```

```

**테스트 파일 규칙**: 테스트는 소스 파일과 동일한 위치에 `.test.ts` 접미사를 붙여 배치합니다 (예: [src/tools/grep/downloader.test.ts L1-L104](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/tools/grep/downloader.test.ts#L1-L104)).

**테스트 구조 예시**:

```

```

**CI 통합**: 테스트는 `master` 및 `dev` 브랜치에 대한 모든 푸시(Push)와 모든 풀 리퀘스트(Pull Request) 발생 시 자동으로 실행됩니다 ([.github/workflows/ci.yml L14-L29](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L14-L29)).

**소스**: [src/tools/grep/downloader.test.ts L1-L104](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/tools/grep/downloader.test.ts#L1-L104)

 [.github/workflows/ci.yml L14-L29](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L14-L29)

 [package.json L28](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L28-L28)

---

## 지속적 통합 (Continuous Integration)

두 개의 GitHub Actions 워크플로우가 품질 검사와 릴리스를 자동화합니다:

### CI 워크플로우 (.github/workflows/ci.yml)

**트리거**: `master`/`dev` 브랜치 푸시 또는 `master` 브랜치 대상 풀 리퀘스트

**작업(Jobs)**:

1. **test**: 신뢰할 수 있는 의존성 허용 목록(Allowlist)과 함께 `bun test` 실행
2. **typecheck**: 타입 검증을 위해 `tsc --noEmit` 실행
3. **build**: 프로젝트를 컴파일하고 출력 결과물이 존재하는지 확인
4. **draft-release**: (`dev` 브랜치 전용) 변경 로그(Changelog)를 포함한 초안 릴리스 생성

**신뢰할 수 있는 의존성**: 워크플로우는 `BUN_INSTALL_ALLOW_SCRIPTS` 환경 변수를 통해 `@ast-grep/napi`에 대해서만 설치 스크립트 실행을 명시적으로 허용합니다 ([.github/workflows/ci.yml L26](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L26-L26), [.github/workflows/ci.yml L43](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L43-L43)).

**스키마 자동 커밋**: 빌드 작업은 `master` 브랜치 푸시 시 `assets/oh-my-opencode.schema.json`의 변경 사항을 자동으로 커밋합니다 ([.github/workflows/ci.yml L76-L86](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L76-L86)).

**소스**: [.github/workflows/ci.yml L1-L135](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L1-L135)

### 게시 워크플로우 (.github/workflows/publish.yml)

**트리거**: 버전 범프(Bump) 선택을 포함한 수동 `workflow_dispatch` 실행

**입력값**:

* `bump`: `major`, `minor`, 또는 `patch` 중 선택
* `version`: 선택 사항인 명시적 버전 재정의(Override)

**작업(Jobs)**:

1. **test**: 릴리스 전 테스트 검증
2. **typecheck**: 릴리스 전 타입 검증
3. **publish**: 버전 범프, npm 게시, GitHub 릴리스 생성, `master` 브랜치 동기화

**OIDC 게시**: 공급망 보안을 위해 `NPM_CONFIG_PROVENANCE: true`를 통한 npm 출처(Provenance) 증명을 사용합니다 ([.github/workflows/publish.yml L126](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/publish.yml#L126-L126)).

**소스**: [.github/workflows/publish.yml L1-L141](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/publish.yml#L1-L141)

---

## 릴리스 프로세스 흐름

```

```

**버전 중복 제거**: 게시 스크립트는 대상 버전이 이미 npm에 존재하는지 확인하고, 충돌을 방지하기 위해 게시를 건너뜁니다 ([script/publish.ts L153-L160](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/script/publish.ts#L153-L160), [script/publish.ts L167-L170](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/script/publish.ts#L167-L170)).

**초안 릴리스 관리**: 게시 후, 워크플로우는 기존의 모든 "next" 초안 릴리스를 삭제합니다 ([.github/workflows/publish.yml L128-L131](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/publish.yml#L128-L131)).

**소스**: [script/publish.ts L1-L184](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/script/publish.ts#L1-L184)

 [.github/workflows/publish.yml L61-L141](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/publish.yml#L61-L141)

---

## 네이티브 의존성 (Native Dependencies)

이 프로젝트에는 특별한 처리가 필요한 네이티브 의존성이 포함되어 있습니다:

### 신뢰할 수 있는 의존성 시스템

다음 패키지들은 설치 스크립트를 실행하며, [package.json L65-L69](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L65-L69)에서 명시적으로 허용 목록에 포함되어 있습니다:

```

```

**설치**: 스크립트 실행을 제한하기 위해 항상 `BUN_INSTALL_ALLOW_SCRIPTS`를 사용하십시오:

```

```

### Ripgrep 런타임 설치

다른 네이티브 의존성과 달리, ripgrep은 패키지 설치 시점에 설치되지 **않습니다**. 대신, [src/tools/grep/downloader.ts L125-L173](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/tools/grep/downloader.ts#L125-L173)에서 처음 사용할 때 ripgrep을 다운로드하여 `~/.cache/oh-my-opencode/bin/`에 설치합니다.

**플랫폼 매핑** ([src/tools/grep/downloader.ts L21-L27](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/tools/grep/downloader.ts#L21-L27)):

| 플랫폼 키 | Ripgrep 플랫폼 | 아카이브 형식 |
| --- | --- | --- |
| `arm64-darwin` | `aarch64-apple-darwin` | tar.gz |
| `arm64-linux` | `aarch64-unknown-linux-gnu` | tar.gz |
| `x64-darwin` | `x86_64-apple-darwin` | tar.gz |
| `x64-linux` | `x86_64-unknown-linux-musl` | tar.gz |
| `x64-win32` | `x86_64-pc-windows-msvc` | zip |

**소스**: [package.json L65-L69](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L65-L69)

 [src/tools/grep/downloader.ts L19-L173](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/src/tools/grep/downloader.ts#L19-L173)

 [bun.lock L25-L29](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/bun.lock#L25-L29)

---

## 로컬 개발 워크플로우

### 초기 설정

```

```

### 개발 사이클

```

```

### 플러그인 로컬 테스트

게시하지 않고 OpenCode에서 플러그인을 테스트하려면:

1. 플러그인 빌드: `bun run build`
2. OpenCode 설정에서 로컬 경로를 참조하십시오: ``` ```

### 커밋 전 확인 사항

```

```

**소스**: [package.json L22-L28](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L22-L28)

 [.github/workflows/ci.yml L23-L29](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L23-L29)

---

## 의존성 업그레이드 전략

**락 파일(Lock File)**: [bun.lock L1-L116](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/bun.lock#L1-L116)은 재현 가능한 빌드를 보장합니다. 의존성 업데이트 후 락 파일 변경 사항을 커밋하십시오.

**네이티브 의존성**: `@ast-grep/cli`, `@ast-grep/napi`, 또는 `@code-yeongyu/comment-checker`를 업그레이드할 때 CI 워크플로우가 여전히 설치 스크립트를 올바르게 실행하는지 확인하십시오.

**OpenCode SDK**: 이 플러그인은 `@opencode-ai/plugin`([package.json L54](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L54-L54))에 의존하며, 이는 `@opencode-ai/sdk`를 전이적(Transitively)으로 포함합니다. 이는 OpenCode의 릴리스 사이클을 따라야 합니다.

**업그레이드 체크리스트**:

1. [package.json L49-L59](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L49-L59)에서 버전 업데이트
2. `bun install`을 실행하여 [bun.lock L1-L116](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/bun.lock#L1-L116) 업데이트
3. `bun run typecheck` 및 `bun test` 실행
4. 로컬 OpenCode 설치 환경에서 테스트
5. `package.json`과 `bun.lock` 모두 커밋

**소스**: [package.json L49-L69](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L49-L69)

 [bun.lock L1-L116](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/bun.lock#L1-L116)

---

## 주요 개발 파일

| 파일 | 용도 | 수정 시점 |
| --- | --- | --- |
| `package.json` | 의존성, 스크립트, 메타데이터 | 의존성 추가, 버전 변경, 스크립트 업데이트 시 |
| `tsconfig.json` | TypeScript 컴파일 옵션 | 타겟/모듈 변경, 경로 매핑 추가 시 |
| `.github/workflows/ci.yml` | CI 자동화 | 테스트 전략 변경, 빌드 단계 추가 시 |
| `.github/workflows/publish.yml` | 릴리스 자동화 | 릴리스 프로세스 수정, npm 설정 변경 시 |
| `script/publish.ts` | 버전 및 릴리스 로직 | 버전 관리 전략 변경, 변경 로그 형식 수정 시 |
| `script/build-schema.ts` | JSON 스키마 생성 | 스키마 출력 형식 변경 시 |

**소스**: [package.json L1-L70](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/package.json#L1-L70)

 [.github/workflows/ci.yml L1-L135](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/ci.yml#L1-L135)

 [.github/workflows/publish.yml L1-L141](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/.github/workflows/publish.yml#L1-L141)

 [script/publish.ts L1-L184](https://github.com/code-yeongyu/oh-my-opencode/blob/b92cd6ab/script/publish.ts#L1-L184)
