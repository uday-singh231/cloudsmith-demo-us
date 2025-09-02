# CI/CD Assessment Solution

## Build_package.yml
- uses of checkout code and Python setup was in a single step which causing the issue. It was seperated in 2 steps as a fix
- In Build package config for building a whl package was missing 
    * pyproject.toml added with package name and version
    * following command added to the Github workflow `python -m build`
  <br>
 ##Release_package.yml
- In cloudsmith namespace, created 2 repo staging and prod.
- Created and added service to the repo access control with write permission
- Enable OIDC for this service and added github action as provider
- Added namespace and service slug as repo variables in github
- in yml file:
     * In Permissions section, added `id-token: write`
     * Added Action for cloudsmith-io/cloudsmith-cli-action@v1.0.3
     * for OIDC auth added namespce/workspace and service slug vars in with section.
<br>
