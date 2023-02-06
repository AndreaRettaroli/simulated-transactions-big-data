# simulated-transactions-big-data

### Simulated Transactions - Project

The goal of this notebook is to analyze and extract some useful informations from [kaggle simulated-transactions dataset](https://www.kaggle.com/datasets/conorsully1/simulated-transactions) using [EMR(Amazon Elastic MapReduce)](https://aws.amazon.com/it/emr/?nc=sn&loc=0), [Apache Spark](https://spark.apache.org/) and [scala](https://www.scala-lang.org/).

### Dataset description

The dataset contains ~22GB of data that represents random transactions.
[Notebook used to generate data](https://github.com/conorosully/medium-articles/blob/master/src/transaction_data_generator.ipynb).

Transactions are generated for 75,000 customers and are classified into 12 expenditure types:

- Groceries
- Clothing
- Housing
- Education
- Health
- Motor/Travel
- Entertainment
- Gambling
- Savings
- Bills and Utilities
- Tax
- Fines

Each transaction is represented by 10 features/columns:

- <strong> CUST_ID</strong>: unique ID for every customer
- <strong> START_DATE</strong>: the month the customer started making transactions
- <strong> END_DATE</strong>: the month the customer stopped making transactions
- <strong> TRANS_ID</strong>: unique ID for every transaction
- <strong> DATE</strong>: the date of the transaction
- <strong> YEAR</strong>: the year of the transaction
- <strong> MONTH</strong>: the month of the transaction
- <strong> DAY</strong>: the day of the transaction
- <strong> EXP_TYPE</strong>: the expenditure type (listed above)
- <strong> AMOUNT</strong>: the amount of the transaction (in dollars $)


# Setup cluster environment 

In this project I'm using the AWS Academy Virtual Lab with a 100$ credit. In the following sections there is described the general process.

### Enable SSH access to the Lab's machines using key pair

In the following classes you will be required to instantiate machines through the Lab and access them via SSH (e.g., Putty). In order to do it, you will need a Private Key Files (.ppk).

From the Console home, select the EC2 service, then go to "Network and security" > "Key pairs", then click on "Create a key pair":

- Put some name (e.g., "bigdata")
- Choose .ppk as the format
- Create the key pair > the .ppk file will be automatically downloaded
Do not lose it, or you will need to create a new key pair!

The downloaded .ppk file will be your Key pair.

### Create cluster

To create the cluster go to EMR service and create cluster using avanced settings following this steps:
- Software
    - Choose the latest EMR version
    - **Services: Hadoop, Hive, JupiterEnterpriseGateway, Spark, Livy**
    - After last step completes: Clusters enters waiting state
- Hardware
    - 1 Master node, On demand, m5.xlarge (default)
    - 2 Core nodes, On demand, m5.xlarge (default)
    - Disable automatic termination
- General
    - Name: whichever you prefer; the same name can be re-used several times
    - Enable log registration
- Security
    - Choose the *Key pair* created in the previous section.

### Connect via SSH and WinSCP to the master node

Once the cluster is up-and-running, you first need to allow SSH access to the master node of the newly created EMR cluster.

- From the *EMR service console*, open the list of created clusters, then open the cluster currently running
  - Located the "Master's Public DNS" in the Summary - it will be used later
  - Under "Security and Access", click on the security group of the master node (ElasticMapReduce-master)
    - In the newly opened page, select again the ID of the security group of the master node (ElasticMapReduce-master)
    - Click on "Edit inbound rules"
    - Add an SSH rule that allows connections to port 22 from your IPv4

Now open **Putty** and enter the following configuration.

- Host Name: hadoop@ec2-xxx-xxx-xxx-xxx.compute-1.amazonaws.com
  - Replace "xxx-xxx-xxx-xxx" with the IP address of the "Master's Public DNS"
- Under "Connection" > Expand "SSH" > "Auth", click "Browse" and select your *Key pair*
- Open the connection

Now open **WinSCP** and enter the following configuration (similar to Putty).

- Server: ec2-xxx-xxx-xxx-xxx.compute-1.amazonaws.com
- User name: hadoop
- Under "Advanced" > "SSH" > "Auth" > "credentials" enter your *Key pair*
- Open the connection

**Notice**: new clusters will be created in each of the following classes; thus, the IP of the Master's Public DNS will need to be changed as well (in both Putty and WinSCP). 

### Connect to services' GUIs through SSh tunnels

Many services (HDFS, YARN, Spark, etc.) expose GUIs with useful information, especially to monitor the execution of jobs and get interesting insights. To access them, SSH tunnels must be enable for each port.

Let XYZ be the port of a given service (e.g., 8088 for YARN's Resource Manager). Open Putty and enter the following configuration.

- Enter the same configuration from 201-2 (host name and key pair)
- Additionally, go to "Connection" > Expand "SSH" > "Tunnels"
  - Source port: XYZ
  - Destination: ec2-xxx-xxx-xxx-xxx.compute-1.amazonaws.com:XYZ
- Open the connection

The GUI is now available under [localhost:XYZ]()







The complete guide is available on [the repository of Prof.re Enrico Gallinucci](https://github.com/unibo-bigdata/lab-21-22)