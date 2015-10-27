{{{ "title": "Get all Runner Jobs", "date": "07-30-2015", "author": "Shan Sundaram", "attachments": [] }}}

Gets a list of jobs published within a given account alias. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of jobs published within a given account and view the details of a job.

## URL

### Structure

    GET https://api.qa.automation.ctl.io/jobs/{accountAlias}?page=0&size=100
    

### Example

    GET https://api.qa.automation.ctl.io/jobs/XXXX
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| page | integer | You can specify the page number for which you would like to get the results for. <br /> Default is "0". | No |
| size | integer | You can specify the page size between 1 to 100. <br /> Default is "100". | No |

## Response

The response will be a list of objects containing entities for each job created in the given account in the order of last created. Along with total number of jobs created under your account alias. <br/>*Note: The maximum number of records per request is 100, use the combination of page and size to recursivrly retrieve subsequent records.*

### Entity Definition

| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| totalSize | integer | Total number of jobs created under your account alias. |
| page | integer | The current page number based on your query. |
| size | integer | Page size of your query. |
| results | array | [List of jobs](#jobs) | 

### Jobs Entity <a name="jobs"></a>
| NAME        | TYPE   | DESCRIPTION |
| :------------ | :------ | :----------------------------------- |
| id          | string | ID of the job. |
| accountAlias | string | The account alias under which the job was created. |
| description | string | Description of the job. |
| repository  | array  | [Github repository details where the playbook is related to the job is present.](#repoEntity) |
| hosts       | array  | [Hosts entity schema](#hostsEntity) |
| callbacks   | array  | Call back webhook urls where you would like to view live feed of job status. |
| createdTime | integer | Timestamp when the Job was created. |
| lastUpdatedTime | integer | Timestamp when the Job was last updated. |
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
    {
    	"totalSize": 2000,
    	"page": 0,
    	"size": 100,
    	"results": [
				      {
				        "id": "1111505e-6773-494a-b2bf-d2cc2684710d",
				        "accountAlias": "XXXX",
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
				          {
				          	"url": "your callback webhook",
				          	"level": "DEBUG"
				          }
				        ],
				        "createdTime": 1440785845177,
				        "lastUpdatedTime": 1440785845177,
				        "links": [
				          {
				            "ref": "self",
				            "id": "52f9505e-6773-494a-b2bf-d2cc2684710d",
				            "href": "/v2/workflow/XXXX/jobs/52f9505e-6773-494a-b2bf-d2cc2684710d",
				            "verbs": [
				              "GET",
				              "POST",
				              "DELETE"
				            ]
				          }
				        ]
				      }
    	]
	}