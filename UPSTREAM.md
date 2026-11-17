# Upstream and maintenance

[한국어](UPSTREAM.ko-KR.md)

This community fork preserves Epic's history and adopts one pinned Codex port. It is not an official Epic Games or OpenAI release.

| Role | Repository | Baseline |
| --- | --- | --- |
| `upstream` | [Epic Games original](https://github.com/EpicGames/unreal-engine-skills-for-claude-code-plugin) | `0e27bde2b55c5d3f6948532f4296aaa3654d8f4b` (3.1.2) |
| `port-origin` | [Idris173 Codex port](https://github.com/Idris173/unreal-engine-skills-for-codex-plugin) | `a6c25ac96cea4cdfb93029e31423efd109d90895` |
| `origin` | [coquid fork](https://github.com/coquid/unreal-engine-skills-for-codex-plugin) | This repository |

The Idris port branches from Epic 3.1.1 (`a6aa73a`). Its commits `5378fdf` and `a6c25ac` are part of this fork's history.
The `create-toolset` and `unreal-skill` directories match the pinned port. The `unreal-mcp` references also incorporate Epic 3.1.2's guidance for assigning per-workspace ports and identifying the responding editor, adapted for Codex project configuration.

The [combined package at 9937d3deeb10e362a7443d849048a9bcd4da7605](https://github.com/coquid/unreal-engine-skills-for-codex-plugin/blob/9937d3deeb10e362a7443d849048a9bcd4da7605/UPSTREAM.md) is the split baseline. [UE AngelScript skills](https://github.com/coquid/ue-angelscript-skills-for-codex-plugins) are maintained independently. This fork retains the UE MCP skills, connection and validation helpers, and the original [MIT notice](LICENSE).

## Updating from Epic

Keep the three remotes above. Fetch `upstream`, review changes from the recorded Epic baseline, and merge a
reviewed upstream commit on a working branch. Keep the file layout and edit the original skills directly where
Codex requires a change; do not generate duplicate skill trees or introduce an overlay build step.

Resolve only the real Codex adaptation conflicts. Preserve Epic improvements to workflow content, examples,
and references. Preserve the Codex manifests and project-controlled connection setup. Do not restore the
removed `.claude-plugin` or automatic `hooks/` configuration: Codex can discover a conventional hooks file even
when a manifest does not explicitly reference it. Do not add a fixed endpoint or automatic configuration writes.
Review any new upstream script or dependency before adopting it.

A later Idris update is a separate, explicitly reviewed change; do not silently follow its HEAD.
Record new baseline SHAs and resolve license notices when importing updates.

## Validation after a merge

Run the package validator and deterministic packager, inspect the upstream skill diffs, and follow the target
project's policy for authored tests. Repeat direct editor checks when transport, discovery, API assumptions,
asset persistence, or UI behavior changes. Record the exact engine build and native plugin BuildId; a UE version
number alone does not establish compatibility. Keep historical third-party evidence separate from this fork's
[validation record](docs/SANDBOX_VALIDATION.md).
