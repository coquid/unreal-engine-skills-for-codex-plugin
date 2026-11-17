# UE MCP 검증

[English](SANDBOX_VALIDATION.md)

독립 Windows 콘텐츠 프로젝트에서 `ModelContextProtocol`과 `ToolsetRegistry`를 활성화합니다. 에디터 조회에는 `EditorToolset`도 활성화합니다. [설치 절차](../README.ko-KR.md)에 따라 배포 ZIP을 설치한 뒤 아래 예시 경로를 바꾸어 실행하세요.

```powershell
$pluginRepo = 'C:\Plugins\unreal-engine-skills-for-codex-plugin'
$projectFile = 'C:\Sandbox\SkillValidation\SkillValidation.uproject'
$engineRoot = 'C:\UnrealWorkspace\Engine'
$resultRoot = 'C:\Sandbox\SkillValidation\Saved\SkillValidation'
$codexExe = 'C:\Tools\Codex\codex.exe'
$runnerArgs = @('--project', $projectFile, '--engine', $engineRoot, '--port', '58241', '--results', $resultRoot,
    '--codex-executable', $codexExe)
python "$pluginRepo\scripts\sandbox_runner.py" preflight @runnerArgs
python "$pluginRepo\scripts\sandbox_runner.py" start @runnerArgs --startup-timeout 300
python "$pluginRepo\scripts\sandbox_runner.py" status @runnerArgs
# 검증이 끝나면 실행
python "$pluginRepo\scripts\sandbox_runner.py" stop @runnerArgs
```

에디터가 수신 대기하면 종료 전에 새 채팅에서 `$unreal-mcp`로 툴셋 목록과 현재 레벨을 조회해 대상 프로젝트를 확인하세요. 설치 목록은 `unreal-mcp`, `create-toolset`, `unreal-skill` 세 개여야 합니다. 확인 후 예시의 마지막 명령으로 이 도우미가 시작한 에디터를 종료하세요.

## 과거 결과

[통합판 v0.1.0의 에디터 검증 기록](https://github.com/coquid/unreal-engine-skills-for-codex-plugin/blob/9937d3deeb10e362a7443d849048a9bcd4da7605/docs/SANDBOX_VALIDATION.ko-KR.md)과 [Idris 포팅 검증](VALIDATION.ko-KR.md)은 각각 해당 버전의 결과입니다.

## 분리판 검증 결과

2026-11-17 Windows의 격리된 Codex 환경에 UE MCP v0.2.0 ZIP을 설치해 스킬 세 개를 확인했습니다. 설치형 UE 5.8(BuildId 55116800)의 콘텐츠 전용 프로젝트에 MCP, ToolsetRegistry, EditorToolset을 활성화했습니다. Codex에서 툴셋 목록과 현재 레벨 `/Engine/Maps/Entry`를 조회했습니다. AngelScript 플러그인을 함께 설치한 환경에서는 서로 다른 스킬 여섯 개를 확인했습니다.
