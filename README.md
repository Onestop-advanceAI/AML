<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [-](#-)
- [How to get account and key](#how-to-get-account-and-key)
- [Setup AML screening and monitoring](#setup-aml-screening-and-monitoring)
    - [Open API Approach](#open-api-approach)
    - [Batch Task Approach](#batch-task-approach)
    - [Check Monitoring Result](#check-monitoring-result)

<!-- markdown-toc end -->


# AML
This is a reference manual and configuration guide for Anti-Money Laundering(AML) integration. It describes how to request an account, AML screening&monitoring, and check results in the OSP.

## How to get account and key
If you are interested in OSP/AML, please contact our operation team to open an account with OSP permission. 

Once your account is setup, verify your account via login [Sandbox OSP portal](https://sandbox-oop.advai.net/). Meanwhile, you also need to request your *ADVAI_KEY* for the purpose of authentication. Protect this key.

## Setup AML screening and monitoring
Two approaches to use AML functions:
### Open API Approach

This is the simplest way to do AML screening and monitoring. Just copy the following command to your shell, replace *YOUR_ADVAI_KEY* with your *ADVAI_KEY*, and then execute it. After execution completes, you will get a `transactionId`, via which you can get a detail screening transaction result in the OSP. 

This shell command only instructs OSP to screen a user: `referenceId` is `kun0991412224124` and `name` is `David`, and adds the user to our profile set. Please refer [AML Screening Monitoring](https://github.com/Onestop-advanceAI/APIRepostiroy/blob/master/open_apis/aml_monitoring_screening.md) to check other parameters. 

```shell

curl --location --request POST 'https://api.advai.net/intl/openapi/monitoring/amlScreeningAndMonitoring' \
--header 'Content-type: application/json' \
--header 'X-ADVAI-KEY: ${YOUR_ADVAI_KEY}' \
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

    
### Workflow Approach
This approach only supports `screening` mode, and the `monitoring` mode will be available soon. 
1. *Step 1: create a AML screening workflow* 

Login OSP portal and goto menu `WORKFLOWS` > `ALLWorkflows`, and click `AML Compliance` template. In the workflow creation page, you can rename the workflow, and then publish it. 
![Workflow Creation ](images/create_workflow.png "Create a workflow")

2. *Step 2: create a batch task* 

Goto menu `VERIFICATION` > `Batch Tasks`, and create a new task. In the pop window, selected the created workflow by name, and download the corresponding excel template. For the template, fill up batch data you want to screen in the *source* sheet after reading *READ THIS FIRST*.
![Create a batch task ](images/create_tasks.png "Create a batch task")

3. *Step 3*

In the create new task page, click `schedule new cases` after uploading data file, setting task name and scheduled time. 

4, *Step 4*: Download the task result file when the task finishes. In the result file, you can get `caseId` for each data record. 

The alternative for *step 2* is to call execute the workflow created in **step 1** using OSP Open API [Workflow Submission](https://github.com/Onestop-advanceAI/APIRepostiroy/blob/master/open_apis/workflow_submit.md)


## Check Monitoring Result
Three approaches to check AML screening and monitoring result when you have a `transactionId`. 

1. *Approach 1* 

Goto `VERIFICATIONS > All Verifications` and retrieve the `transactionId` in the search box. In this way, you can get transaction detail info, e.g., status, input parameters, and decision result. If there is `case` with this transaction, you can goto menu `CASES > All Cases` to review and finalize the case status in a similar way. 

2. *Approach 2* 

Retrieve transaction detail information via our Open API [getTransactionDetail](https://github.com/Onestop-advanceAI/APIRepostiroy/blob/master/open_apis/workflow_query_result.md) with `transactionId` and *ADVAI_KEY*.

3. *Approach 3* 

Setup a transaction callback method, and OSP will notify you when transaction ends. This feature is not public currently, and you need to contact our engineers to set it up.

