{{{ "title": "Get Job Executions", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Gets details of all the executions of a particular Job by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get details of all the executions of a particular job created within a given account.

## URL

### Structure

    GET http://64.15.188.230/jobs/{accountAlias}/{id}/executions

### Example

    GET http://64.15.188.230/jobs/ALIAS/ba7e6f6a-2673-4580-a297-8d7e44483bd7/executions

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job being queried. | Yes   |

## Response

Preview of all executions of a particular job.

### Entity Definition

| Name        | Type   | Description |
| :----------- | :------ | :--- |
| id          | string | Execution id of the queried Job. |
| start | number | EPOCH format of job execution start Date time in GMT.  |
| end  | number  | EPOCH format of job execution end Date time in GMT. |
| job_id       | string  | Id of the job being queried. |
| account_alias     | string  | Short code for a particular account. |
| exit_status   | string  | Outcome of the ansible playbook execution with either "SUCCESS" or "FAILURE".  |
| result       | array  | This is the final status returned by the ansible runner. |


### Examples

    JSON
    [
	  {
	    "id": "29a3c264-b8f1-4608-ab7d-34a1aae6f6b1",
	    "start": 1439998433881,
	    "end": 1439998433889,
	    "job_id": "d2b66469-5767-4426-9da0-efcebf82c7aa",
	    "account_alias": "WFAQ",
	    "exit_status": "SUCCESS",
	    "result": {
	      "localhost": {
	        "unreachable": 0,
	        "skipped": 0,
	        "ok": 3,
	        "changed": 1,
	        "failures": 0
	      }
	    }
	  },
	  {
	    "id": "ba7e6f6a-2673-4580-a297-8d7e44483bd7",
	    "start": 1439999024933,
	    "end": 1439999024941,
	    "job_id": "d2b66469-5767-4426-9da0-efcebf82c7aa",
	    "account_alias": "WFAQ",
	    "exit_status": "SUCCESS",
	    "result": {
	      "localhost": {
	        "unreachable": 0,
	        "skipped": 0,
	        "ok": 3,
	        "changed": 0,
	        "failures": 0
	      }
	    }
	  }
	]