# OpenSCAD Parametric Modeler Agent

A workflow and agent configuration for generating and validating parametric 3D models using OpenSCAD.

## Prerequisites

- **OpenSCAD**: The `openscad` binary must be installed and available in your PATH.

## Installation

1. Clone or copy this repository.
2. Ensure `AGENTS.md` is present to configure the agent persona.
3. Place your OpenSCAD model (`.scad`) in this directory.

## Getting Started

### For Humans
To manually check your model for errors, run:

```bash
openscad -o /dev/null --export-format stl -q <your_file.scad> 2> errors.txt
```

- If `errors.txt` is empty, the model is valid.
- If `errors.txt` contains errors, review them and update the model.

### Breaking the Loop
If the agent gets stuck in a loop (e.g., repeatedly fixing the same error):
1. **Inspect `errors.txt`**: Check if the error is consistent or changing.
2. **Manual Fix**: Edit the model file directly to resolve the issue.
3. **Restart**: Give the agent a new file or updated parameters to start fresh.

### For Agents
You are an **Expert OpenSCAD Engineer**. Your goal is to create valid OpenSCAD code following this strict loop:

1. **Target**: Work on the file specified by the user (default: `working.scad`).
2. **Validate**: Run the command above on the target file.
3. **Analyze**: Read `errors.txt`.
   - If empty: Stop. The model is valid.
   - If errors exist: Fix **only** the reported issues. Do not redesign the model.
4. **Iterate**: Repeat until `errors.txt` is empty.

## Rules of Engagement

| Rule | Description |
|------|-------------|
| **Selective Modification** | Modify only the specific parts requested by the user. |
| **Code Integrity** | Keep all other code unchanged to ensure existing functionality is preserved. |
| **File Handling** | Do **not** overwrite the original `.scad` file. Write all modifications to a new file with a similar filename (e.g., `original_modified.scad`). |

## Project Files

| File | Description |
|------|-------------|
| `AGENTS.md` | Agent persona and rules. |
| `working.scad` | The current OpenSCAD source file. |
| `errors.txt` | The latest compilation log. |
