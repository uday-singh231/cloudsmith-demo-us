# CI/CD Assessment Solution

## Build_package.yml
- In Build package step there was no step to perform added `pip install build` to the step
- In Build package config for building a whl package was missing 
    * pyproject.toml added with package name and version
    * following command added to the Github workflow `python -m build`
  <br>
 ## Release_package.yml
- In cloudsmith namespace, created 2 repo staging and prod.
- Created and added service to the repo access control with write permission
- Enable OIDC for this service and added github action as provider
- Added namespace and service slug as repo variables in github
- in yml file:
     * In Permissions section, added `id-token: write`
     * Added Action for cloudsmith-io/cloudsmith-cli-action@v1.0.3
     * for OIDC auth added namespce/workspace and service slug vars in with section.
   <br>
## Promote_package.yml
- Configure webook in Staging repo
- Changed `workflow_disptach` to `repository_dispatch` and configure trigger event.
- Changed following command from `cloudsmith list package ${{ env.CLOUDSMITH_NAMESPACE }}/${{ env.CLOUDSMITH_STAGING_REPO }} -q "$PACKAGE_QUERY" -F json` to `PACKAGE_ID=$(cloudsmith list packages ${CLOUDSMITH_NAMESPACE}/${CLOUDSMITH_STAGING_REPO} -q "$PACKAGE_NAME" --output-format json | jq -r '.data[0].identifier_perm')`
- Added command to list all vars for ready-for-production tag `cloudsmith list packages ${CLOUDSMITH_NAMESPACE}/${CLOUDSMITH_STAGING_REPO} -q "tag:ready-for-production" --output-format json | jq -r '.data[0].identifier_perm'`
