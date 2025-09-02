# CI/CD Assessment Solution

## Build_package.yml
- uses of checkout code and Python setup was in a single step which causing the issue. It was seperated in 2 steps as a fix
- In Build package config for building a whl package was missing 
    * pyproject.toml added with package name and version
    * following command added to the Github workflow <sup>python -m build</sup> 
