{{{ "title": "Create Automation Job", "date": "07-31-2015", "author": "Shan Sundaram", "attachments": [] }}}

Creates an automation job in a given account. The automation jobs have to be scripted plays using Ansible. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new job within a given account. You also have the option to run it immediately or as needed.

## URL

### Structure

    PUT https://api.qa.automation.ctl.io/jobs/{accountAlias}?immediate=true|false
    

### Example

    PUT https://api.qa.automation.ctl.io/jobs/ALIAS?immediate=false
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| immediate | boolean | To indicate if the job to be executed immediately after creation. <br /> Default is "false". | No   |

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
| sshPrivateKey | string | Private Key (*base64 encoded*) required when any task to be performed on the specified host connected via SSH. | No |

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
                		"ansible_connection": "ssh",
                		"datacenter": "VA1"
                	},
                "sshPrivateKey" : "TUlJRW93SUJBQUtDQVFFQXM1VlpyV0txbitjU0dVbjYzMUZSN2M1NWV1dGZ4bHErY2pheHNGRUlrWWhoMXluaw0KdFM5T1pRLzF6YVp0MFZUY0thT1lUc0RmdnZES3Awc1pMUXFZWnFCMkkyallER2lwUGZOZk9Mb1Q4NDFqVHBmdg0KcTk3aUs1QUxMRHh6elRZSW0wVHB5YnNaTS9pVTZuc0gxTlh1SE9CNXAwY1pYRytpOXh3UUxMSkx2TnRJRGJpKw0KeE5sVWVOZkNvcFVMVzVuWWFwQUJDQWs3UjM0RkxJT3k2SHEvQVNNQ2Fhb1lSNUFNRWFiQkdBdU1kbnpZMzZoNQ0Kc3k0WVQxbk5jZmdiSjl6Z3RSbzd2dE9QYzkxTTQ0UStHSTJlSnNHVHRYSmdINVRpY0ZEeTUxSG1MMUk5dytaeA0KamZ1Sll0cFFxRHBkMmliNW1LL2JhNGxKV1RVc2RGSU9OcnlvSVFJREFRQUJBb0lCQUZpU0thZWxTU2dTYkUvQw0KdUJQYVpNRVlHN3d2U0k1cEJSTUp2THVNUytDVFZrWXJxRnhnVjVicXR6M1Zmc1pHeDB0V0gzR0FHUnB3WWxMKw0KYkExVjgzSnlZN0gxTE5GNThUYlh5TGdPdG5aaDNuL04yZXgzd2k3Z0hWS1ZBanhORVJPYmVuNy9ZMS9KazVETw0KV3o5eXY3eklUZGZkN2prejZqbGNRdkg0Z2ZoRGppR2g3Y1d6aldpY3BEQWM1SVA2MURxRFBKMlI3ZFJyS0xKRA0KSHRKb3EvY2Vxak1CNUNqcjcwQVdFelk5OUJCbDBSdWRRUERveHU2MkRMWDVMelg0d2FxWXhTQ04wMFRkakdoUQ0KbEN6ZzFoSW9CKzlEWTZIM21GM3hpbkhFUGxyeVV3VHJRWmRTTmJJMTNzRkQvNUlOaUM0U3hCNzJBLy9zVmpidQ0KQlVYOVJ3RUNnWUVBNjh4MjdORU5yaHFab0taN2hKSEdBUC83ZHp6aXl0RldtbW9JQVp4RkdCTXNCYmRvSWlwZA0KS3I3SXdIZWliQXl6VnN0WGlCd0ZTSVNDcWVwUWNOWjB6VDVzUVg1NGpVS0RkUnBrSEJ5OEN6WFpMS1g2ekFwZw0KQWlsL1RkU0ozUmpiU0dqdjZtNzZRVWx3cmhCam05clB1VUxHZk00MnF3K0NPSHNoV004ZHlyRUNnWUVBd3ZmNA0KNjdRUGE4SW5ZVWluZ3lkeW9RalZ5bVFkSTFOS081R1VDY1M1cFEvanF1U0VneVhpNU9kRlNSbThsL3JEeFI2Rg0KcytaY3Vwb3lEc1Z3ck1XZ0wwQ1ZDQlBHSE9iVEhOZDZEWjRadStsYjlKcjM2bmJOdVAwbnU1WndZQmFMNGl2SA0KOGlmMjA3ZjN1cWs5d0dPbHhOZGRpQkg5OUFYaWhSRVZUYmtsTUhFQ2dZRUFqV1k3R3AveVdDbFRYdWIyd3ZTMw0KaS9uMVRmZVErSmE0SERqaFBEWDlxUVkySytkajVya0l6WTFDelVmd2VtTFRXSVR2cEl0SkQ4ZUdvMllEZnViYg0KZkFpbTJrK0E4eFNqeUNGZlR3eGNKMHpQUXRyMW5rM0tiUUY5ZWFxdVVZdUtVODI1c1JlRHNvcmJxMFhndGFGdA0KVjJjWHA5ZnhLSHRRVjVaZTFPYStzc0VDZ1lBeC8vUDNSb01aNkgyKzVpb0hhWXR0SHQzcy9JVzRkSGk2RkJoNQ0KOU5pREt6TUF0WUFDUGlvVTkvWjl5N3JnNHU5bjB1OEk5cy9iRHdZOVlZY0cxOXUvb25sVnkvUm5udzZPKy9lUw0KSEhTUEMwYUkwV0U0NE9UYlJ4ajBjNTA0RnpBaWZZWFdaVWRZZm5wcWhWS1B6ejVJMzg1ZHdmZDFxRGl5VlhJNA0KTDM0SkVRS0JnQUV5dE4xMlBnUG9tV2IyMko0TUFWNER1cTMzUmtDaEx0TmtsUjhEbi9ISTNza3Z6MHBObWx2RQ0KV3lSblpNN29lZS9YRFg5dmFRdXlFaDhxblZHSW02WFRWcFBvVld2MFBRSk1zQkowcEpROVViRExNdVU3d0xYdA0KOHFjVGo5QjMyeTgrN0FWSEJsdi9YT0lrSy9xY0tZQUF1a3pFT1hvV1hUVGRvWE81ZnQ1dg==",
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
| createdTime | integer | Timestamp when the Job was created. |
| lastUpdatedTime | integer | Timestamp when the Job was last updated. |
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
              "ansible_connection": "ssh",
              "datacenter": "VA1",
              "public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAAQQDxt+1boRV5ZuyTPJsmz2mBe0AG+9zaSRrRHVIgwjl5uHso9GZAn8G7+hAKJuHSzfxTQXGwTdLmozrhizlpix3f test@test\n",
          "state": "present"
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
        "createdTime": 1440785845177,
        "lastUpdatedTime": 1440785845177,
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