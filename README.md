# Meep Skill

A Codex skill for creating, debugging, and optimizing Meep/PyMeep simulations using a bundled local snapshot of the Meep documentation.

## What This Repo Contains

- `SKILL.md`: Main skill instructions and workflow.
- `references/navigation.md`: Task-to-document routing.
- `references/examples.md`: Task-to-tutorial-example routing with snippet pull commands.
- `references/workflows.md`: Implementation playbooks (flux, Harminv, near-to-far, mode decomposition, etc.).
- `references/troubleshooting.md`: Common failure modes and fixes.
- `scripts/meep_docs.py`: Local docs query/snippet extraction helper.
- `doc/docs`: Bundled Meep docs (primary source of truth for API behavior).

## Quick Start

Run from the repo root:

```bash
python scripts/meep_docs.py list --limit 40
python scripts/meep_docs.py search "stop_when_fields_decayed"
python scripts/meep_docs.py toc Python_User_Interface.md --max 50
python scripts/meep_docs.py section Python_User_Interface.md "Flux Spectra"
```

## Example Code Retrieval

List tutorial sections that contain code snippets:

```bash
python scripts/meep_docs.py examples --max-results 200
```

List snippets in a specific section:

```bash
python scripts/meep_docs.py snippets Python_Tutorials/Basics.md --title "Transmittance Spectrum of a Waveguide Bend" --lang py
```

Extract one snippet:

```bash
python scripts/meep_docs.py snippet Python_Tutorials/Basics.md 1 --title "Transmittance Spectrum of a Waveguide Bend" --lang py
```

Extract a full composed section script (recommended):

```bash
python scripts/meep_docs.py compose Python_Tutorials/Basics.md --title "Transmittance Spectrum of a Waveguide Bend" --lang py
```

## Using As a Codex Skill

1. Copy this folder to your Codex skills directory as `meep`.
2. Ensure `SKILL.md` remains at the skill root.
3. Trigger the skill by asking for Meep/PyMeep/FDTD simulation help.
4. Follow `SKILL.md` plus `references/*.md` and verify APIs in `doc/docs/Python_User_Interface.md`.

## Validation

If you have the skill-creator tooling available:

```bash
python ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py <path-to-this-skill>
```

## Notes

- Prefer Python (`import meep as mp`) unless Scheme/C++ is explicitly requested.
- For accuracy, adapt tutorial examples from `references/examples.md` before writing code from scratch.
- Always run convergence checks (resolution, runtime/decay, PML thickness) before final conclusions.
