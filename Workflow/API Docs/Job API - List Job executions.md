{{{ "title": "Get Job Executions", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Gets details of all the executions of a particular Job by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the \[Login API\]\[1\] for information on acquiring this token.

### When to Use It

Use this API operation when you want to get the details of all the executions of a particular job created within a given account.

## URL

### Structure

    GET http://64.15.188.230/jobs/{accountAlias}/{id}/executions

### Example

    GET http://64.15.188.230/jobs/ALIAS/d268c7e5-3dd9-4c7c-a043-63d0599e7cb3/executions

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job to be deleted from the account. | Yes   |

## Response

The response will be updated details of the Job.

### Entity Definition

| Name        | Type   | Description |
| ----------- | ------ | -- |
| id          | string | Execution id. |
| start | TBD | TBD |
| end  | TBD  | TBD |
| job_id       | string  | TBD |
| account_alias     | string  | TBD |
| exit_status   | string  | TBD |
| exit-status       | string  | TBD|

### Examples

    JSON
    [
        {
            "id": "568c28c4-8ecf-4087-bed1-e1761c86bb02",
            "start": "1438346432514",
            "end": "1438346432521",
            "job_id": "d268c7e5-3dd9-4c7c-a043-63d0599e7cb3",
            "account_alias": "WFAD",
            "exit_status": null,
            "exit-status": "FAILURE"
        }
    ]
