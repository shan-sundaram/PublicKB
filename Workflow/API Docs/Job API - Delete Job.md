{{{ "title": "Delete a Runner Job", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Delete an existing Runner job in a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete an existing job within a given account.

## URL

### Structure

    DELETE https://api.qa.automation.ctl.io/jobs/{accountAlias}/{id}
    

### Example

    DELETE https://api.qa.automation.ctl.io/jobs/XXXX/e436f511-21f9-4cda-9026-a68cd6112240
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job to be deleted from the account. | Yes   |


## Response


| HTTP CODE         | DESCRIPTION   |
| :------------ | :------ |
| 204 | Sent when a request to delete a Job is successful. |