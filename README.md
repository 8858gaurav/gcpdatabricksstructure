Go to catalog page on databricks UI -> go to credentials (under connect sections) -> create credentials for GCP: this will give you a service principal for DB , e.g : db-uc-credential-06f9g6iang-qc@uc-asias1.iam.gserviceaccount.com
now give the access of your gcp bucket to this service principal (db-uc-credential-06f9g6iang-qc@uc-asias1.iam.gserviceaccount.com)

create an external locations(input_path, output_path, deltatable -> for gcp buckets) on databricks to read the contents from GCP accounts by using your credentials.


on github UI -> setting -> developer settings -> PAT(personal access token) -> Tokens(Classics)
databricks-gcp-token: XXXXXXX

On databricks UI -> setting -> linked accounts -> add your git credentials and PAT toekn here.
On databricks UI -> workspace -> create -> Git folder -> passed your Github Repo

