# 3DMSA — PDB + MSA Conservation Viewer

A single-file, browser-based tool for visualising protein structures coloured by multiple sequence alignment (MSA) conservation. No installation, no build step — just open `index.html`.

## Features

- **3D structure viewer** powered by [3Dmol.js](https://3dmol.csb.pitt.edu/) (WebGL)
- **Load PDB** from a local file or fetch directly from the RCSB PDB
- **Load MSA** in FASTA (`.fa`, `.fasta`) or Clustal (`.aln`, `.clustal`) format — auto-detected
- **Automatic sequence matching** — the MSA row closest to the PDB chain is identified via semi-global alignment, supporting domain-vs-full-length ORF matching
- **Per-residue conservation colouring** on the structure using a ConSurf-style cyan (variable) → white → maroon (conserved) ramp
- **Two conservation metrics** — % pairwise identity (default) or Shannon entropy, switchable on the fly
- **Block-wrapped MSA display** (Clustal-style) with residue numbering, toggleable sequences, and real-time conservation recalculation
- **Bidirectional linked selection** — click a 3D residue to highlight its MSA column; click an MSA cell to label the residue on the structure
- **Combinable 3D styles** — mix Cartoon, Stick, Sphere, Line, and Surface with adjustable surface transparency
- **PyMOL export** — download a self-contained `.pml` script with conservation mapped to the B-factor column, ready to open in PyMOL

## Quick start

### Option 1 — Local HTTP server (recommended)

Serving via HTTP enables the **Fetch RCSB** button to download structures directly from the PDB. Any static HTTP server works; the simplest is Python's built-in one:

```bash
cd /path/to/this/folder
python3 -m http.server 8000
```

Then open [http://localhost:8000](http://localhost:8000) in your browser.

### Option 2 — Open the file directly

Double-click `index.html` or open it with `File → Open` in your browser. Everything works except **Fetch RCSB**, which is blocked by the browser's cross-origin policy when loading from a `file://` URL. You can still load local `.pdb` files with the **Load PDB file** button.

## Usage

1. **Load a structure** — click **Load PDB file** to open a local `.pdb` / `.cif`, or type a 4-character PDB ID and press **Fetch RCSB**.
2. **Load an alignment** — click **Load MSA** and select a FASTA or Clustal alignment file.
3. The closest MSA sequence is auto-matched to the PDB chain (highlighted with a yellow **MATCH** badge). Conservation is mapped onto the structure immediately.
4. **Toggle sequences** on/off with the checkboxes — conservation updates in real time. The matched row is locked on.
5. **Switch conservation metric** with the dropdown (% pairwise identity or Shannon entropy).
6. **Mix 3D styles** by toggling Cartoon / Stick / Sphere / Line / Surface. Adjust surface transparency with the **&alpha;** slider.
7. **Click a 3D residue** to highlight its column in the MSA, or **click an MSA cell** to label the corresponding residue on the structure. Press **Esc** to clear.
8. **Export to PyMOL** — click **Export PyMOL** to download a `.pml` script. Open it in PyMOL with `File → Run Script` or from the command line:
   ```bash
   pymol session.pml
   ```
   To save as a `.pse` session file, run the script then save:
   ```bash
   pymol -cq session.pml -d "save session.pse; quit"
   ```

## Example files

| File | Description |
|------|-------------|
| `H.pdb` | e structure (2 chains, 1aa each) |
| `.aln` | Clustal alignment  |
| `.fa` | FASTA alignment of 15  |

## Requirements

- A modern browser with WebGL support (Chrome, Firefox, Edge, Safari)
- No server-side dependencies — the only external resource is the 3Dmol.js library loaded from CDN
- Python 3 (optional, only needed for Option 1)

## License

MIT
