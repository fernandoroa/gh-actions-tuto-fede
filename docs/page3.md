Pages (left) refer to [youtube video](https://www.youtube.com/watch?v=0jPclM5fALs) parts

# 3. Create App, Service Principal and Role

04:10 - 06:07

## Links

04:36 - [https://learn.microsoft.com/en-us/azure/developer/github/connect-from-azure?tabs=azure-cli%2Clinux](https://learn.microsoft.com/en-us/azure/developer/github/connect-from-azure?tabs=azure-cli%2Clinux)

## Exercise 1:

### Task 1 (CLI equivalent of steps 5 to 8)

4.  Provider:

    ```zsh
    ❯ az provider register --namespace Microsoft.Web
    ```

5.  Create App:

    - get `.json` file

          ```zsh
          ❯ export myApp=eShop
          ❯ az ad app create --display-name $myApp > app.json
          ```

    - get `APP_ID` from `.json` file

          ```zsh
          ❯ export APP_ID=$(awk 'BEGIN { FS="\""; RS="," }; { if ($2 == "appId") {print $4} }' app.json)
          ❯ echo $APP_ID
          ```

6.  Create the Service Principal:

    - get `.json` file

          ```zsh
          ❯ az ad sp create --id $APP_ID > service.json
          ```

    - get `SP_ID` from `.json` file

          ```zsh
          ❯ export SP_ID=$(awk 'BEGIN { FS="\""; RS="," }; { if ($2 == "id") {print $4} }' service.json)
          ❯ echo $SP_ID
          ```

7.  Create Role Assignment:

    ```zsh
    ❯ az role assignment create --role contributor --subscription $AZURE_SUBSCRIPTION_ID \
    --assignee-object-id $SP_ID --assignee-principal-type ServicePrincipal \
    --scope /subscriptions/$AZURE_SUBSCRIPTION_ID/resourceGroups/$AZURE_ESHOP_RESOURCE_GROUP > role.json
    ```
