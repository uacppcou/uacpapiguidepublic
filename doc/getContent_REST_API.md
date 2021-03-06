## getContent REST API

The getContent API returns content and metadata of a specific topic.

***

### Request

**URI:**`http://help.sap.com/http.svc/getcontent`

**HTTP Method:****GET**

**Permissions: Without authentication only public content \(status =PRODUCTION and read = EVERYONE\) can be found.**

***

#### Request Parameters

|Parameter|Required|Data Type|Description|Example|Parameter Type|
|---------|--------|---------|-----------|-------|--------------|
|**deliverable**|No|String|Deliverable LOIO \(output LOIO\)|a14ec5921d4c420298b27a8cdd4e4abb|Query string|
|**version**|Yes|String|Product versionInstead of the version, you can also enter **latest** to get the results for the latest version.|1.0|Query string|
|**language**|Yes|String|Document languageIf not specified, the default en-US is used.|en-US|Query string|
|**fallbackLanguage**|No|String|Fallback language, if the content is not found in the specified language.For example, if language=de-DE and fallbackLanguage=en-US, if no result is available in German, then the English result is returned.|en-US|Query string|
|**transtype**|Yes|String|Deliverable transtype \(output format\)If not specified, the default `html5.uacp` is used.|dhtml.sap|Query string|
|**state**|Yes|String|Publishing statusIf not specified, the default PRODUCTION is used.|DRAFT|Query string|
|**topic**|Either **topic** or **filepath** is required.|String|Topic LOIO|69c51e38264c4f169a76f7a115196d1|Query string|
|**filepath**|Either **topic** or **filepath** is required.|String|Relative path to the file as an alternative to topic loio| |Query string|
|**nocontent**|No|String|If set to true, only metadata is returned|false|Query string|

***

#### Request Example

```
https://help.sap.com/http.svc/getcontent?deliverable=39615c43587c4405aba2de8ebf33cd66&version=6.18.06&topic=4c450e681a75415ba146a563817e68c2&language=en-US&state=PRODUCTION 
```

***

### Response

***

#### Response Status and Error Codes

|Code|Reason|
|----|------|
|200|Data successfully returned|
|404|Content not found \(for example, due to invalid paramters\)|
|500|Internal server error|

***

#### Response Elements

The result is returned as JSON document as part of the response body. The table lists all elements. Depending on the content type, some elements can be empty.

|Element|Description|Example|
|-------|-----------|-------|
|date|Last publishing date|2017-05-15|
|description|Short description|The Max DB .....|
|documentType|Topic or product, here, only topics are retrieved.|Topic|
|format|Format of the document. Allowed values are: Standard \(html5, uacp\), HTML, PDF, Others \(rtf, xhtml\)|Standard|
|lastModified|Date the topic was last modified|2017-04-06|
|lastModifiedBy|User ID of the user who last modified the topic|D064123|
|mimeType|Mime type, such as PDF, or HTML|text/html|
|product|Product the topic is part of|SAP NetWeaver|
|size|Size of the content in bytes|1234|
|state|Publishing status of the content|DRAFT|
|title|Title of the topic|SAP MaxDB|
|transtype|Transtype \(output format\)|html5.uacp|
|version|Product version|7.5 SPS02|
|content|Topic content|<html\><title\>SAP MaxDB....</html\>|

***

#### Response Example

```
{
    "status": "OK",
    "data": {"content":     {
        "content": "<!DOCTYPE html  SYSTEM \"about:legacy-compat\">\<html lang=\"en-us\" dir=\"ltr\">   <head> ....<\/html>",
        "date": "2016-03-10",
        "description": "The error messages generated by the SAP DITA Framework are seen in the\n\t\tBuild Dashboard's Log Analyzer. They contain a message ID, severity level, and message text,\n\t\tfollowing DITA-OT conventions. This topic lists each error message type and provides\n\t\tadditional information to help understand and resolve the error condition.",
        "documentType": "Topic",
        "format": "standard",
        "mimeType": "text/html",
        "product": "dita_output_validation_uacp",
        "size": "0",
        "state": "DRAFT",
        "title": "SAP DITA Framework Error Messages",
        "transtype": "html5.uacp",
        "url": "/viewer/#/DRAFT/e3a1c96e2b8145298541ce21b0f5c983/1/en-US/3f1a18dc1a4143b884020af3483d7359.html",
        "version": "1"
    }}
}
```

