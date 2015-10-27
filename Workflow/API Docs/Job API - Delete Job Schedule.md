{{{ "title": "Create Schedule Jobs", "date": "10-16-2015", "author": "Shan Sundaram", "attachments": [] }}}

Delete a schedule of an existing job. Have your [Account Service Alias created](./Account Service Alias API - Create Account Service Alias.md). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this request when you would like to delete a schedule of an existing job.

## URL

### Structure

    DELETE https://api.qa.automation.ctl.io/jobs/{accountAlias}/{jobId}/schedules/{jobScheduleId}
    

### Example

    DELETE https://api.qa.automation.ctl.io/jobs/XXXX/6f6546f8-316d-4cc0-b144-cac3f5668e8d/schedules/9b68b4cd-f642-4358-93b6-32f522fa1448
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| jobId | string | Job Id for which the scheduled will be removed. | Yes   |
| jobScheduleId | string | Id of the job schedule to be removed. | Yes   |