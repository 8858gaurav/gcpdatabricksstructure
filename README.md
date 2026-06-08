Go to catalog page on databricks UI -> go to credentials (under connect sections) -> create credentials for GCP: this will give you a service principal for DB , e.g : db-uc-credential-06f9g6iang-qc@uc-asias1.iam.gserviceaccount.com
now give the access of your gcp bucket to this service principal (db-uc-credential-06f9g6iang-qc@uc-asias1.iam.gserviceaccount.com)

create an external locations(input_path, output_path, deltatable -> for gcp buckets) on databricks to read the contents from GCP accounts by using your credentials.


on github UI -> setting -> developer settings -> PAT(personal access token) -> Tokens(Classics)
databricks-gcp-token: XXXXXXX

On databricks UI -> setting -> linked accounts -> add your git credentials and PAT toekn here.
On databricks UI -> workspace -> create -> Git folder -> passed your Github Repo

================================================================================================

Step 1: Connecting Databricks to GitHub (Repos)

go to Github -> create Repos -> 
to generate token -> go to Github -> settings -> developer settings -> PAT -> tokens classic

go to databricks -> settings -> linked accounts -> add git credentials -> pass your token here & other stuffs
go to databricks -> settings -> development -> git url allow list -> paste your git repo url

go to databricks -> click on Workspace icon -> click on Workspace folder ->  select the Repos folder (under Workspace folder, you'll find the folder name as Repos) -> Create Git Folder -> ( give your repo link, select providers, git folder name)

=======================================================================================================================================

Step 2: Setting up the CI Folder Structure
creat .github (add yml script: databricks_ci.yml under github folder) and tests folder (add untit test python script: test_transformations.py under tests folder)
you need to create this .github folder, and test folder under your git folder name which you have created in step 1
or you can create this folder .github/test by using Gihub UI


e.g 
1. test_transformations.py files looks like as below:
# tests/test_transformations.py
def calculate_discount(price, discount):
    return price - discount

def test_calculate_discount():
    # This is a 'Unit Test'
    assert calculate_discount(100, 20) == 80
    assert calculate_discount(50, 50) == 0

2. add teh contents for databricks_ci.yml files.


now, if you push your code from databricks with the help of local branch, then merge the request on Github by creating a pull request: workflow under Github actions will run and it's name will be : Databricks Medallion CI
Where it's running : Github server VM, this serves also run our unit test cases: test_transformations.py

=======================================================================================================================================
how to Get Databricks PAT:
go to DB UI -> Settings -> Developer -> Acess token -> manage -> generate new token

DATABRICKS_TOKEN:
Go to your Repo Settings -> Secrets and variables -> Actions -> secrets tab -> New repository secret -> DATABRICKS_TOKEN -> paste your db personal access token
DATABRICKS_HOST:
Go to your Repo Settings -> Secrets and variables -> Actions -> click on Variable tab ->  New Repository Variable -> paste your db worskpace link

