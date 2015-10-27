{{{ "title": "Create Account Service Alias", "date": "10-15-2015", "author": "Shan Sundaram", "attachments": [] }}}

The Account Service alias is a secure store of a users credentials. These credentials are associated with a Job and a Schedule. The credentials are stored in a secure format seperate from the job definition and other account identifying elements. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API to create account service alias under your CenturyLink account and use this alias for executing scheduled jobs.

## URL

### Structure

    POST https://api.qa.automation.ctl.io/serviceAccounts/{accountAlias}

### Example

    POST https://api.qa.automation.ctl.io/serviceAccounts/XXXX

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code of your CenturyLink Account Alias. | Yes  |

### Entity Definition
| Name        | Type   | Description | REQ. |
| :----------- | :------ | :--- | :--- |
| alias | string | Enter your Account Service Alias name. | Yes |
| username | string | Your CenturyLink Account username. | Yes |
| password | string | Your CenturyLink Account password.| Yes |

## Response

Details of the new account service alias created.

### Entity Definition

| Name        | Type   | Description |
| :----------- | :------ | :--- |
| id | string | id of your new Account Service Alias. |
| accountAlias | string | Short code of your CenturyLink Account Alias. |
| alias | string | Your Account Service Alias name. |
| username | string | Your CenturyLink Account username. |
| password | string | Your CenturyLink Account password.|

### Examples

    JSON
    {
	  "id": "729e3136-c474-42fb-976e-53786f5fb000",
	  "accountAlias": "XXXX",
	  "alias": demo-account-service-account1,
	  "username": "your-username",
	  "password": "your-password"
	}