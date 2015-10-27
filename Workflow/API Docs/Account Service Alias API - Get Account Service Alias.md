{{{ "title": "Get Account Service Alias", "date": "10-15-2015", "author": "Shan Sundaram", "attachments": [] }}}

The Account Service alias is a secure store of a users credentials. These credentials are associated with a Job and a Schedule. The credentials are stored in a secure format seperate from the job definition and other account identifying elements. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use to view all the account service alias under your CenturyLink account. 

## URL

### Structure

    GET https://api.qa.automation.ctl.io/serviceAccounts/{accountAlias}

### Example

    GET https://api.qa.automation.ctl.io/serviceAccounts/XXXX

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code of your CenturyLink Account Alias. | Yes  |

## Response

Array of all account service alias created under your Centurylink Account.

### Entity Definition

| Name        | Type   | Description |
| :----------- | :------ | :--- |
| accounts | array | List of Account Service Alias created. |

### Examples

    JSON
    {
  		"accounts": [
		    "demo-account-service-account1",
		    "demo-account-service-account2",
		    "demo-account-service-account3",
		    "demo-account-service-account4"
	  ]
	}