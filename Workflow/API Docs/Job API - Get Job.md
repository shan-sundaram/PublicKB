{{{ "title": "Get Automation Job", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Gets a given automation job by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the \[Login API\]\[1\] for information on acquiring this token.

### When to Use It

Use this API operation when you want to get the details of a specific job created within a given account.

## URL

### Structure

    GET http://64.15.188.230/jobs/{accountAlias}/{id}

### Example

    GET http://64.15.188.230/jobs/ALIAS/1111505e-6773-494a-b2bf-d2cc2684710d

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job being queried. | Yes   |

## Response

The response will be a list of objects containing entities for each job created in the given account.

### Entity Definition

| NAME        | TYPE   | DESCRIPTION |
| :------------ | :------ | :----------------------------------- |
| id          | string | ID of the job. |
| description | string | Name of the job. |
| repository  | array  | Github repository specifications where the playbook is related to the job is present. |
| hosts       | array  | TBD |
| details     | array  | TBD |
| callbacks   | array  | Call back webhook urls where you would like to view live feed of job status. |
| links       | array  | Collection of \[entity links\](../Getting Started/api-v20-links-framework.md) that point to resources related to this policy. |

### Repository Entity
TBD

### Hosts Entity
TBD

### Details Entity
TBD

### Links Entity
TBD

### Examples

    JSON
    
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
