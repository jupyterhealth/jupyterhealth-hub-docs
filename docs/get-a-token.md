# Get your own Exchange token

The Hub sets `JHE_TOKEN` for you, so you only need this to use the [client library](xref:jh/glossary#term-client-library) somewhere else, like your own laptop.

1. [Log in to the Exchange](sign-up.md) in your browser and open {guilabel}`Data Portal`.

2. Click your user email in the bottom left, then {guilabel}`Profile`.

   ```{figure} images/exchange-user-menu.png
   :alt: The user menu at the bottom left of the Data Portal, with Profile and Log Out options
   :width: 250px
   ```

3. Under {guilabel}`Generate Bearer Token`, click {guilabel}`Create New` and copy the token.

   ```{figure} images/exchange-profile-token.png
   :alt: The User Profile page, with a Create New button under Generate Bearer Token
   :width: 400px
   ```

4. Set them as **environment variables** called `JHE_TOKEN` and `JHE_URL`, before creating a client:

   ```bash
   export JHE_URL=https://<your-exchange-url>
   export JHE_TOKEN=<your-token>
   ```

When you create a new Exchange Client, it should use these tokens from the environment variables to connect.

Tokens are time-limited, so create a new one when it expires.

:::{note} Don't share the token!
Treat the token like a password!
:::

