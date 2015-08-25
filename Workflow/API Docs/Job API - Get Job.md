{{{ "title": "Get Automation Job", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Gets a given automation job by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get the details of a specific job created within a given account.

## URL

### Structure

    GET http://api.qa.automation.ctl.io/jobs/{accountAlias}/{id}

### Example

    GET http://api.qa.automation.ctl.io/jobs/ALIAS/1111505e-6773-494a-b2bf-d2cc2684710d

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job being queried. | Yes   |

## Response

The response will be a Job object containing all its entities.

### Entity Definition

| NAME        | TYPE   | DESCRIPTION |
| :------------ | :------ | :----------------------------------- |
| id          | string | ID of the job. |
| accountAlias | string | The account alias under which the job was created. |
| description | string | Name of the job. |
| repository  | array  | [Github repository details where the playbook is related to the job is present.](#repoEntity) |
| hosts       | array  | [Hosts entity schema](#hostsEntity) |
| callbacks   | array  | Call back webhook urls where you would like to view live feed of job status. |
| links       | array  | Collection of [entity links](https://www.ctl.io/api-docs/v2/#getting-started-api-v20-links-framework) that point to resources related to this policy. |

### Repository Entity <a name="repoEntity"></a>
| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| credentials | array | Credentials of a private git repository where the playbook is present. |
| url | string | Playbook git repository url. |
| branch | string | Repository bracnh or tag where the playbook is present. |
| defaultPlaybook | string | Name of the playbook to be executed with file extension. |

### Credentials Entity

| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| username | string | User name of your private git repository. |
| password | string | Password of your private git repository. |

### Hosts Entity <a name="hostsEntity"></a>
Defined list of hosts and their related variable made available to the playbook when a play or task is executed for that host.


| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| id | string | Host name on which the play is to be executed. |
| hostVars | array | Host vars are made available to the playbook when a play or task is executed for that host. |


### Examples

    JSON
    
    [
      {
        "id": "1111505e-6773-494a-b2bf-d2cc2684710d",
        "accountAlias": "account Alias",
        "description": "Your job description",
        "repository": {
          "url": "https://github.com/yourrepository.git",
          "branch": "repository_branch",
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
