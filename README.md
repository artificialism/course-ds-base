# course-ds-base

## Setup

Fork [the course repository](https://github.com/iterative/course-ds-base), clone your fork, and check out `step-1-organize-ml-project` where the project files live.

Use Python 3.11 for the versions of pandas and NumPy in `requirements.txt`. On macOS with Homebrew, install it with `brew install python@3.11`.

From the repository root, create and activate the local environment:

```bash
python3.11 -m venv dvc-venv
printf '\nexport PYTHONPATH=%q\n' "$PWD" >> dvc-venv/bin/activate
source dvc-venv/bin/activate
python -m pip install --upgrade 'pip>=25.3'
```

Constrain Cython when pip builds the older PyYAML release from source:

```bash
build_constraints="$(mktemp)"
printf 'Cython<3\n' > "$build_constraints"
python -m pip install --build-constraint "$build_constraints" -r requirements.txt
python -m pip check
```

Register the environment as a Jupyter kernel and start Notebook:

```bash
python -m ipykernel install --user --name dvc-venv
jupyter notebook
```

Open `notebooks/step-0-prototype.ipynb` and select the `dvc-venv` kernel. In a new terminal, reactivate `dvc-venv` before starting Jupyter.

## Project layout

| Directory | Contents |
| --- | --- |
| `notebooks/` | The original experiment prototypes |
| `data/raw/` | Source data |
| `data/processed/` | Data prepared for training |
| `models/` | Trained models |
| `reports/` | Metrics, plots, and reports |

## Code documentation

The Iris prototype uses petal length divided by petal width as a feature. Type annotations show that the function accepts and returns measurements as floats. The docstring records the input requirement.

```python
def petal_ratio(length_cm: float, width_cm: float) -> float:
    """Calculate length divided by width for a petal with positive width."""
    return length_cm / width_cm
```

## Task tracking

Use the [course issues](https://github.com/iterative/course-ds-base/issues) as checklists. Link the relevant issue in your pull request and list how you verified the change. For example, reference `iterative/course-ds-base#2` for the repository structure and `iterative/course-ds-base#3` for the environment.
