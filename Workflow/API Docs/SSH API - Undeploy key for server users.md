{{{ "title": "Undeploy key for server users", "date": "08-31-2015", "author": "Shan Sundaram", "attachments": [] }}}

Undeploy key pair for a specific server user. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to undeployed a key pair for certain server users.

## URL

### Structure

    DELETE https://api.qa.automation.ctl.io/keypairs/{accountAlias}/{keypairAlias}/{serverId}
    

### Example

    DELETE https://api.qa.automation.ctl.io/keypairs/ALIAS/TestGroup/UC1ACCTUBUSVR04
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| keypairAlias | string | Categorize and manage your keys with an alias name. | Yes |
| serverId | string | Server Id for which the key has to be undeployed for a specific user. | Yes |

### Content Properties

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| usernames | array | Array of server usernames for which the keys have to be undeployed. |

### Example
   
    JSON
    {
    	"usernames": ["admin"]
    }

## Response


The response will not contain JSON content, but should return a standard HTTP <code>200 OK</code> response upon key has been undeployed for the server user name.

