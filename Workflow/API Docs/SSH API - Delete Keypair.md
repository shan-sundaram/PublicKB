{{{ "title": "Delete Key pairs", "date": "08-31-2015", "author": "Shan Sundaram", "attachments": [] }}}

Delete deployed SSH credentials to Centurylink servers. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to remove a deployed key pair from your Centurylink account alias.

## URL

### Structure

    DELETE https://api.qa.automation.ctl.io/keypairs/{accountAlias}/{keypairAlias}
    

### Example

    DELETE https://api.qa.automation.ctl.io/keypairs/ALIAS/TestGroup
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| keypairAlias | string | Categorize and manage your keys with an alias name. | Yes |

### Example
   
    https://api.qa.automation.ctl.io/keypairs/accountalias/TestGroup

## Response

The response will not contain JSON content, but should return a standard HTTP <code>200 OK</code> response upon deletion of the keypair.

