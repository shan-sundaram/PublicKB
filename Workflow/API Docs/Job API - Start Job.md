{{{ "title": "Start a Job", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Kick starts an existing job by ID against different host(s). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to explicitly start a job execution on any host(s).

## URL

### Structure

    GET http://64.15.188.230/jobs/{accountAlias}/{id}/start

### Example

    GET http://64.15.188.230/jobs/ALIAS/1111505e-6773-494a-b2bf-d2cc2684710d/start

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job to be started. | Yes   |

### Content Properties
| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| hosts | array | [Hosts entity schema](#hostsEntity) | Yes |
| sshPrivateKey | string | Common SSH private key (*base64 encoded*) that can be used to connect to all list hosts. | No |

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
      			"id": "string",
      			"sshPrivateKey": [
        			"string"
      			]
    		}
    	],
    	"sshPrivateKey": [
    		"string"
    	]
	}

## Response

The Job detail in the response will be same as when it was created but you could view the execution details by making a call to the GET Job Executions.

### Entity Definition

| Name        | Type   | Description |
| :----------- | :------ | :--- |
| id          | string | ID of the job. |
| description | string | Name of the job. |
| repository  | array  | Github repository specifications where the playbook is related to the job is present. |
| hosts       | array  | Defined list of hosts and their related variables provided part of request payload. |
| details     | array  | Information about the latest executed job. |
| callbacks   | array  | Call back webhook urls where you would like to view live feed of job status. |
| links       | array  | Collection of [entity links](https://www.ctl.io/api-docs/v2/#getting-started-api-v20-links-framework) that point to resources related to this policy. |


### Examples

    JSON
    [
      {
        "id": "1111505e-6773-494a-b2bf-d2cc2684710d",
        "accountAlias": "account Alias",
        "description": "Your job description",
        "repository": {
          "url": "https://github.com/yourrepository.git",
          "branch": "master",
          "defaultPlaybook": "example.yml",
          "credentials": {
            "username": "git username",
            "password": "git password"
          }
        },
        "hosts": [
          {
            "id": "localhost",
            "hostVars": {
              "ansible_connection": "local",
              "datacenter": "VA1"
            }
          }
        ],
        "properties": {},
        "status": "ACTIVE",
        "details": {
          "lastRun": 1435868422456,
          "lastStatus": {
            "host": {
              "changed": 16,
              "failures": 0,
              "ok": 22,
              "skipped": 0,
              "unreachable": 0
            }
          }
        },
        "callbacks": [
          "your callback webhook"
        ],
        "links": [
          {
            "ref": "self",
            "id": "52f9505e-6773-494a-b2bf-d2cc2684710d",
            "href": "/v2/workflow/WFAD/jobs/52f9505e-6773-494a-b2bf-d2cc2684710d",
            "verbs": [
              "GET",
              "POST",
              "DELETE"
            ]
          }
        ]
      }
    ]