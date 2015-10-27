{{{ "title": "Create Schedule Jobs", "date": "10-16-2015", "author": "Shan Sundaram", "attachments": [] }}}

Get schedule(s) of an existing job. Have your [Account Service Alias created](./Account Service Alias API - Create Account Service Alias.md). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this request when you would like to get the schedule(s) of an existing job.

## URL

### Structure

    GET https://api.qa.automation.ctl.io/jobs/{accountAlias}/{jobId}/schedules
    

### Example

    GET https://api.qa.automation.ctl.io/jobs/XXX/6f6546f8-316d-4cc0-b144-cac3f5668e8d/schedules
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| jobId | string | Job Id for which the schedule(s) are requested. | Yes   |
| page | integer | You can specify the page number for which you would like to get the results for. <br /> Default is "0". | No |
| size | integer | You can specify the page size between 1 to 100. <br /> Default is "100". | No |

## Response

The updated schedule document will be your response. <br /> **Note: We will need to save the id field for later to delete the schedule.**

### Entity Definition

| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| totalSize | integer | Total number of job schedules created for the job under your account alias. |
| page | integer | The current page number based on your query. |
| size | integer | Page size of your query. |
| results | array | [List of Job Schedules](#jobSchedules) | 

### Job Schedule Entity <a name="jobSchedules"></a>
| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| id | string | Job scheduled Id. |
| jobId | string | Id of the job for which the schedule(s) are requested. |
| accountAlias | string | The account alias under which the job schedule was created. |
| scheduleId | string | Id of the job schedule. |
| description | string | Description of the job schedule. |


### Examples

    JSON
    {
	  "totalSize": 1,
	  "page": 0,
	  "size": 1,
	  "results": [
	    {
	      "id": "e68e6bc3-75be-4f8c-8ee9-de13d6218278",
	      "jobId": "6f6546f8-316d-4cc0-b144-cac3f5668e8d",
	      "accountAlias": "XXX",
	      "scheduleId": "26f9bd9e-8115-4e57-b1da-4d50c066dd09",
	      "description": "Job Schedule demo."
	    }
	  ]
	}