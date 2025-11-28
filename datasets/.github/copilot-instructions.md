## Purpose
Short, actionable guidance for AI coding agents working in this repo.

## Big picture (what this project is)
- Small learning project centered on a dataset: `housing/housing.csv` (California housing dataset, ~20k rows).
- Primary entrypoint: the Jupyter notebook `housing/conceção.ipynb` which contains exploratory/workflow code and a couple of inline package installs.

## Key files to inspect
- `housing/conceção.ipynb` — open this first. It runs `pip install psycopg2-binary` in a cell, imports `dotenv` and `psycopg2`, and sets `os.environ['PGPASSFILE'] = 'NUL'` (Windows-specific).
- `housing/housing.csv` — main dataset used by the notebook. Columns are present in the header (e.g. longitude, latitude, median_income, median_house_value, ocean_proximity).
- `housing/Exercícios aprendizado de maquina.txt` — plain-text notes and questions in Portuguese; useful for context but not runnable.

## Discovered patterns & conventions
- Notebook-first development: there is no package manifest or tests. The notebook may install packages inline (see the top cell installing `psycopg2-binary`).
- DB usage: notebook contains a PostgreSQL connection snippet with hard-coded example values (DB_HOST, DB_NAME, DB_USER, DB_PASSWORD). Treat these as examples only — do not commit real credentials.
- Windows-specific handling: the notebook sets `PGPASSFILE = 'NUL'` to avoid password-file usage on Windows. Respect this when running locally on Windows.
- Filenames include non-ASCII characters (e.g., `conceção.ipynb`). Use proper encoding/quoting when creating scripts or referencing paths.

## Agent behaviour checklist (concrete, repository-specific)
- When inspecting code, open `housing/conceção.ipynb` and look for inline `pip install` cells — consider moving inline installs to a `requirements.txt` if you add reproducible scripts.
- If you find DB credentials in code, replace them with environment variable lookups (e.g., via `python-dotenv`). Do not leave plaintext credentials in commits.
- Use `housing/housing.csv` as the canonical dataset path for examples and tests; reference it with relative paths from the repo root.
- When adding reproducible runs, add a small `requirements.txt` listing observed imports (at minimum: `python-dotenv`, `psycopg2-binary`) and a short README note about launching the notebook.

## How to run / reproduce (what I observed)
- There is no build or test script. Repro steps (manual):
  1. Open `housing/conceção.ipynb` in VS Code or Jupyter.
  2. Run cells; the notebook itself contains a `pip install psycopg2-binary` cell which may try to install packages at runtime.
  3. The notebook attempts a Postgres connection using example values — either provide a `.env` file or skip DB cells.

## Integration points & risks
- Postgres: the notebook connects to a Postgres DB called `viagem_milhas` in an example; be careful not to execute destructive SQL if you wire a real DB.
- No CI or tests present: changes that modify notebook logic should include a short runnable script or tests so future agents can validate behavior.

## Where to make small, safe improvements
- Add `requirements.txt` with minimal deps discovered in the notebook.
- Add a short `README.md` in `housing/` explaining the dataset and which notebook to run.
- Replace any hard-coded credentials with `.env` access and add `.env.example` (do not add real secrets).

## If you need more context
- Ask the human owner to confirm: intended database usage, whether to formalize runtime deps, and preferred filename encoding handling for `conceção.ipynb`.

---
If you'd like, I can: create `housing/README.md`, generate a starter `requirements.txt` (based on imports observed), and add `.github/copilot-instructions.md` updates in Portuguese as well. What would you like next?
