# Superflows Document Analyzer

This tutorial is designed for developers who want to integrate the Superflows Document Analyzer into their web applications. The library integrates with HTML. With just three straightforward steps—installation, embedding, and result-extraction, developers can seamlessly incorporate document analysis into their applications. Furthermore, the analyzer supports asynchronous workflows, enabling developers to effortlessly dispatch analysis results to webhook URLs. This streamlined approach not only saves time but also empowers developers to enhance their applications efficiently and effectively.

## How It Works

Step 1 - Install the library in the page header.

Step 2 - Use it in the HTML code.

Step 3 - Receive the analysis and validation results.

## Step 1 - Installation

### Include Javascript

Add the following script tag to import the necessary JavaScript files:

```html

<script type="module">
import {LitElement, html, css} from 'https://esm.run/lit-element/lit-element.js';
import {SfIUploader} from 'https://esm.run/sf-i-uploader@1.0.42/sf-i-uploader.js';
</script>

```

### Include CSS

Add the required CSS files to style the analyzer:


#### Uploader CSS

```html

<link href="sfiuploader.css" rel="stylesheet" />

```
The vanilla stylesheet is available <a target="_blank" href="https://stackblitz.com/edit/stackblitz-starters-wt34hh?file=index.html,sfiuploader.css">here</a>.

#### Supporting CSS

```html

<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0" rel="stylesheet"/>

```

## Step 2 - Usage

Once the library is installed, you can easily integrate the document analyzer into your HTML forms. Show the analyzer to begin analyzing documents. For instance, place the following code within your HTML form to enable document analysis.

```html

<sf-i-uploader></sf-i-uploader>

```

Users can then select a document for analysis.

## Step 3 - Extract the results

After the analysis completes, the results can be extracted using two methods.

### Method 1 - Javascript call

Use the `selectedValues()` function to extract the results. For e.g., invoke this function from the from validation function in your form submission workflow.

```javascript

document.querySelector('sf-i-uploader').selectedValues();

```

### Method 2 - Via A Webhook

Use this method to implement an asynchronous workflow. Provide the `callbackUrlHost` and the `callbackUrlPath` arguments. If these arguments are provided the analyzer constructs the webhook url as `https://callbackUrlhost/callbackUrlPath` and dispatches the analysis results to it after completion.

```html

<sf-i-uploader 
    callbackUrlHost="<host>" 
    callbackUrlPath="<path>">
</sf-i-uploader>

```

To ensure proper integration, replace `callbackUrlHost` and `callbackUrlPath` with the actual hostname and path of your webhook endpoint. In the example provided, the constructed webhook URL will be `https://abc.net/processresult`.

```html

<sf-i-uploader 
    callbackUrlHost="abc.net" 
    callbackUrlPath="/processresult">
</sf-i-uploader>

```


## Demo

Check out the live demo on StackBlitz for a quick demonstration.

[<img src="https://developer.stackblitz.com/img/open_in_stackblitz.svg">](https://stackblitz.com/edit/stackblitz-starters-wt34hh?file=index.html)

## Use Cases


### Restrict file types

Specify the allowed file types by setting the `allowedExtensions` variable. In the example provided below, only *png* and *jpg* file types will be accepted.

```html

<sf-i-uploader 
    allowedExtensions="[&quot;jpg&quot;,&quot;png&quot;]">
</sf-i-uploader>

```

### Validate various document types

Specify the document type for validation by setting the `docType` variable. The example below validates the uploaded document against the *aadhar* document type. 

```html

<sf-i-uploader 
    docType="aadhar">
</sf-i-uploader>

```

### Implement asynchronous flow using a webhook

Specify your webhook URL by setting the `callbackUrlHost` and the `callbackUrlPath` parameters. If these arguments are provided the analyzer constructs the webhook url as `https://callbackUrlhost/callbackUrlPath` and dispatches the analysis results to it after completion. In the example provided, the constructed webhook URL will be `https://abc.net/processresult`.

```html

<sf-i-uploader 
    docType="aadhar"
    callbackUrlHost="abc.net" 
    callbackUrlPath="/processresult">
</sf-i-uploader>

```

## Reference

### Arguments

| Argument | Mandatory | Datatype | Description | Allowed Values & Examples | Default Value |
|----------|---------- |----------|-------------|---------------------------|---------------|
| apiId | yes | alphanumeric string | Api key | 1peg5170d3 is the value for the free plan. For a pro plan, you will receive a personalized key | "1peg5170d3" |
| allowedExtensions | no | encoded json array string | JPG, PNG and PDF files are supported. This array allows you to enable / disable / choose one or more of these. | [&quot;jpg&quot;,&quot;png&quot;,&quot;pdf&quot;] will allow all three extensions. [&quot;jpg&quot;] will only allow the PDF extension. | "[&quot;jpg&quot;,&quot;png&quot;,&quot;pdf&quot;]" |
| docType | no | string | Code for the document type validation | "aadhar" for Aadhar card, "pan" for PAN card. The entire document type code reference is available here. | "aadhar" |
| callbackUrlHost | no | url string | If provided, the uploader calls the https://callbackUrlHost/callbackUrlPath a payload containing the upload and processing result. | "example.com" for callbackUrlHost and "processresult" for callbackUrlPath results in a webhook call to https://example.com/processresult. |
| callbackUrlPath | no | url path string | If provided, the uploader calls the https://callbackUrlHost/callbackUrlPath with a payload containing the upload and processing result. | "example.com" for callbackUrlHost and "processresult" for callbackUrlPath results in a webhook call to https://example.com/processresult. |
| dataPassthrough | no | encoded json object string | The payload specific to your use-case, which you wish to receive at the webhook. The uploader calls https://callbackUrlHost/callbackUrlPath webhook with a payload containing the upload and processing result. If provided, the dataPassthrough object is attached with the payload as well. | Upto you. Maximum permissible size is 500 KB. | "{}" |


### Functions

| Functions | Returntype | Description |
|----------|---------- |----------|
| selectedValues() | json array object | Returns the results of the document analysis. |


### Document Types

| Type | Code | Description |
|----------|---------- |----------|
| Aadhar | "aadhar" | Aadhaar by UIDAI is a 12-digit unique identification number issued to residents of India based on their biometric and demographic data. |
| PAN | "pan" | PAN (Permanent Account Number) is a unique alphanumeric identifier issued by the Income Tax Department of India to individuals and entities for tracking financial transactions and filing taxes. |
| Voter ID | "voterid" | Voter ID, issued by the Election Commission of India (ECI), is a unique identification card that enables eligible Indian citizens to participate in the electoral process by casting their votes in elections. |
| Passport (India) | "passportin" | The Indian passport is an official document issued by the Government of India, serving as proof of nationality and identity for international travel. |



