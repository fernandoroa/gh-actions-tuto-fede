Pages (left) refer to [youtube video](https://www.youtube.com/watch?v=0jPclM5fALs) parts

# 2. Create Resource Group and System Variables

01:55 - 04:09

## Links

02:32 - [https://learn.microsoft.com/en-us/azure/app-service/quickstart-multi-container](https://learn.microsoft.com/en-us/azure/app-service/quickstart-multi-container)  
04:03 - [https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt)

## Requirements:

4.  Azure CLI

    - [https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt)

## Exercise 1:

### Task 1 (CLI equivalent)

1.  login to Azure CLI:

    - create .json file

          ```zsh
          ❯ az login > login.json
          ```

    - continue login process on browser
    - contents of .json

          ```zsh
          ❯ cat login.json
          ```

2.  Save secrets locally (these SECRETS are for later):

    - From .json to system variable:

          ```zsh
          ❯ export AZURE_SUBSCRIPTION_ID=$(awk 'BEGIN { FS="\""; RS="," }; { if ($2 == "id") {print $4} }' login.json)
          ❯ echo $AZURE_SUBSCRIPTION_ID
          ```

    - From .json to system variable:

          ```zsh
          ❯ export AZURE_TENANT_ID=$(awk 'BEGIN { FS="\""; RS="," }; { if ($2 == "tenandId") {print $4} }' login.json)
          ❯ echo $AZURE_TENANT_ID
          ```

3.  Create Resource Group

    - Save name to system variable:

          ```zsh
          ❯ export AZURE_ESHOP_RESOURCE_GROUP=rg-eshoponweb-federated
          ❯ echo $AZURE_ESHOP_RESOURCE_GROUP
          ```

    - Create group:

          ```zsh
          ❯ az group create --name $AZURE_ESHOP_RESOURCE_GROUP --location "South Central US" > group.json
          ```
