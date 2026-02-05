## Purpose
Short, actionable guidance for AI coding agents working in this repository.

## Big picture
- This is a learning-focused machine learning repository based on the book "Hands-On Machine Learning with Scikit-Learn, Keras and TensorFlow". Notebooks are the primary artifacts.
- Main datasets and experiments live under `datasets/housing/` (canonical data: `housing.csv`).
- Primary entrypoints: `aprendizado_de_maquina.ipynb`, `Modelo_Classificação.ipynb`, and `datasets/housing/conceção.ipynb` — open these notebooks first to understand workflows.

## Key files to inspect (use these first)
- `datasets/housing/conceção.ipynb` — exploratory analysis, inline `pip install` cells, and a Postgres connection snippet. Contains Windows-specific handling: `os.environ['PGPASSFILE'] = 'NUL'`.
- `datasets/housing/housing.csv` — canonical dataset used by the notebooks (relative path from repo root).
- `README.md` — project purpose and used libraries (Python 3.11, scikit-learn, Keras/TensorFlow, matplotlib/seaborn, pandas, numpy).

## Discovered patterns & repo-specific conventions
- Notebook-first development: there is no top-level `requirements.txt`, no tests, and no CI. Expect exploratory code in .ipynb files.
- Inline installs: some notebooks run `pip install` in cells (example: `psycopg2-binary`). When converting cells to scripts, move installs into a `requirements.txt` or environment spec.
- Windows handling: the notebook explicitly sets `PGPASSFILE = 'NUL'`. When running on Windows, respect this or use equivalent handling for password files.
- Filenames contain non-ASCII characters (e.g., `conceção.ipynb`). Use UTF-8 aware file handling and quote paths when scripting.
- Database snippets are examples: Postgres connection values are illustrative — do not commit real credentials.

## Repro / developer workflows (concrete)
- Typical manual workflow:
  1. Create/activate a virtual env (`python -m venv .venv` + `.\.venv\Scripts\Activate.ps1`) or use conda.
  2. Open the target notebook in VS Code or Jupyter and run cells interactively.
  3. If a notebook has inline `pip install`, either run it interactively or extract requirements and install before running.
- Recommended commands (PowerShell):
```powershell
python -m venv .venv; .\.venv\Scripts\Activate.ps1; pip install -r requirements.txt
```

## Agent behaviour checklist (concrete, repository-specific)
- Open `datasets/housing/conceção.ipynb` first and read top cells for inline installs and DB usage.
- If adding reproducible scripts: extract imports from notebooks and create `requirements.txt` (minimum: `python-dotenv`, `psycopg2-binary`, `pandas`, `scikit-learn`, `tensorflow` as observed).
- Replace hard-coded DB credentials with environment variables or `.env` (use `python-dotenv`) and add `.env.example` (never commit secrets).
- When referencing the dataset, use the repository-relative path `datasets/housing/housing.csv`.
- Preserve notebook semantics when converting to scripts (data paths, encoding for `conceção.ipynb`).

## Integration points & risks
- Postgres example in the notebook: may contain example DB name `viagem_milhas`. Avoid executing any SQL that could be destructive when connected to a real DB.
- No CI/tests: validate changes by adding a small script or unit test that loads `datasets/housing/housing.csv` and runs a lightweight data-loading assertion.

## Small, safe improvements agents may propose or implement
- Add `requirements.txt` with minimal discovered deps.
- Add `datasets/housing/README.md` explaining the dataset and which notebook to run.
- Add `.env.example` showing expected environment variables for DB connection.
- Convert small, self-contained notebook fragments into runnable scripts under `scripts/` and include a short test that loads `housing.csv`.

## Questions for the repo owner (ask before making big changes)
- Do you want inline notebook installs consolidated into a single `requirements.txt` or left as-is?
- Should notebook filenames with non-ASCII characters be normalized, or keep original names?
- Is the Postgres snippet intended to connect to a real service or just an example for local experimentation?

---
If you want, I can: create `requirements.txt`, add `datasets/housing/README.md`, and add a root `.github/copilot-instructions.md` translation to Portuguese. Which would you like next?
