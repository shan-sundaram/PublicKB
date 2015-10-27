{{{ "title": "Get status of all Job Executions", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Get status information of all the excutions of a Job by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to view the detailed Status information of all the executions of a specific job created within a given account.

## URL

### Structure

    GET https://api.qa.automation.ctl.io/status/{accountAlias}/job/{jobId}

### Example

    GET https://api.qa.automation.ctl.io/status/XXXX/job/1111505e-6773-494a-b2bf-d2cc2684710d

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| jobId | string | Id of the job being queried. | Yes   |

## Response

The response will be detailed status of all executions of the queried Job.

