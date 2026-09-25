# Get your own Exchange token

When you use the Hub, `JHE_TOKEN` is set for you. If you're using the [client library](xref:jh/glossary#term-client-library) from another computational environment, you'll need to generate a token and set `JHE_TOKEN` yourself.

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

4. Copy your token and Exchange URL. In your notebook, set them before creating a client:

   ```python
   from jupyterhealth_client import JupyterHealthClient
   
   JHE_URL = "https://<your-exchange-url>"
   JHE_TOKEN = "<your-token>"
   client = JupyterHealthClient(JHE_URL, token=JHE_TOKEN)
   ```

Tokens are time-limited, so create a new one when it expires.

:::{note} Don't share the token!
Treat the token like a password!
:::

