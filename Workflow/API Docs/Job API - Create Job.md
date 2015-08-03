{{{ "title": "Create Automation Job", "date": "07-31-2015", "author": "Shan Sundaram", "attachments": [] }}}

Creates an automation job in a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the \[Login API\]\[1\] for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new job within a given account. You also have the option to run it immediately or as needed.

## URL

### Structure

    POST http://64.15.188.230/jobs/{accountAlias}?immediate=true|false
    

### Example

    POST http://64.15.188.230/jobs/ALIAS?immediate=false
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| AccountAlias | string | Short code for a particular account. | Yes  |
| immediate | boolean | To indicate if the job to be executed immediately after creation. <br /> Default is "false". | No   |

### Content Properties

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| description | string | Name of the job. | No |
| callbacks | array | Call back webhook urls where you would like to view live feed of job status. | No |
| hosts | array | TBD | TBD |
| repository | array | TBD | Yes |

### Repository Entity
| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |

    JSON
    {
        "description": "string",
        "callbacks": [
            "string"
        ],
        "hosts": [
            {
                "hostVars": {},
                "id": "string",
                "sshPrivateKey": [
                    "string"
                ]
            }
        ],
        "properties": {},
        "repository": {
            "credentials": {
                "password": "string",
                "sshPrivateKey": [
                    "string"
                ],
                 "username": "string"
            },
            "defaultPlaybook": "string",
            "ref": "string",
            "url": "string"
        },
        "sshPrivateKey": [
            "string"
        ],
    }
## Response

The response will be a list of objects containing entities for each job created in the given account.

### Entity Definition

| Name        | Type   | Description |
| ----------- | ------ | -- |
| id          | string | ID of the job. |
| description | string | Name of the job. |
| repository  | array  | Github repository specifications where the playbook is related to the job is present. |
| hosts       | array  | TBD |
| details     | array  | Information about the latest executed job. |
| callbacks   | array  | Call back webhook urls where you would like to view live feed of job status. |
| links       | array  | Collection of \[entity links\](../Getting Started/api-v20-links-framework.md) that point to resources related to this policy. |

### Examples

    JSON
    [
      {
        "id": "1111505e-6773-494a-b2bf-d2cc2684710d",
        "accountAlias": "account Alias",
        "description": "Your job description",
        "repository": {
          "url": "https://github.com/yourrepository.git",
          "ref": "master",
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
