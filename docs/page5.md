Pages (left) refer to [youtube video](https://www.youtube.com/watch?v=0jPclM5fALs) parts

# 5. Modify Workflow and commit changes, deployment

07:49 - end

## Requirements:

## Exercise 1:

### Task 2 (modified)

1.  Remove unnecessary file to avoid some errors:

    - Go to Code tab in Github
    - Navigate to `.github/workflows/dotnetcore.yml`
    - Click on `...` menu (top right)
    - Click on `Delete file`
    - Click on `Commit Changes` button

2.  Update `eshoponweb-cicd.yml`

    - Navigate to `.github/workflows/eshoponweb-cicd.yml`
    - Uncomment line 4: `on: [push, ...]`

    - Add id-token permissions:  
      Add this after `on:` line

          ```yml title="eshoponweb-cicd.yml"
          permissions:
            contents: read
            id-token: write
          ```

    - Update `env:` section:

          - Remove line with `SUBSCRIPTION-ID`, it should be a secret
          - For `RESOURCE-GROUP`, use `rg-eshoponweb-federated`, as in command line, previously
          - For `WEBAPP-NAME`, use a globally unique name, i.e. `eShop-unique-1546`

    - In the `login` step:

          - remove `creds:` key line
          - add:

              ```yml title="eshoponweb-cicd.yml"
              client-id: ${{ secrets.AZURE_CLIENT_ID }}
              tenant-id: ${{ secrets.AZURE_TENANT_ID }}
              subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
              ```

    - In the `deploy` step:

          - substitute `env.SUBSCRIPTION-ID` with `secrets.AZURE_SUBSCRIPTION_ID`

    - Commit changes

### Task 3

1.  Go to `Actions` menu in Github
2.  Go to the URL of the App in the browser
