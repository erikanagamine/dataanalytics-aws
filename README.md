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
