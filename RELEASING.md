# Releasing bm25s-cupy

This repository is configured as a drop-in fork:

- PyPI distribution name: `bm25s-cupy`
- Python import package: `bm25s`
- Release workflow: `.github/workflows/publish-python.yaml`
- GitHub environment expected by the workflow: `pypi`

## One-time PyPI setup

Create a PyPI Trusted Publisher for `bm25s-cupy`.

If the project does not exist on PyPI yet, create a pending publisher from your
PyPI account publishing settings:

- PyPI project name: `bm25s-cupy`
- Owner: `lm-cyber`
- Repository: `bm25s_cupy`
- Workflow name: `publish-python.yaml`
- Environment name: `pypi`

The pending publisher creates the PyPI project on the first successful publish.
It does not reserve the project name before that first publish, so do the first
release soon after creating it.

In GitHub repository settings, create an environment named `pypi`. Keep required
reviewers enabled if you want a manual approval gate before uploading to PyPI.

## Release flow

1. Make sure the branch to release is merged to `main`.
2. Create a tag using a valid Python version:

   ```bash
   git tag v0.1.0
   git push origin v0.1.0
   ```

3. Create a GitHub Release for that tag.
4. Publish the GitHub Release.
5. Approve the `pypi` environment deployment if GitHub asks for approval.
6. Check the package at https://pypi.org/project/bm25s-cupy/.

The release workflow sets `BM25S_VERSION` from the GitHub Release tag. Tags like
`v0.1.0` are normalized to package version `0.1.0`.

## Local build check

Before publishing, run:

```bash
python -m pip install --upgrade build twine
BM25S_VERSION=0.1.0 python -m build
twine check dist/*
```
