# S3 Thumbnail Generator

This sample is an implementation of the image thumbnail generation sample (adapted from the [AWS documentation](https://docs.aws.amazon.com/lambda/latest/dg/with-s3-example-deployment-pkg.html#Node.js)) on top of the Sigma IDE.

## Prerequisites

All deployments of this application are based on Amazon AWS. You can open the project using the [Sigma IDE](https://sigma.slappforge.com). You can [create an account] and provide your AWS credentials to open the project (Your AWS credentials will not be acquired by SLAppForge under any circumstances).

Once you have completed the signup process, select the `s3-thumbnail-generator` option under the *Samples* option on the [*Project* page](https://sigma.slappforge.com/#/project). If you are already inside an open project, you can use the *Change Project* toolbar button instead.

## Use Case Description

Similar to the [original AWS sample](https://docs.aws.amazon.com/lambda/latest/dg/with-s3-example-deployment-pkg.html#Node.js), sample picks up image files placed in an S3 bucket, converts them into thumbnails, and uploads them into another S3 bucket. It uses `imageMagick` from the [`gm`](https://www.npmjs.com/package/gm) library for the thumbnail generation step, and the standard [AWS JavaScript SDK](https://aws.amazon.com/sdk-for-node-js/) for file uploads and downloads. In addition to the original sample, this sample makes the uploaded thumbnails files publicly readable using the [`acl` parameter of the `putObject` S3 operation](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/S3.html#putObject-property).

## Getting Started

In order to get started, simply open the sample project from the Sigma IDE.

Because bucket names in S3 are globally unique, you will have to change the bucket name used in the sample, in order to avoid conflicts during deployment. For this,

1. Update the triggers of the lambda function to point to the correct source bucket.
* click the *Manage Triggers* icon (the green circle with a lightning icon) on the left margin of the code editor (line 20),
* click on each of the two triggers in turn (to open the trigger editor pop-up),
* select *New Bucket*,
* enter a desired name for the source bucket, and
* click *Update*.

Alternatively, you can also select an existing bucket on your AWS account, using the *Existing Bucket* option.

2. Update the source bucket in the application code to point to the new bucket name.
* click the *Edit Operation* icon (the small red S3 icon) on the left margin of the code editor near the `s3.getObject` call (line 45),
* select *Existing Bucket* (since you already defined it under the trigger), and
* select the bucket name that you entered earlier, for the trigger, and
* click *Update*.

3. Update the destination bucket in the application code to point to a new bucket name.
* click the *Edit Operation* icon (the small red S3 icon) on the left margin of the code editor near the `s3.putObject` call (line 73),
* select *New Bucket* (or *Existing Bucket* if you want the thumbnails to be saved into an already existing bucket on your account),
* enter (or select) the destination bucket name, and
* click *Update*.

## Deployment

Once you are done, click the *Deploy Project* toolbar button. Since you have made changes in the project, the IDE will commit a copy of the project into a repository on your own GitHub account, so that you can keep on playing with the source code to get familiar with the application later on.

Once you provide a commit message and click *Commit*, the IDE will automatically commit and build the project, and finally show a *Changes Summary* pop-up so that you can review the deployment configuration of the project on the AWS side. Clicking *Execute* on this pop-up will start the deployment process.

## Testing

After the deployment, you can test the sample application by simply dropping a JPG or PNG file into the source bucket that you selected, and verifying that a new thumbnail image file (named `thumb-<original file name>`) gets created in the destination bucket.

## Authors

* Adapted from [the official S3 thumbnail generation sample from AWS documentation](https://docs.aws.amazon.com/lambda/latest/dg/with-s3-example-deployment-pkg.html), retrieved on 2018-01-19)
* Modified for Sigma by *Janaka Bandara*

## License

```
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in 
compliance with the License. You may obtain a copy of the License at 

http://www.apache.org/licenses/LICENSE-2.0 

Unless required by applicable law or agreed to in writing, software distributed under the License is 
distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. 
See the License for the specific language governing permissions and limitations under the License. 
```

## Acknowledgments

* AWS documentation team
* Awesome SLAppForge team
