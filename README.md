# Pipeline-deployment

![alt text](https://github.com/Malvearun/unknown/blob/master/Pipeline.jpg "pipeline")

Using sample node.js application in GitHub, setup the pipeline so that whenever we commit the any changes to application and GitHub it will trigger the AWS code pipeline instance to start the deployment process. This will deploy the application on target server which will setup an AWS elastic beanstalk, code will live on EC2 instance. This is one stage pipeline.

AWS Elastic Beanstalk is an easy to use service. Deployment implementation is faster and managed application uploaded to AWS cloud. Application which are developed in languages Java, Python, Go, etc., Application server platform like Apache Tomcat, Nginx etc.,
Note: Developers can focus on writing code and can run on Elastic BeanStalk, it will handle the deployment, provision, Load balancing, auto-scaling and health monitoring.
Cost: It will cost only for EC2 instance and S3 bucket resources.

#### Creating and deploying Elastic Beanstalk with Tomcat:

Tomcat is a Java HTTP web server environment, in which Java code can run. There is implementation of Java Servlet, JavaServer pages (jsp), Java Expression Language, Websocket technologies. IT is an open-source software which is licensed under Apache.
Reference link: https://www.apache.org/licenses/

Elastic BeanStalk Tomcat platform runs on Java web application. Below are the steps to follow in setting up the infrastructure for Tomcat web-based application through Elastic beanstalk.

#### Creating and deploying Elastic Beanstalk with Tomcat:

•	Login to AWS Console &rarr; Service &rarr; Elastic BeanStalk &rarr; Create Application  &rarr; Get Started 

•	Create environment &rarr; Select Web server environment 

•	Environment / Application Name: `Hello-Tomcat`

•	Domain: will replace with same `Environment Name`

•	**Base Configuration**: 

1.	Platform: PreConfigured platform – EC2 instance will be create and tomcat will be added to the container.

2.	Select `Tomcat`, Platform branch and Platform version can be selected has per the project requirement.

•	**Application Code**:

o	Select `upload you code` &rarr; browse the source file `S3 URL` or locally &rarr; under `target` folder &rarr; .war file &rarr; upload 

o	Reference files for the project are injected in GitHub repository: https://github.com/Malvearun/AWS-BeanStalk-Tomcat.git

o	Should see it will be tagged with the name.

o	Click on `Create application /environment`.


It will create AWS beanstalk environment with ec2 along with the code is deployed. This is how it will deploy our application by creating a new configuration from scratch.

•	While creating the application it will create elastic beanstalk instance and create EC2 instance and deploys the web application.

•	Creation of the `Security Group` it is part of creation environment to secure the EC2 instance inside the Beanstalk so can have specific groups connected to a particular EC2 who can login to the instance.

•	Auto Scaling configuration will be created. followed by creating CloudWatch alarm.

•	Created the EIP address configure in Elastic loadbalncer, so request is routed to the web application.

•	Springboot application will be in process, inside the tomcat will be coming up.

•	Last step should be able to see the URL, access the web servers. URL is Elastic load balancing, it will redirect the request to web application where our application is deployed. Click on it – should there will be an error.

•	Successfully Launched environment:

From url link `http://hellotomcat-env.eba-w2g3zzhm.us-east-1.elasticbeanstalk.com/` followed with `hello` or ` actuator/health` should be working

#### CodePipeline:

•	AWS &rarr; services &rarr; Code Pipeline &rarr; create Pipeline &rarr;

o	Pipeline name**: Hello-Tomcat
o	Service role: New service role
o	Default location: it will store in S3 bucket.

Leave other settings in default and click on Next

•	**Source stage**:

Source provider: `GitHub` and click on `connect`. Select the repository with branch.
How pipeline will be trigger: GitHub web hooks and click on Next

•	**deploy stage**: 

o	Deploy provider: AWS Elastic Beanstalk
o	Region: eu-central-1
o	Application name: Hello-Tomcat
o	Environment name: Hello-Tomcat-env-1
o	click on Next
o	Review and create pipeline, it will be created. Should see `successful congratulations`.

•	**Deploy**: Click on `AWS Elastic Beanstalk output` &rarr; click on the environment `Hello-Tomcat-env-1` &rarr; click on the `http://Hello-Tomcat-env-1.eba-w2g3zzhm.eu-central-1.elasticbeanstalk.com/` followed with more information on page. Should see it is working.

![alt text](https://github.com/Malvearun/unknown/blob/master/Page.jpg "Browser page")

## Creating and deploying Elastic Beanstalk with Node.js:

•	Login to AWS Console &rarr; Service &rarr; Elastic BeanStalk &rarr; Create Application  &rarr; Get Started 

•	Create environment &rarr; Select Web server environment 

•	Environment / Application Name: `Hello-web-app`

•	Domain: will replace with same `Environment Name`

•	Base Configuration: 
1.	**Platform**: PreConfigured platform – EC2 instance will be create and tomcat will be added to the container.
o		Select `**node.js**`, Platform branch and Platform version can be selected has per the project requirement.

2.	**Application Code**:
o	Select `simple application`
o	Click on `Create application /environment`.

It will create AWS beanstalk environment with ec2 along with the code is deployed. This is how it will deploy our application by creating a new configuration from scratch.

First, we created an environment with node.js, elastic beanstalk has create a sample application, in Overview you will not be see much information what is happening in background. Not required to write any scripts for build like example npm install, basically elastic beans will find the package with json format and execute in the root. The process is automated process. Successfully Launched environment:

•	Elastic Beanstalk &rarr; Dashboard &rarr; follow the `Overview` page with other components `Health` to see the status. 

•	From url link `http:// Hello-web-app-env.eba-w2g3zzhm.eu-central-1.elasticbeanstalk.com/` followed with more information on page.

#### CodePipeline:
•	AWS &rarr; services &rarr;  Code Pipeline &rarr; create Pipeline &rarr; 

o	Pipeline name: hello-web-app 

o	Service role: New service role 

o	Default location: it will store in S3 bucket.

Leave other settings in default and click on Next

•	**Source stage**:

Source provider: `GitHub` and click on `connect` . Select the repository with branch.

How pipeline will be trigger: GitHub web hooks and click on Next

•	**Deploy stage**: 
o	Deploy provider: AWS Elastic Beanstalk

o	Region: eu-central-1

o	Application name: Hello-web-app

o	Environment name: Hello-web-app-env-1

o	click on Next

o	Review and create pipeline, it will be created. Should see `successful congratulations`.

•	**Deploy**: Click on `AWS Elastic Beanstalk output` &rarr; click on the environment `Hello-web-app-env-1` &rarr; click on the `http://Hello-web-app-env.eba-w2g3zzhm.eu-central-1.elasticbeanstalk.com/` followed with more information on page. Should see it is working.

•	Let’s see the change in application code and see if it triggers, same has in production.

•	Let’s add health check url to see if the code pipeline is working has expected. 
