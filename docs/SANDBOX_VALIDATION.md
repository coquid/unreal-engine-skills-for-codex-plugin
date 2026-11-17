# UE MCP validation

[한국어](SANDBOX_VALIDATION.ko-KR.md)

Enable `ModelContextProtocol` and `ToolsetRegistry` in an independent Windows content project. Enable `EditorToolset` for editor queries. Install the packaged ZIP using the [README](../README.md), then replace these example paths.

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
# After verifying the editor
python "$pluginRepo\scripts\sandbox_runner.py" stop @runnerArgs
```

Once the editor listens, open a new chat before running the stop command. Use `$unreal-mcp` to list toolsets and inspect the current level to confirm the target project. Verify the installed skills are `unreal-mcp`, `create-toolset` and `unreal-skill`. Use the final command to close the editor started by the helper.

## Historical results

The [combined v0.1.0 sandbox record](https://github.com/coquid/unreal-engine-skills-for-codex-plugin/blob/9937d3deeb10e362a7443d849048a9bcd4da7605/docs/SANDBOX_VALIDATION.md) and the [Idris port report](VALIDATION.md) document earlier versions.

## Split release verification

On 2026-11-17, the UE MCP v0.2.0 ZIP installed into an isolated Codex client home on Windows. Its catalog exposed all three UE skills. A stock UE 5.8 editor (BuildId 55116800) ran a content-only project with MCP, ToolsetRegistry and EditorToolset enabled. Codex listed its toolsets and read the current level as `/Engine/Maps/Entry`. Installing the AngelScript companion alongside it exposed six distinct skills.
