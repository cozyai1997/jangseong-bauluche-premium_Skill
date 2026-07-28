# Jangseong Bauluche Premium Skill Pack

장성 바울루체 프리미엄 웹사이트의 현재 구현 계약을 재사용 가능한 Codex 스킬로 분리한 저장소입니다.

이 저장소는 사이트 소스가 아니라 유지보수 지침 모음입니다. 실제 사이트 소스 저장소는 `cozyai1997/jangseong-bauluche-premium`이며, 각 스킬은 임시 작업 경로가 아닌 Git·패키지 정체성으로 소스 저장소를 찾습니다.

## 포함된 스킬

| 스킬 | 용도 |
|---|---|
| `$bauluche-project-orientation` | 현재 Vercel/Supabase 경로, 코드 위치, 테스트 범위 확인 |
| `$bauluche-cinematic-match-cut` | 4초 인트로, 새로고침 재생, 히어로 매치컷, 접근성 |
| `$bauluche-development-evidence-ui` | 공식 근거 기반 개발호재 콘텐츠와 반응형 UI |
| `$bauluche-unit-plan-gallery` | 잘리지 않는 평면도, 검증된 타입 정보, 접근 가능한 탭 |
| `$bauluche-owner-auth-security` | 단일 소유자 매직링크 로그인과 관리자 경계 |
| `$bauluche-media-control-editor` | 6개 그룹·19개 이미지 카드와 편집/이력 UI |
| `$bauluche-signed-tus-upload` | 브라우저에서 Supabase로 직접 보내는 서명 TUS 업로드 |
| `$bauluche-media-lifecycle-security` | 업로드 펜스, 정리 경합, 이력/복원/보존, RLS와 Storage 보안 |
| `$bauluche-release-verification` | 로컬 검사, Vercel 배포 SHA, Supabase 및 운영 인수 검증 |

## 권장 사용 순서

1. 작업을 시작할 때 `$bauluche-project-orientation`으로 현재 저장소와 런타임을 확인합니다.
2. 변경 영역에 맞는 기능 스킬을 사용합니다.
3. 업로드 변경은 UI 스킬과 TUS 스킬을, 데이터베이스 변경은 수명주기 스킬을 함께 사용합니다.
4. 완료·푸시·배포 전에는 `$bauluche-release-verification`을 사용합니다.

각 폴더는 독립적인 스킬이며 다음을 포함합니다.

- `SKILL.md`: 트리거와 핵심 실행 절차
- `agents/openai.yaml`: 표시 이름, 설명, 기본 프롬프트
- `references/`: 상세 계약과 검증 기준

## 보안 원칙

이 저장소에는 환경 변수 값, 소유자 이메일, 매직링크, 쿠키, 업로드 토큰 또는 Supabase 비밀 키를 저장하지 않습니다. 문서에는 필요한 환경 변수 이름과 공개 가능한 구조만 기록합니다.
