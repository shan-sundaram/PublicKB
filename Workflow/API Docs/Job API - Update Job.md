{{{ "title": "Update Automation Job", "date": "08-04-2015", "author": "Shan Sundaram", "attachments": [] }}}

Updates the details of an existing automation job by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to update the details of a specific job created within a given account. Basically you can re-write the entire Job description of an exisitng Job.

## URL

### Structure

    POST https://api.qa.automation.ctl.io/jobs/{accountAlias}/{id}

### Example

    POST https://api.qa.automation.ctl.io/jobs/ALIAS/1111505e-6773-494a-b2bf-d2cc2684710d

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| id | string | Id of the job being updated. | Yes   |

### Content Properties

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| description | string | Name of the job. | No |
| callbacks | array | Call back webhook urls where you would like to view live feed of job status. | No |
| repository | array | [Repository Entity schema](#repoEntity) | Yes |
| hosts | array | [Hosts entity schema](#hostsEntity)  | Yes |
| properties | array | [Property entity schema](#propEntity) | No |
| sshPrivateKey | string | The default private key (*base64 encoded*) when connecting to hosts during playbook execution. | No |
| useDynamicInventory | boolean | Instructs the ansible runner to gather all hosts of your account alias. This makes all hosts available as inventory during the playbook execution. Your playbook can then filter the hosts using the `hosts` property. | No |

### Repository Entity <a name="repoEntity"></a>
| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :--- |
| credentials | array | [Required only when executing playbooks from a private git repository.](#credEntity) | No |
| url | string | Playbook git repository url. <br /> *Note: HTTPS url should be provided* | Yes |
| branch | string | Repository bracnh or tag where the playbook is present. <br /> *Note: Not required if the playbook is in master branch*.  | No |
| defaultPlaybook | string | Name of the playbook to be executed with file extension. | Yes |

### Credentials Entity <a name="credEntity"></a>
In order to execute the playbook from your private git repository please provide username and password or SSH Key associated with your git account.

*Note: Git credentials are NOT required for a playbook in a public repository.*

| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| username | string | User name of your private git repository. |
| password | string | Password of your private git repository. |
| sshPrivateKey | string | The private key (*base64 encoded*) associated with your private git account. |

### Hosts Entity <a name="hostsEntity"></a>
Define list of hosts and their related variable made available to the playbook when a play or task is executed for that host.


| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :--- |
| id | string | Host name on which the play is to be executed. | Yes |
| hostVars | array | Host vars are made available to the playbook when a play or task is executed for that host. | No |
| sshPrivateKey | string | Private key (*base64 encoded*) Required when any task to be performed on the specified host connected via SSH. | No |

### Properties Entity <a name="propEntity"></a>
This entity can contain an object that will be provided to the playbook as extra variables. Similar to the command line --extra-vars argument.

    JSON 
    {
        "property1":"value1", 
        "property2":"value2"
    }

### Example
    JSON
    {
        "description": "Sample Job",
        "repository": {
            "credentials": {
                "username": "git username",
                "password": "git password"
            },
            "defaultPlaybook": "example.yml",
            "branch": "feature",
            "url": "https://github.com/yourrepository.git"
        },
        "callbacks": [
            "your callback webhook"
        ],
        "hosts": [
            {
                "hostVars": { 
                		"ansible_connection": "local",
                		"datacenter": "VA1"
                	},
                "id": "localhost"
            }
        ]
    }
## Response

The response will be a list of objects containing entities for each job created in the given account.

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
        "description": "Sample Job",
        "repository": {
          "url": "https://github.com/yourrepository.git",
          "branch": "feature",
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