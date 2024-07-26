
# Enable Google OAuth Scopes on Cloud Composer

Ref: https://stackoverflow.com/questions/69817236/enable-google-drive-oauth-scopes-on-cloud-composer-2-0


1.  Create a [Google Cloud Airflow Connection](https://cloud.google.com/composer/docs/how-to/managing/connections#creating_a_connection_to_another_project)
    -   Name the Connection
    -   Specify a Service account key file path or JSON
    -   Specify the scopes you need to use to preform your task. (<https://www.googleapis.com/auth/spreadsheets>)
2.  Within your DAG, where you call on the operator to build the task, include the [parameter](https://airflow.apache.org/docs/apache-airflow-providers-google/stable/_api/airflow/providers/google/cloud/transfers/sheets_to_gcs/index.html#airflow.providers.google.cloud.transfers.sheets_to_gcs.GoogleSheetsToGCSOperator):
    -   **gcp\_conn\_id** \= '< name of connection >'

Cloud Composer v2 doesn't support OAuth on the Environment Level anymore because it now uses GKE Autopilot. 
GKE Autopilot does not support OAuth since this is a [legacy method](https://cloud.google.com/compute/docs/access/service-accounts#accesscopesiam) of GCE. 
For the connections that still need OAuth you will need to define these in an Airflow Connection and use the connection in your task. 
The scope of the connection seems to override and preexisting scopes that may be included by default, like the full `cloud-platform` scope. 
I had to specify both `spreadsheets` and `cloud-platform` in my connection for the [sheets\_to\_gcs](https://airflow.apache.org/docs/apache-airflow-providers-google/stable/_api/airflow/providers/google/cloud/transfers/sheets_to_gcs/index.html#airflow.providers.google.cloud.transfers.sheets_to_gcs.GoogleSheetsToGCSOperator) operator.
