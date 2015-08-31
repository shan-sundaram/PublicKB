{{{ "title": "Get Deployed Key pairs", "date": "08-31-2015", "author": "Shan Sundaram", "attachments": [] }}}

To get the details of deployed SSH credentials to Centurylink servers. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to retrieve the details of deployed key pair to your Centurylink account alias.

## URL

### Structure

    GET https://api.qa.automation.ctl.io/keypairs/{accountAlias}/{keypairAlias}
    

### Example

    GET https://api.qa.automation.ctl.io/keypairs/ALIAS/TestGroup
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| keypairAlias | string | Categorize and manage your keys with an alias name. | Yes |

### Example
   
    https://api.qa.automation.ctl.io/keypairs/accountalias/TestGroup

## Response
The response will be an object with the key deployed to servers.

### Entity Definition

| Name        | Type   | Description |
| :----------- | :------ | :--- |
| alias | string | The custom alias name provided to categorize your keys. |
| publicKey | string | The SSH publicKey deployed for the servers. |
| deployedServers | array | [Array list of servers and their user names](#serverEntityResponse) |


### Server Entity <a name="serverEntityResponse"></a>
| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| serverId | string | Server Id for which the key(s) is deployed. |
| usernames | array | Array of server usernames to be authorized with the key. |

	JSON
	{
		alias: "TestGroup"
		publicKey: "ssh-rsa CYXYXHXY3NzaC1yc2EAAAADAQABAAABAQCzlVmtYqqf5xIZSfrfUVHtznl661/GWr5yNrGwUQiRiGHXKeS1L05lD/XNpm3RVNwpo5hOwN++8MqnSxktCphmoHYjaNgMaKk98184uhPzjWNOl++r3uIrkAssPHPNNgibROnJuxkz+JTqewfU1e4c4HmnRxlcb6L3HBAssku820gNuL7E2VR418KilQtbmdhqkAEICTtHfgUsg7Loer8BIwJpqhhHkAwRpsEYC4x2fNjfqHmzLhhPWc1x+Bsn3OC1Gju+049z3UzjhD4YjZ4mwZO1cmAflOJwUPLnUeYvUj3D5nGN+4li2lCoOl3aJvmYr9triUlZNSx0Ug42vKgh abc.def@fghijk.com"
		deployedServers: [
		{
			serverId: "UC1ACCTUBUSVR04"
			usernames: ["root"]
		},
		{
			serverId: "UC1ACCTUBUSVR05"
			usernames: ["root"]
		}
	}

