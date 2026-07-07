# 12V PWM Pump and Fan Adaptor Board

This project uses a self-contained, project-specific library structure to ensure maximum portability across different machines via Git.

## KiCad Library Organization

Instead of relying on global or system-wide KiCad libraries, all components (symbols, footprints, and 3D models) are stored locally within the `lib/` directory.

### Directory Structure

The `lib/` directory is organized as follows:

*   **`lib/downloads/`**: Staging area for raw files downloaded from component vendors (e.g., `.zip` files containing symbols, footprints, and 3D models).
*   **`lib/symbols/`**: Contains the project's schematic symbol libraries (`.kicad_sym`).
*   **`lib/footprints/`**: Contains the project's footprint libraries (`.pretty` folders with `.kicad_mod` files).
*   **`lib/3D/`**: Stores the 3D models (e.g., `.stp` files) used by the footprints.

Within these directories, files are typically categorized by component type (e.g., `connectors`).

### Linking Assets

To ensure portability, all assets are linked using the project-relative path variable `${KIPRJMOD}`:

1.  **Library Tables**: In the `fp-lib-table` (and `sym-lib-table`), libraries are referenced relatively, e.g., `${KIPRJMOD}/lib/footprints/connectors/connectors.pretty`.
2.  **Footprint to 3D Model**: In the footprint editor, the 3D model is linked using the relative path, e.g., `${KIPRJMOD}/lib/3D/connectors/0039300080.stp`.
3.  **Symbol to Footprint**: Symbols in the schematic are linked to the local footprint library, e.g., `connectors:39-30-Y080`.

## Workflow for Adding New Components

When adding a new component from the web, follow this routine:

1.  **Download**: Save the downloaded KiCad library archive into `lib/downloads/`.
2.  **Decompress & Organize**: Extract the files and move them to their respective directories (`.kicad_sym` to `lib/symbols/`, `.kicad_mod` to `lib/footprints/`, and `.stp`/`.wrl` to `lib/3D/`). Create new library files/folders if necessary.
3.  **Link 3D Model**: Open the footprint in the KiCad Footprint Editor, configure the 3D model path to point to the correct file in `lib/3D/` using the `${KIPRJMOD}` prefix, and save it to the correct project footprint library.
4.  **Link Footprint**: Open the symbol in the KiCad Symbol Editor (or directly in the schematic), update the Footprint property to point to the newly imported footprint in the local library, and save it.
