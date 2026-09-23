# Run a simple analysis

This walks through pulling data from the JupyterHealth Exchange into a notebook.
It assumes you have [logged in and launched a session](log-in.md).

## Connect to the Exchange

Your server starts with two environment variables so the client can reach the Exchange as you, without logging in again:

```{list-table}
:header-rows: 1

* - Variable
  - Meaning
* - `JHE_URL`
  - URL of the JupyterHealth Exchange the Hub is connected to
* - `JHE_TOKEN`
  - Your access token for that Exchange
```

The [client library](https://jupyterhealth-client.readthedocs.io) reads these automatically.
Open a new notebook with {gui}`File --> New --> Notebook` and run:

```python
from jupyterhealth_client import JupyterHealthClient

client = JupyterHealthClient()
```

Tokens expire after a day.
If requests start failing, log out, log back in, and restart your server.

To use the client outside the Hub, [get your own token](get-a-token.md).

## Find a study and a patient

Data is organized by organization, study, and patient.
List the studies you can see, then the patients in one of them:

```python
for study in client.list_studies():
    print(study["id"], study["name"])

study_id = 30006  # pick one from above

for patient in client.list_patients(study_id=study_id):
    print(patient["id"], patient["nameFamily"], patient["nameGiven"])
```

Only patients who have consented to share data with the study will have data available.
Check with `client.get_patient_consents(patient_id)`.

## Load observations into a DataFrame

```python
from jupyterhealth_client import Code

df = client.list_observations_df(
    patient_id=40006,  # pick one from above
    study_id=study_id,
    code=Code.BLOOD_GLUCOSE,
    limit=10_000,
)
df.head()
```

For a full worked example, including glucose metrics and plots, run the [CGM tutorial](https://jupyterhealth.github.io/software-documentation/tutorial/tutorial-cgm).
The [client API reference](https://jupyterhealth-client.readthedocs.io) lists the other data codes and methods.
