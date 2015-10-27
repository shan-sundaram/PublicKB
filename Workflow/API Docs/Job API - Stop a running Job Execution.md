{{{ "title": "Stop a Running Job Execution", "date": "10-20-2015", "author": "Shan Sundaram", "attachments": [] }}}

To stop a `Running` job execution gracefully. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.
Once the execution is created, it will be queued to start at the earliest.  Live status feed of the execution can be viewed with your callback(s) url if you have defined at the time of job creation.

### When to Use It

Use this API operation when you would like to stop a `Running` execution of a job. 

## URL

### Structure

    POST https://api.qa.automation.ctl.io/jobs/{accountAlias}/{jobId}/executions/{executionId}/stop

### Example

    POST https://api.qa.automation.ctl.io/jobs/XXXX/1111505e-6773-494a-b2bf-d2cc2684710d/executions/44fdcfa2-6a7f-46d3-9f71-22e629e2358a/stop

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job to be started. | Yes   |
| executionId | string | Execution id of the job to be re-started. | Yes |

### Content Properties

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| expiryDuration | number | Stop signal expiry duration in seconds. <br /> Default value is zero seconds. | No |


### Example

    JSON
    {
	 	"expiryDuration": 5
	 }

## Response

An execution document with your previous run timer details with an updated status as "STOPPING" will be your repsonse. Eventually the status will change to STOPPED. You could view the execution details by making a call to the GET Job Executions `GET https://api.qa.automation.ctl.io/jobs/ALIAS/1111505e-6773-494a-b2bf-d2cc2684710d/executions`.

**Note:** *Tasks that are executed until the stop request will not rollback.*

### Entity Definition

| Name        | Type   | Description |
| :----------- | :------ | :--- |
| execution_id | string | Execution id of the queried Job. |
| timers | array | [History of execution timers.](#execTimers) |
| job_id       | string  | Id of the job being queried. |
| account_alias     | string  | Short code for a particular account. |
| status   | string  | Will be PENDING at the time of start.   |
| repository_log | string | Git commit version of the playbook, if the defined peoplelaybook is from git repository. |
| failed_hosts | array | List of failed hosts. |
| is_vpn_established | boolean | Set to `true` if the execution has any VPN connections enabled part of the play. |

### Execution timers Entity <a name="execTimers"></a>
An execution will have multiple timers only when it is restarted.
| Name        | Type   | Description |
| :----------- | :------ | :--- |
| start | number | EPOCH format of job execution start Date time in UTC.  |
| end  | number  | EPOCH format of job execution end Date time in UTC. |

### Examples

    JSON
    {
		"timers": [
		    {
		      "start": 1445359386400,
		      "end": 1445359388219
		    }
  		],
		job_id: "1111505e-6773-494a-b2bf-d2cc2684710d"
		execution_id: "44fdcfa2-6a7f-46d3-9f71-22e629e2358a"
		account_alias: "XXXX"
		status: "PENDING"
		repository_log: null
		failed_hosts: [0]
		is_vpn_established: false
	}