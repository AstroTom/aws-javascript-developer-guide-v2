--------

The AWS SDK for JavaScript version 3 \(v3\) is a rewrite of v2 with some great new features, including modular architecture\. For more information, see the [AWS SDK for JavaScript v3 Developer Guide](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/welcome.html)\.

--------

# Uploading an Archive to S3 Glacier<a name="glacier-example-uploadrchive"></a>

![\[JavaScript code example that applies to Node.js execution\]](http://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/images/nodeicon.png)

**This Node\.js code example shows:**
+ How to upload an archive to Amazon S3 Glacier using the `uploadArchive` method of the S3 Glacier service object\.

The following example uploads a single `Buffer` object as an entire archive using the `uploadArchive` method of the S3 Glacier service object\.

The example assumes you've already created a vault named `YOUR_VAULT_NAME`\. The SDK automatically computes the tree hash checksum for the data uploaded, though you can override it by passing your own checksum parameter:

## Prerequisite Tasks<a name="glacier-example-uploadrchive-prerequisites"></a>

To set up and run this example, you must first complete these tasks:
+ Install Node\.js\. For more information about installing Node\.js, see the [Node\.js website](https://nodejs.org)\.
+ Create a shared configurations file with your user credentials\. For more information about providing a shared credentials file, see [Loading Credentials in Node\.js from the Shared Credentials File](loading-node-credentials-shared.md)\.

## Upload the Archive<a name="glacier-example-uploadrchive-code"></a>

```
// Load the SDK for JavaScript
var AWS = require('aws-sdk');
// Set the region
AWS.config.update({region: 'REGION'});

// Create a new service object and buffer
var glacier = new AWS.Glacier({apiVersion: '2012-06-01'});
buffer = Buffer.alloc(2.5 * 1024 * 1024); // 2.5MB buffer

var params = {vaultName: 'YOUR_VAULT_NAME', body: buffer};
// Call Glacier to upload the archive.
glacier.uploadArchive(params, function(err, data) {
  if (err) {
    console.log("Error uploading archive!", err);
  } else {
    console.log("Archive ID", data.archiveId);
  }
});
```