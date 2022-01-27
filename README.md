# dataanalytics-aws

```
sudo yum install -y aws-kinesis-agent
wget http://media.sundog-soft.com/AWSBigData/LogGenerator.zip
unzip LogGenerator.zip
chmod a+x LogGenerator.py
sudo mkdir /var/log/cadabra
cd /etc/aws-kinesis/
sudo vi agent.json

{
  "cloudwatch.emitMetrics": true,
  "kinesis.endpoint": "",
  "firehose.endpoint": "firehose.us-west-2.amazonaws.com",

  "awsAccessKeyId":"",
  "awsSecretAccessKey":"",

  "flows": [
    {
"filePattern": "/var/log/cadabra/*.log",
"deliveryStream": "PurchaseLogs"
    }
  ]
}

sudo service aws-kinesis-agent start

sudo chkconfig aws-kinesis-agent on

cd ˜
sudo ./LogGenerator.py 500000
cd /var/log/cadabra/
ls

tail -f /var/log/aws-kinesis-agent/aws-kinesis-agent.log 


```
Firehose:

```
cd /etc/aws-kinesis/

sudo vi agent.json 

[ec2-user@ip-172-31-18-110 aws-kinesis]$ cat agent.json 
{
  "cloudwatch.emitMetrics": true,
  "kinesis.endpoint": "kinesis.us-west-2.amazonaws.com",
  "firehose.endpoint": "firehose.us-west-2.amazonaws.com",
  
  "awsAccessKeyId": "",
  "awsSecretAccessKey": "",

  "flows": [
    {
      "filePattern": "/var/log/cadabra/*.log",
      "kinesisStream": "CadabraOrders",
      "partitionKeyOption": "RANDOM",
      "dataProcessingOptions": [
        {
  "optionName": "CSVTOJSON",
  "customFieldNames": ["InvoiceNo", "StockCode", "Description", "Quantity", "InvoiceDate", "UnitPrice", "Customer", "Country"]
}
      ]
    },
    {
      "filePattern": "/var/log/cadabra/*.log",
      "deliveryStream": "PurchaseLogs"
    }
  ]

sudo service aws-kinesis-agent restart

```

EMR:

```
Conectar no  EMR:
cp /usr/lib/spark/examples/src/main/python/ml/als_example.py ./

hadoop fs -mkdir -p /user/hadoop/mllib/als

hadoop fs -copyFromLocal /usr/lib/spark/data/mllib/als/sample_movielens_ratings.txt /user/hadoop/mllib/als/sample_movielens_ratings.txt

spark-submit als_example.py

```
