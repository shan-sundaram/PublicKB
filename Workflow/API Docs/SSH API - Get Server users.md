{{{ "title": "Get Server users", "date": "08-31-2015", "author": "Shan Sundaram", "attachments": [] }}}

Get server usernames for a deployed SSH keypair. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get the list of usernames (of a specific server) for deployed key pairs.

## URL

### Structure

    GET https://api.qa.automation.ctl.io/keypairs/{accountAlias}/{keypairAlias}/{serverId}
    

### Example

    GET https://api.qa.automation.ctl.io/keypairs/ALIAS/TestGroup/UC1ACCTUBUSVR04
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| keypairAlias | string | Categorize and manage your keys with an alias name. | Yes |
| serverId | string | Server Id for which the key(s) is deployed. | Yes |

### Example
   
    https://api.qa.automation.ctl.io/keypairs/accountalias/TestGroup/UC1ACCTUBUSVR04

## Response

The response will be server usernames (listed as array of string) for a deployed SSH keypair.

<code>["root"]</code>

