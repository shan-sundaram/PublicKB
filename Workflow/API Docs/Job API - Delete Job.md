{{{ "title": "Delete Automation Job", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Remove an existing automation job in a given account. The automation jobs have to be scripted plays using Ansible. Calls to this operation must include a token acquired from the authentication endpoint. See the \[Login API\]\[1\] for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete an existing job within a given account.

## URL

### Structure

    DELETE http://64.15.188.230/jobs/{accountAlias}/{id}
    

### Example

    DELETE http://64.15.188.230/jobs/ALIAS/e436f511-21f9-4cda-9026-a68cd6112240
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job to be deleted from the account. | Yes   |


## Response

TBD
