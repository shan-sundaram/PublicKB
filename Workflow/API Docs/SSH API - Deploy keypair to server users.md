{{{ "title": "Deploy keypair for Server users", "date": "08-31-2015", "author": "Shan Sundaram", "attachments": [] }}}

Add server users for a deployed SSH keypair. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to add server users to an already deployed key pair.

## URL

### Structure

    POST https://api.qa.automation.ctl.io/keypairs/{accountAlias}/{keypairAlias}/{serverId}
    

### Example

    POST https://api.qa.automation.ctl.io/keypairs/ALIAS/TestGroup/UC1ACCTUBUSVR04
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| keypairAlias | string | Categorize and manage your keys with an alias name. | Yes |
| serverId | string | Server Id for which the key(s) is deployed. | Yes |

### Content Properties

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| usernames | array | Array of additional server usernames to be authorized with the key. |

### Example
   
    JSON
    {
    	"usernames": ["admin"]
    }

## Response


The response will not contain JSON content, but should return a standard HTTP <code>200 OK</code> response upon new server user name addition.

