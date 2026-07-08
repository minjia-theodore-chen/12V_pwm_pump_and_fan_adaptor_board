---
name: Process KiCad Component
description: Triggers when the user asks to process a downloaded KiCad component zip file and integrate it into the local libraries.
---

# Process KiCad Component Workflow

When the user asks you to process a new KiCad component (often downloaded as a ZIP file), follow this routine exactly to maintain the project's local library organization:

1. **Locate the Download**: Find the newly downloaded zip file. The user typically places it in `lib/downloads/` or sometimes in their system Downloads folder (`C:\Users\Chen\Downloads`).
2. **Decompress**: Unzip the contents into a temporary staging folder within `lib/downloads/`.
3. **Organize and Move Assets**:
   - Locate any `.kicad_sym` files, extract the `(symbol ...)` block, and append it into the category library `lib/symbols/<category>/<category>.kicad_sym`. Do not leave them as separate `.kicad_sym` files.
   - Locate any `.kicad_mod` files and move them to `lib/footprints/<category>/<category>.pretty/` (note the category subfolder before `.pretty`).
   - Locate any 3D model files (`.step`, `.stp`, `.wrl`) and move them to `lib/3D/<category>/`.
4. **Update File Associations (Crucial Step)**:
   - Read the `.kicad_mod` file you just moved.
   - Look for the `(model ...)` line.
   - Modify the 3D model path to use the project-relative `${KIPRJMOD}` convention. For example: `(model "${KIPRJMOD}/lib/3D/<category>/<model_filename>")`.
5. **Clean Up**: Delete the temporary extraction folder and the original `.zip` file from `lib/downloads/` to keep things tidy.
6. **Notify User**: Inform the user that the component has been successfully imported, placed in the local libraries, and that the relative paths are correctly configured for cross-machine portability.

*Note: Avoid writing random python scripts in the project root directory. Use powershell commands like `Expand-Archive`, `Move-Item`, or use your direct file editing tools.*
