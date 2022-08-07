<!-- # AML
 One-stop Platform(OSP) enables banks and financial institution to provides Anti-money Laundering(AML) with AML toolkit.

OSP AML toolkit is important to customer's business, especially for their on-boarding processes. First, financial institutions have to protect themselves from risks and meet AML obligations. Thus, these institutions have to perform an extended AML screening to determine their customer risks and response them according to their business rules. Second, customer risks are not static and change over time, and they should be periodically checked and assessed with new actions. 

OPS AML toolkit provides two APIs and one openAPI to screen and monitor a user's risk. 

## AML Screening (api lib -> workflow)

## AML Monitoring (api lib -> workflow)

## AML MonitoringAndScreening (engine: call directedly)

## How to do integration

## API definitions
--> 
<!-- Start Document Outline -->
* [AML](#AML)
* [Installation](#installation)
* [Links](#links)
* [Show your Support](#show-your-support)
* [Features](#features)
	* [Markdown Editor](#markdown-editor)
		* [Image Features](#image-features)
		* [Editing Features](#editing-features)
		* [Output and Selections](#output-and-selections)
		* [Theme Support](#theme-support)
		* [File Operations](#file-operations)
		* [Weblog Publisher](#weblog-publisher)
		* [Non Markdown Features](#non-markdown-features)
	* [Command Line features](#command-line-features)
	* [Why another Markdown Editor?](#why-another-markdown-editor)
* [Acknowledgements](#acknowledgements)
* [Spread the Word about Markdown Monster](#spread-the-word-about-markdown-monster)
* [License](#license)
	* [Contribute - get a Free License](#contribute---get-a-free-license)
	* [Warranty Disclaimer: No Warranty!](#warranty-disclaimer-no-warranty)
<!-- End Document Outline -->

# AML
This is a reference manual and configuration guide for Anti-Money Laundering(AML) integration. It describes how to request an account, screening&monitoring a user, and check monitoring result in the OSP

## Request an OSP account and login OSP
If you are interested in OSP/AML, please contact our operation team to open an account with OSP permission. 

Once your account is setup, you should be able to login [Sandbox OSP portal](https://sandbox-oop.advai.net/). You can also request your *ADVAI_KEY* for the purpose of authentication and no leak for it.

## Setup AML screening and monitoring
### Via OSP Open API

This is the simplest way to do AML screening and monitoring. Just copy following command to your shell, replace `${YOUR_ADVAI_KEY}` with your *ADVAI_KEY*, and then execute it. After execution completes, you will get a `transactionId`, via which you can get a detail screening transaction result in the OSP. 

This shell command only instructs OSP to screen a user: `referenceId` is `kun0991412224124` and `name` is `David`, and adds the user to our profile set. Please refer [AML Screening Monitoring](https://github.com/Onestop-advanceAI/APIRepostiroy/blob/master/open_apis/aml_monitoring_screening.md) to check other parameters. 

```shell

curl --location --request POST 'https://sandbox-oop.advai.net/intl/openapi/monitoring/AMLScreeningAndMonitoring' \
--header 'Content-type: application/json' \
--header 'X-ADVAI-KEY: ${YOUR_ADVAI_KEY}' \
'
--data-raw '{                                 
  "name": "David",                    
  "type": [                           
    "Person"                          
  ], 
  "referenceId": "kun0991412224124", 
  "idNumber": "", 
  "dob": "", 
  "regionList": [ 
    "Indonesia" 
  ], 
  "gender": "Female", 
  "mode": 1, 
  "score": 0.95, 
  "contentList": ["OOL"], 
  "intervalTime": 1 
}
'
```


### Via OSP Batch



## Check Monitoring Result
