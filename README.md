A quick and dirty demonstration of how to setup a Poetry apps that are organized
in a monorepo-ish fashion.

Lets say you have a subproject, `project_b` that depends on `project_a`. You would
add it on `project_b/pyproject.toml` as:
```
project_a  = { path = "../project_a", develop = true }
```

On your dockerfile for `project_b` all you have to is `COPY` the required local 
projects/folders used by it and then run `poetry install` from it.

# Running
1. Build the image: `docker build -t monorepo_test ../ --file Dockerfile`
2. Run: `docker run -it --name monorepo_test --rm monorepo_test`

Step 2 will drop you directly into the container. You can test that `project_b` was
installed correctly by firing up python and trying to import a function from it.
Note that the function on the example below depends itself on a function defined on
`project_a`

```python
from project_b import add_multiply

add_multiply(2, 3)  # should return 11 -> 2*3 + 2 + 3
```
