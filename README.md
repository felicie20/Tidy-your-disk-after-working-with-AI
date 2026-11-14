
Organize files after AI-assisted work: preserve final deliverables and source files, collect deletion candidates, simplify folders, and flag uncertain files with full paths. Use only after project completion; not recommended during active work. Personal, non-commercial use only.
# AI Workspace Tidy

**Keep your project easy to navigate after working with AI.**

Image generation, document revisions, slide creation, and repeated exports often leave behind duplicate files, abandoned drafts, temporary assets, and deeply nested output folders. This Agent Skill helps an AI assistant organize those materials, preserve final deliverables and essential source files, and set aside files that are clearly safe to remove.

> **When unsure whether a file can be deleted, leave it in place, list its full path, and ask the user to review it.**

## What it does

- **Preserves essential materials:** final deliverables, original inputs, editable source files, required assets, and configuration.
- **Groups deletion candidates:** verified duplicates, explicitly superseded drafts, and temporary files confirmed to be reproducible and no longer needed.
- **Handles empty folders:** checks for hidden files and identifies directory trees containing only empty subfolders.
- **Simplifies folder structure:** removes unnecessary organizational layers and keeps related images and ZIP packages together.
- **Flags uncertain files:** provides each file's full absolute path, the reason for uncertainty, and what the user should check.
- **Records the changes:** tracks file locations, verifies content, and distinguishes candidate file sizes from actual disk space recovered.

This is an instruction-based Agent Skill. It requires an AI assistant with permission to read and move local files. It does not include a standalone cleanup program and requires no additional service or API key. Other tools supporting Agent Skills may be able to use these instructions; discovery and file permissions depend on the host tool.

The skill instructions are currently written in Chinese. This README provides English installation and usage guidance. Default working folder names include `可删` (deletion candidates) and `清单与记录` (inventories and records). You can request alternative folder names in your prompt.

## Install in Codex

Download this repository. Name the folder containing `SKILL.md` as `ai-workspace-tidy` and place it in one of these locations:

| Scope | Location |
|---|---|
| Personal use | `~/.agents/skills/ai-workspace-tidy/` |
| Current project only | `<project>/.agents/skills/ai-workspace-tidy/` |

On Windows, `~` refers to your user home directory, such as `C:\Users\YourName`. Check that `ai-workspace-tidy/SKILL.md` exists directly inside the installed folder, without an extra nesting level introduced during extraction.

Codex detects skill changes automatically. If the skill does not appear, restart Codex. See the [official OpenAI Skills documentation](https://learn.chatgpt.com/docs/build-skills) for current installation and discovery behavior.

## Usage

Open your AI tool in the target project, or specify the folder to organize in your request:

```text
Use $ai-workspace-tidy to organize the files from this AI work session.
Preserve final deliverables and essential source files. Move clearly removable
files into a folder named "可删" and simplify unnecessary folder nesting.
Leave uncertain files in place, list their full absolute paths, and remind me
to review them. Write the report in English.
```

You can also request a narrower task.

**Review without moving anything:**

```text
Use $ai-workspace-tidy to review this project. List files to keep, deletion
candidates, and files requiring my review. Do not move anything yet.
```

**Collect deletion candidates:**

```text
Use $ai-workspace-tidy to move clearly removable files into "可删".
Preserve their relative paths so I can review them easily.
```

**Simplify the folder structure:**

```text
Use $ai-workspace-tidy to simplify this project's folder structure and record
the moves. Keep project and asset directories that rely on relative paths intact.
```

## How files are classified

| Category | Evidence | Default action |
|---|---|---|
| Keep | Confirmed final deliverables, original inputs, essential source files, and dependencies | Preserve intact in an appropriate location |
| Deletion candidate | Matching content with a complete retained copy; explicitly superseded drafts; confirmed unused caches or temporary outputs | Move to `可删` in the project root |
| Needs review | Unclear version status, unknown purpose, unique assets, or distinct design alternatives | Leave in place and report the full path |

A filename containing `draft`, `tmp`, or `v1` does not prove that a file is disposable. The highest version number does not prove that a file is final. A temporary folder may contain the only editable presentation, source file, or reference asset; those materials must be identified and preserved first.

## Example: files requiring review

These paths are illustrative and do not refer to real project files.

| Full absolute path | Why it needs review | What to check |
|---|---|---|
| `C:\Projects\Campaign\posters\poster-v2.png` | Uses a different color scheme from v3; no evidence it was rejected | Whether this color variant is still needed |
| `C:\Projects\Campaign\tmp\editable-source.pptx` | May be the only editable version | Whether this is the source for the final presentation |

The assistant should proactively point out these paths in its results. Uncertain files should not prevent it from organizing other files whose status is clear.

## Example output structure

Folder names and categories should fit the project. This structure is illustrative, not a required template.

```text
project/
├── topic-a/
│   ├── collection-one/
│   └── collection-two/
├── shared-designs/
├── references/
├── 清单与记录/              # Inventories, reports, and move records
├── 可删/                    # Deletion candidates
│   └── 空文件夹/            # Empty folders
└── folder-guide.md
```

The records folder holds move mappings, classification reasons, verification results, and files requiring review. Significant structural changes should also produce a short navigation guide. Older inventories with outdated paths should be marked as historical records.

## Default handling rules

- Collect deletion candidates by default. **Do not permanently delete files or empty the Recycle Bin.** Delete only when explicitly requested and within the authorized scope.
- Moving files into a candidate folder on the same disk **does not free disk space**. Reports distinguish candidate sizes, estimated deleted bytes, and measured changes in available space.
- Do not silently overwrite files, follow links outside the project, or reorganize hidden configuration and version-control directories without a reason and authorization.
- Check for file changes before moving. Verify file counts and SHA256 hashes afterward, and preserve or update internal references as needed.
- Work within the specified project. This skill is intended for organizing project materials, rather than whole-disk cleanup or source-code repository restructuring.

These are instructions for an AI assistant. Results depend on the model, available context, and tool permissions. The assistant should report what it actually verified and identify anything it could not complete.

## Repository contents

```text
ai-workspace-tidy/
├── SKILL.md                 # Skill description and workflow instructions
├── agents/
│   └── openai.yaml          # Display metadata and default prompt
├── README.md                # Installation and usage guide
└── LICENSE                  # Custom personal non-commercial use license
```

## License

This project is distributed under the custom [Personal Non-Commercial Use License](LICENSE).

- **Allowed:** individuals using the skill for personal hobbies, private learning, and organizing their own personal files; personal modifications; and sharing copies without charge under the same terms.
- **Not allowed:** use by companies, schools, universities, nonprofits, government bodies, or other organizations, including internal or non-commercial use.
- **Not allowed:** employment-related tasks, paid work, freelancing, consulting, client projects, or work performed on behalf of an organization, even through a personal account or device.
- **Not allowed:** selling the skill or including it in a paid product or service without separate written permission.

These restrictions apply to use of the skill. They do not transfer ownership of your files or impose a new license on your organized materials or generated reports.

This is a source-available project with usage restrictions, **not an OSI-approved open-source project**. The full terms in [LICENSE](LICENSE) govern use and redistribution.

## Feedback and contributions

Issues and pull requests are welcome, especially for reproducible cases involving ambiguous versions, source files hidden in temporary folders, filename conflicts, or relative-path dependencies.

Use fictional paths or a sanitized directory structure when sharing examples. Include the original layout, expected behavior, and actual result; private project files are not needed.

