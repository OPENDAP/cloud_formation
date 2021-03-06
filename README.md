
This directory contains AWS Cloud Formation templates that build
various sorts of AMIs that run the Hyrax web server. Current versions
use the RPM packages stored on S3 or www.OPeNDAP.org and support
CentOS7 and RedHat7. The 'gitHyraxCentos7.json' templete builds a 
machine setup for a source buid using the 'hyrax' GitHub repo.

To use these templates with AWS, goto the CloudFormation services page
and choose 'Create Stack' on the upper left-hand corner. The only
parameters that need to be set are the Stack Name (choose something
innocuous like 'Hyrax-01') and the EC2 KeyPair to enable SSH access to
the instance (I used our 'test' key). After that, the web interface
prompts for a number of optional parameters; the defaults for these
are fine.

Each of the templates will name the AMI (i.e., the name that shows up
in the AWS console) using the value of Tags key Name

To make a CentOS7 AMI from your local machine using the AWS cli tools,
use:

    aws cloudformation deploy --template-file snapshotHyraxTemplateCentos7.json \
        --stack-name Hyrax-8 --parameter-overrides KeyName=opendap-test-aws-east-2017

Note that the PEM file name lacks the '.pem' extension.

Also, just a bit of a reminder WRT 'aws' and credentials, if your ~/.aws/credentials
file lists a public and private key you want to use under a profile, you should
provide that and the region, like this:

    aws --profile jimg --region us-east-1 cloudformation deploy \
        --template-file gitHyraxCentos7.json --stack-name Hyrax-git-01 \
        --parameter-overrides KeyName=opendap-test-aws-east-2017
        
KeyName is the name of the pem file used to grant access to the host your building,
the --profile and --region are used by the 'aws' command line client.

The AMI instance numbers were fund using the Cloud Market site:
https://thecloudmarket.com. 

Amazon has a set of utilities that can be installed by yum. Look at this
page: https://github.com/OPENDAP/cloud_formation.

The zip file holds a collection of example files that show all kinds
of ways this service can be used.

