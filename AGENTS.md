# AGENTS.md

Guidance for AI coding agents working in this repository. Humans may follow it too.

## What this repository is

A **Timelink project directory**: Kleio source files associated with a
database. It serves as `timelink-home` in single-user, single-project mode,
and can also live inside the `projects/` directory of a multi-project home,
being used either standalone or as part of it. The `.timelink-project`
marker file in the root identifies the directory.

## Layout

| directory             | content                                                     |
|-----------------------|-------------------------------------------------------------|
| `sources/`            | Kleio source files (`.cli`, `.kleio`)                       |
| `structures/`         | structure files describing each type of source              |
| `mappings/`           | mappings between Kleio groups and database tables           |
| `inferences/`         | inference rules applied when processing the sources         |
| `identifications/`    | exports of the identification (record linking) process      |
| `database/sqlite/`    | SQLite database files (generated)                           |
| `database/backups/`   | database backups (generated)                                |
| `extras/`             | auxiliary project files: working documents, scripts, derived data |
| `notebooks/`          | Jupyter notebooks working with the project data             |
| `etc/doc/`            | pointers to the documentation                               |

## Rules

* **Do not delete or rename `.timelink-project`.** `find_local_kleio_home()`
  and the `timelink` CLI detect this directory by that marker; without it,
  detection falls back to fragile heuristics.
* **Never commit generated files.** Databases, backups and Kleio translation
  byproducts (`*.err`, `*.ids`, `*.org`, `*.old`, `*.cli-renamed`, `*.rep`,
  `strs/`) are covered by `.gitignore`; do not force-add them.
* **Kleio sources are transcriptions.** Files in `sources/` are scholarly
  work, and each file is copyright of its transcriber. Never rewrite them
  mechanically; content changes go through the researcher. Validate
  translations with the Kleio server before importing.
* **The database is derived data.** Everything in `database/` can be rebuilt
  from `sources/` by translating and importing; treat it as disposable.

## Python environment: one shared venv, OUTSIDE this project

Do not create a virtual environment inside this repository, and do not
accept VS Code's *Create Environment* prompt — it always writes `.venv`
into the workspace root, and per-project venvs accumulate silently (one
cleanup of a multi-project home removed nine of them: 3.9 GB, ~209,000
files, created one by one over three years of accepting that prompt).

Instead, create one shared venv outside the project and register it as a
Jupyter kernel:

```bash
python3.12 -m venv ~/venvs/timelink
~/venvs/timelink/bin/pip install -U pip
~/venvs/timelink/bin/pip install timelink            # stable release, the default
# or, to exercise unreleased code:
~/venvs/timelink/bin/pip install -e /path/to/timelink-py-checkout

~/venvs/timelink/bin/python -m ipykernel install --user --name timelink \
    --display-name "Python (timelink)"
```

Kernel registrations are user-level, not per-folder: every notebook on the
machine can pick **Python (timelink)** from the kernel picker. This
replaces the per-project `.venv`.

To stop VS Code from offering to create environments, preselect the
interpreter — VS Code has no setting to relocate the `.venv` its Create
Environment button creates; preselection is what prevents the prompt. Add
to this project's `.vscode/settings.json` (not to the template: the path
is machine specific):

```json
{ "python.defaultInterpreterPath": "/ABSOLUTE/PATH/TO/venvs/timelink/bin/python" }
```

Project resolution never depended on the venv location: it depends on the
working directory. Run notebooks from this directory or from `notebooks/`;
`find_local_kleio_home()` finds the project by the marker file.

Maintenance: `~/venvs/timelink/bin/pip install -U timelink` (or `git pull`
in the checkout, for the editable form). To pin a research run to a
release, create a versioned sibling venv such as `~/venvs/timelink-1.2.0`.

## Project specifics

<!-- Describe here the source collections of this project, the conventions
     used by the researchers, and anything else an agent must know before
     editing sources, structures or notebooks. -->
