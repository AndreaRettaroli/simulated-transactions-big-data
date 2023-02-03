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