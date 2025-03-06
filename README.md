# image-stored-one-s3-to-another-s3
1. Create S3 Buckets:
	.Go to the AWS S3 console.
	.Click "Create bucket".
	.Name the first bucket (e.g., source-bucket-yourname), leave settings default, and click "Create".
	.Create the second bucket (e.g., destination-bucket-yourname) the same way.
-------------------------------------------------------------------------------------
3. Set Up the Lambda Function:
	.Go to the AWS Lambda console.
	.Click "Create function" → Choose "Author from scratch".
	.Function name: S3CopyFunction
	.Runtime: Python 3.x
	.Click "Create function".
---------------------------------------------------------------------------
3.Add Environment Variable:
	.In the Lambda function, go to the "Configuration" tab → "Environment variables".
	.Add a variable:
	.Key: DEST_BUCKET
	.Value: destination-bucket-yourname
--------------------------------------------------------------------------
4. Add Permissions (IAM Role):
	.Go to the "Configuration" tab → "Permissions" → Click the role name.
	.Attach the following policy:
	{
  	"Effect": "Allow",
  	"Action": ["s3:GetObject", "s3:PutObject"],
  	"Resource": [
	    "arn:aws:s3:::source-bucket-yourname/*",
	    "arn:aws:s3:::destination-bucket-yourname/*"
	  ]
	}
	.Save changes.
-------------------------------------------------------------------------
6. Add the Code:
	.In the "Code" tab of the Lambda function, paste the code I shared earlier.
	.Click "Deploy".
---------------------------------------------------------------------------
8. Set S3 Trigger:
	.Go to the "Configuration" tab → "Triggers" → Add trigger.
	.Select "S3" as the source.
	.Choose source-bucket-yourname.
	.Event type: PUT (For new object creation).
	.Click "Add".
--------------------------------------------------------------
9. Check It:
	.Go to the S3 console and upload an image to source-bucket-yourname.
	.Check the destination-bucket-yourname — the image should be copied automatically!
---------------------------------           ---------------------------------
 
 
