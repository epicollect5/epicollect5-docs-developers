# Create Client App

In order to access a private project's resources via the API, you can **create a project App**. This is suitable for machine-to-machine authentication, for example in a scheduled job which is performing tasks over the API.

In order to create a project App, you must login to Epicollect5 and either create a new project or access the details page for an existing project. From here, select the 'Apps' menu option on the left hand side and click 'Create New App'. Enter your 'App Name' and click 'Create'.

You will need to make a note of your **Client ID** and **Client Secret**, which are used when requesting access tokens.

PLEASE NOTE: currently only one project App may be created per project and anyone who has access to the project details page may add or remove a project App (the project Creator and project Managers).

## Revoke Token

If, for whatever reason, you need to revoke a live `access_token` (for example if you suspect the token has been compromised), you can revoke a token via the 'Revoke Token' button on the project App from the 'Apps' page on the project details page.

## Delete App

You can delete a project App at any time, via the 'Delete' button on the project App from the 'Apps' page on the project details page.

## Further Information

The Epicollect5 Client Credentials Grant flow is based on Laravel Passport's implementation:

[https://laravel.com/docs/5.4/passport](https://laravel.com/docs/5.4/passport)
