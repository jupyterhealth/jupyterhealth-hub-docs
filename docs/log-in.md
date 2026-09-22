# Log in and launch a session

:::{important} You'll need an Exchange account
The Hub logs you in through the JupyterHealth Exchange, so you need an Exchange account first.
See [Sign up for the Exchange](sign-up.md).
:::

## Log in

1. Go to <https://jupyter-health.2i2c.cloud> and click {guilabel}`Log in to continue`.

   ```{figure} images/hub-login.png
   :alt: The Hub landing page with a Log in to continue button
   :width: 500px
   ```

2. You are sent to the JupyterHealth Exchange.
   Enter the email address and password of your [Exchange](xref:jh/glossary#term-exchange) account and click {guilabel}`Log In`.

   ```{figure} images/exchange-login.png
   :alt: The JupyterHealth Exchange log in form
   :width: 300px
   ```

3. You are sent back to the Hub, which starts your server.

% We need a more user-friendly documentation of organizations in JHE!
Access is granted by membership in a [JupyterHealth Exchange organization](xref:jhe/jhe/access-control#organization-hierarchy-and-authority).
If you don't have an account, [sign up for the Exchange](sign-up.md), then ask your study or organization administrator to add you to their organization.

:::{note}
% We need a more user-friendly documentation of organizations in JHE!
If you get an error after logging in, you are probably not in an organization yet.
See the [Exchange access control docs](xref:jhe/jhe/access-control) for how accounts, roles, and organizations work.
:::

## Launch a session

After you log in, the Hub starts a JupyterLab server for you.
It might take a minute or two!

## User environment

The server runs the [JupyterHealth environment image](https://github.com/jupyterhealth/singleuser-image), which has Python, the [client library](xref:jh/glossary#term-client-library), Jupyter AI, and common data science libraries pre-installed.

**Packages you install with `pip` will not persist across sessions!** If you must `pip install`, put `%pip install ...` at the top of notebooks that need extra packages.

## Storage

Your home directory persists between sessions.
Add and edit whatever files you like, but try to keep file size down.

## Stop your session

When you're done, choose {menuselection}`File --> Hub Control Panel --> Stop My Server` so your server stops using cloud resources.

If you leave your Hub session idle for long enough, it will be shut down automatically.

## Get help

- Problems with the Hub itself (login loops, server won't start): use the [2i2c support process](xref:2i2c#support).
- Questions about JupyterHealth data or the Exchange: ask in [Zulip](xref:jh/glossary#term-zulip).
