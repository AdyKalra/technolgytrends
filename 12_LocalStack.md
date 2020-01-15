## LocalStack

```One of the challenges of using cloud services is being able to``` **develop and test locally.** 

[LocalStack](https://github.com/localstack/localstack) solves this problem for [AWS](https://www.thoughtworks.com/radar/platforms/aws) by providing local [test double](https://martinfowler.com/bliki/TestDouble.html) implementations of a wide range of AWS services **including S3, Kinesis, DynamoDB and Lambda.** 

It builds on top of best-of-breed tools such as [Kinesalite,](https://github.com/mhart/kinesalite) [dynalite](https://github.com/mhart/dynalite) and [Moto](https://github.com/spulec/moto) and adds isolated processes and error injection functionality. 

```LocalStack is very easy to use, ships with a simple JUnit runner and a JUnit 5 extension and can also``` **run inside a docker container.** ```For many teams, it has become the default for testing services that are deployed on AWS.```
