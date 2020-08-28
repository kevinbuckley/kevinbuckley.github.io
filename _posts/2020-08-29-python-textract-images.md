---
layout: post
title:  "using aws textract to read text from images"
date:   2020-08-27 00:00:00 -0000
tags: python aws textract
---

 I found lots of tutorials on setting up a github pages blog with jekyll but none that had every step I did.  Here's every step I did.   *Disclaimer: This applies to jekyll v4*

<br>
### Setup AWS Textract access and user

1. setup an aws account in us-east2.  you'll end up needing to put a credit card # in but don't worry, the charges are in the single digits per month from my experience.  [https://us-east-2.console.aws.amazon.com/](https://us-east-2.console.aws.amazon.com/)

2. create a user for the scritp to use. navigate to [https://console.aws.amazon.com/iam/home?region=us-east-2#/users](https://console.aws.amazon.com/iam/home?region=us-east-2#/users), follow through the wizard with the following instructions:
    - Whatever name you want
    - Set Access Type to **Programmatic access**
    - Create a permission group, add the permission **AmazonTextractFullAccess** to it. 
    - Assign your user to the newly created group
    - Tags don't matter
    - IMPORTANT: Save the **Access key ID** and **Secret access key** locally

<br>
### How to call the Textract API

Using the boto3 client, call the API passing in the png as a byte array with some simple config settings.


```python
file_name = 'that_dope_file.png'
my_config = Config(
    region_name = 'us-east-2',
    signature_version = 'v4',
    retries = {
        'max_attempts': 10,
        'mode': 'standard'
    }
)
# Read document content
with open(file_name, 'rb') as document:
    imageBytes = bytearray(document.read())

# Amazon Textract client
textract = boto3.client('textract', config=my_config)

# Call Amazon Textract
return textract.detect_document_text(Document={'Bytes': imageBytes})
```
### How to parse the results

This is pretty simple, it categorized the image as BlockTypes.  Pull out is the LINE block types, which have text in them.

```python
arr = []
for item in extract["Blocks"]:
    if item["BlockType"] == "LINE":
        arr.append(item["Text"])
return arr
```

Now we have an array with all the sweet text from the image.  Nice.

----
**resources:**
- [https://aws.amazon.com/textract/](https://aws.amazon.com/textract/)
- [https://textract.readthedocs.io/](https://textract.readthedocs.io/)
- [https://botocore.amazonaws.com/v1/documentation/api/latest/reference/config.html](https://botocore.amazonaws.com/v1/documentation/api/latest/reference/config.html)
