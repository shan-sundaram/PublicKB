{{{ "title": "Start a Job", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Creates an execution of an existing job by ID against different host(s). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.
Once the execution is created, it will be queued to start at the earliest.  Live status feed of the execution can be viewed with your callback(s) url if you have defined at the time of job creation.

### When to Use It

Use this API operation when you want to explicitly start a job execution on any host(s).

## URL

### Structure

    POST https://api.qa.automation.ctl.io/jobs/{accountAlias}/{id}/start

### Example

    POST https://api.qa.automation.ctl.io/jobs/XXXX/1111505e-6773-494a-b2bf-d2cc2684710d/start

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job to be started. | Yes   |

### Content Properties
Based on your job definition you have to start an execution by passing in required host(s) information. If you would like to start the execution without any host, then you have to `POST` an empty object.

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| hosts | array | [Hosts entity schema](#hostsEntity) | No |
| sshPrivateKey | string | SSH private key (*base64 encoded*) that can be used to connect listed hosts. | No |

### Hosts Entity <a name="hostsEntity"></a>
Define list of hosts and their related variable made available to the playbook when a play or task is executed for that host.


| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :--- |
| id | string | Host name on which the play is to be executed. | Yes |
| sshPrivateKey | string | Private Key (*base64 encoded*) required when any task to be performed on the specified host connected via SSH. | No |

### Example

    JSON
    {
	 	"hosts": [
    		{
      			"id": "localhost"
      		}
    	]
	}

## Response

An execution document will be your repsonse but you could view the execution details by making a call to the GET Job Executions `GET https://api.qa.automation.ctl.io/jobs/XXXX/1111505e-6773-494a-b2bf-d2cc2684710d/executions`.

### Entity Definition

| Name        | Type   | Description |
| :----------- | :------ | :--- |
| execution_id | string | Execution id of the queried Job. |
| start | number | EPOCH format of job execution start Date time in UTC.  |
| end  | number  | EPOCH format of job execution end Date time in UTC. |
| job_id       | string  | Id of the job being queried. |
| account_alias     | string  | Short code for a particular account. |
| status   | string  | Will be PENDING at the time of start.   |


### Examples

    JSON
    {
		start: null
		end: null
		job_id: "1111505e-6773-494a-b2bf-d2cc2684710d"
		execution_id: "44fdcfa2-6a7f-46d3-9f71-22e629e2358a"
		account_alias: "XXXX"
		status: "PENDING"
		repository_log: null
		failed_hosts: [0]
		is_vpn_established: false
	}