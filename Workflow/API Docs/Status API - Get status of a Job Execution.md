{{{ "title": "Get status of a Job Execution", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Get detailed status information of a Job execution by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to view the detailed Status information of an execution of a specific job created within a given account.

## URL

### Structure

    GET https://api.qa.automation.ctl.io/status/{accountAlias}/job/{jobId}/execution/{executionId}

### Example

    GET https://api.qa.automation.ctl.io/status/XXXX/job/1111505e-6773-494a-b2bf-d2cc2684710d/execution/28ae401b-9620-4a5f-b16d-82a06841b6c4

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| jobId | string | Id of the job being queried. | Yes   |
| executionId | string | Id of the job execution being queried. | Yes   |

## Response

The response will be detailed status of an execution of the queried Job.

