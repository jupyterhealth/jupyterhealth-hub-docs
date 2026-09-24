# Explore your data

Starting with a blank notebook, this page walks you through connecting to the JupyterHealth Exchange and viewing the data you can access.
It assumes you have [logged in and launched a session](log-in.md).

## Connect to the Exchange

Your Hub session provides two environment variables so the client can reach the Exchange using your account, without asking you to log in again:

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

Open a new notebook with {gui}`File --> New --> Notebook` and run the following code blocks in order:

```python
from jupyterhealth_client import JupyterHealthClient

client = JupyterHealthClient()
```

Tokens expire after a day.
If requests start failing, log out, log back in, and restart your server.

To use the client outside the Hub, [get your own token](get-a-token.md).

## Check your connection

Run this to see your user information:

```python
client.get_user()
```

## List studies and patients

Data is organized by organization, study, and patient.
List the studies you can access. You'll use one of these IDs in the next step:

```python
print("All my studies:")
for study in client.list_studies():
    print(f"  - [Study ID: {study['id']}] {study['name']} (org: {study['organization']['name']})")
```

Choose an ID from the list above and replace `<STUDY_ID>` before running this cell:

```python
study_id = <STUDY_ID>

client.get_study(study_id)
```

List the patients in that study:

```python
print("Patients in this study:")
for patient in client.list_patients(study_id=study_id):
    print(f"  - [Patient ID: {patient['id']}] {patient['nameGiven']} {patient['nameFamily']}")
```

## View patient data

Choose a patient ID from the list above and replace `<PATIENT_ID>` before running this cell. This example retrieves blood glucose observations:

```python
from jupyterhealth_client import Code

patient_id = <PATIENT_ID>

df = client.list_observations_df(
    patient_id=patient_id,
    study_id=study_id,
    code=Code.BLOOD_GLUCOSE
)
df.head()
```

If the DataFrame is empty, this patient may not have blood glucose data available for this study. Check their consent with `client.get_patient_consents(patient_id=patient_id)`, or try another patient or data code.

For an example of glucose metrics and plots, see the [CGM tutorial](https://jupyterhealth.github.io/software-documentation/tutorial/tutorial-cgm).
The study and patient IDs in that tutorial are illustrative, so its code won’t run as written. Replace them with IDs from your own study.
The [client API reference](https://jupyterhealth-client.readthedocs.io) lists the other data codes and methods.
