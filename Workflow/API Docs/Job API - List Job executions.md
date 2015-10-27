{{{ "title": "Get Job Executions", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Gets details of all the executions of a particular Job by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get details of all the executions of a particular job created within your account.

## URL

### Structure

    GET https://api.qa.automation.ctl.io/jobs/{accountAlias}/{jobId}/executions?page=0&size=100

### Example

    GET https://api.qa.automation.ctl.io/jobs/XXXX/ba7e6f6a-2673-4580-a297-8d7e44483bd7/executions

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job being queried. | Yes   |
| page | integer | You can specify the page number for which you would like to get the results for. <br /> Default is "0". | No |
| size | integer | You can specify the page size between 1 to 100. <br /> Default is "100". | No |

## Response

Preview of all executions of a particular job.

### Entity Definition

| Name        | Type   | Description |
| :----------- | :------ | :--- |
| totalSize | integer | Total number of executions for a queried job. |
| page | integer | The current page number based on your query. |
| size | integer | Page size of your query. |
| results | array | [List of job executions](#executions) | 

### Job Executions Entity <a name="executions"></a>
| Name        | Type   | Description |
| :----------- | :------ | :--- |
| execution_id | string | Execution id of the queried Job. |
| timers | array | [History of execution timers.](#execTimers) |
| job_id       | string  | Id of the job being queried. |
| account_alias     | string  | Short code for a particular account. |
| status   | string  | Current status of the execution. Status transition from PENDING > RUNNING > SUCCESS/FAILURE.  |
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
  		"totalSize": 2,
  		"page": 0,
  		"size": 2,
  		"results": [
			{
		      	"start": 1444924450534,
		      	"end": 1444924452123,
		      	"job_id": "ba7e6f6a-2673-4580-a297-8d7e44483bd7",
		      	"execution_id": "43324ce3-dc2a-480e-94b9-1ea705373111",
		      	"account_alias": "XXXX",
		      	"status": "FAILURE",
				"repository_log": "{
				  'recent_commit': [
				      {
				           "commit": "b087e1a44c79d0576d7cccd249d3e71a3c54fe12",
				           "author": "Author name",  
				           "author_email": "sample@xxx.com",  
				           "date": "Wed Sep 16 16:27:20 2015 -0500",  
				           "message": "Latest commit"
				      }
				  ],
				  'tags': []
				}",
				"failed_hosts": [
									"localhost"
				],
				"is_vpn_established": false
			},
			{
				"start": 1444919575778,
				"end": null,
				"job_id": "ba7e6f6a-2673-4580-a297-8d7e44483bd7",
				"execution_id": "44fdcfa2-6a7f-46d3-9f71-22e629e2358a",
				"account_alias": "XXXX",
				"status": "RUNNING",
				"repository_log": "{
				  'recent_commit': [
				      {
				           "commit": "b087e1a44c79d0576d7cccd249d3e71a3c54fe12",
				           "author": "Author name",  
				           "author_email": "sample@xxx.com",  
				           "date": "Wed Sep 16 16:27:20 2015 -0500",  
				           "message": "Latest commit"
				      }
				  ],
				  'tags': []
				}",							                "failed_hosts": [        
				],
				"is_vpn_established": false,
				"id": "61671a90-93f2-491a-b8f2-aed515f0b5a6"
			}
		]	
	 }