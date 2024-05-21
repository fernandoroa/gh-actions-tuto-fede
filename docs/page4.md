Pages (left) refer to [youtube video](https://www.youtube.com/watch?v=0jPclM5fALs) parts

# 4. Add Secrets to Github and Create Federated ID

06:08 - 07:48

## Requirements:

5.  xclip or equivalent

        ❯ sudo apt install xclip

6.  nano editor or any text editor

## Exercise 1:

### Task 1 (CLI equivalent of steps 9 to 11)

8.  Copy SECRETS to the clipboard and paste them in Github:

    - paste the AZURE_SUBSCRIPTION_ID value in Github / Settings / Secrets and Variables / Actions

            ❯ echo $AZURE_SUBSCRIPTION_ID | xclip -selection clipboard

    - paste the APP_ID value as AZURE_CLIENT_ID in Github / Settings / Secrets and Variables / Actions

            ❯ echo $APP_ID | xclip -selection clipboard

    - paste the AZURE_TENANT_ID value in Github / Settings / Secrets and Variables / Actions

            ❯ echo $AZURE_TENANT_ID | xclip -selection clipboard

9.  Create the federated Identity

    - create the credential.json file

            ❯ nano credential.json

    - Content: (update with your repository data)

          ```json title="credential.json"
          {
            "name": "federated_id",
            "issuer": "https://token.actions.githubusercontent.com",
            "subject": "repo:fernandoroa/eShop:environment:Development",
            "description": "Testing",
            "audiences": ["api://AzureADTokenExchange"]
          }
          ```

    - Federated identity command:

          ```sh
          ❯ az ad app federated-credential create --id $APP_ID --parameters credential.json > federated.json
          ```
