{{{ "title": "Create Schedule Jobs", "date": "10-16-2015", "author": "Shan Sundaram", "attachments": [] }}}

Update a schedule for an existing job. Have your [Account Service Alias created](./Account Service Alias API - Create Account Service Alias.md). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this request when you would like to update a schedule of an existing job.

## URL

### Structure

    PUT https://api.qa.automation.ctl.io/jobs/{accountAlias}/{jobId}/schedules/{jobScheduleId}
    

### Example

    PUT https://api.qa.automation.ctl.io/jobs/XXXX/6f6546f8-316d-4cc0-b144-cac3f5668e8d/schedules/9b68b4cd-f642-4358-93b6-32f522fa1448
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| jobId | string | Job Id for which the scheduled will be updated. | Yes   |
| jobScheduleId | string | Id of the job schedule to be udpated. | Yes   |

### Content Properties

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| description | string | Description of the job schedule. | Yes |
| serviceAccountAlias | string | Account Service Alias created from API `https://api.qa.automation.ctl.io/serviceAccounts/{accountAlias}` | Yes |
| trigger | array | [Trigger entity schema](#scheduleTrigger) | Yes |

### Trigger Entity <a name="scheduleTrigger"></a>

| Name        | Type   | Description | REQ. |
| :----------- | :------ | :--- | :--- |
| type | string | Type of schedule expression, could be either "cron" or "date". | Yes | 
| expression | string | Unix cron expression if the type is "cron" and UTC date format for "date" type.  | Yes |

### Example
	JSON
	{
		"description": "Job Schedule demo.",
		"type": {
			"type": "cron",
			"expression": "* 1 * * *"
		},
		"serviceAccountAlias": "demo-account-service-account1"
	}
	
## Response

The updated schedule document will be your response. <br /> **Note: We will need to save the id field for later to delete the schedule.**

### Entity Definition

| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| id | string | Job scheduled Id. |
| jobId | string | Id of the job to be scheduled. |
| accountAlias | string | The account alias under which the job schedule was created. |
| scheduleId | string | Id of the schedule that was created. | 
| description | string | Description of the job schedule. |


### Examples

    JSON
    {
	    "id":"9b68b4cd-f642-4358-93b6-32f522fa1448",
	    "jobId":"6f6546f8-316d-4cc0-b144-cac3f5668e8d",
	    "accountAlias":"XXXX",
	    "scheduleId":"3f3b1353-7048-4f51-bbb7-a741c1fd2f14",
	    "description":"Job Schedule demo."
	}