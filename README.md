This repository provides a layer for AWS Lambda to support the
python 3.8 pandas library. It places the libraries into the right
places in the Linux filesystem as seen from your lambda function.

To use it:
1. Upload the layer file pandas.zip to an S3 bucket
2. Upload the layer file from S3 into your lambda execution environment by
using the AWS CLI command

aws lambda publish-layer-version --layer-name pandas-layer --description "pandas layer" --content S3Bucket=<S3bucketname>,S3Key=pandas.zip --compatible-runtimes python3.8
(A sample S3 bucketname is myproj-5fu41htku3jr)

3. In the AWS Lambda console, use "Add A Layer", choose Custom Layer, and
find pandas-layer, and specify version 1. You will see its ARN, like
arn:aws:lambda:us-east-1:317555515996:layer:pandas:1

4. You can specify use of the layer in serverless.yml for a lambda function
using this ARN, for ex.:
functions:
  create:
    handler: records/create.create
    layers:
      - arn:aws:lambda:us-east-1:668099181075:layer:AWSLambda-Python38-SciPy1x:29
      - arn:aws:lambda:us-east-1:317555515996:layer:pandas-layer6:1
     ...

Thanks to Stack Overflow 43877692 and 55695187
"# pandas" 
