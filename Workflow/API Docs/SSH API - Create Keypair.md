{{{ "title": "Create Key pair", "date": "08-31-2015", "author": "Shan Sundaram", "attachments": [] }}}

Creates and deploys SSH credentials to Centurylink servers in a given account, so the keys can be used to authenticate these servers when executing automation jobs. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create, deploy and manage SSH keys to machines involved in an automation job. 
</br> *Note: The SSH privateKey is generated only once, so you have to save the privatekey from the response.*

## URL

### Structure

    POST https://api.qa.automation.ctl.io/keypairs/{accountAlias}/{keypairAlias}
    

### Example

    POST https://api.qa.automation.ctl.io/keypairs/ALIAS/TestGroup
    

## Request

### URI Parameters

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| accountAlias | string | Short code for a particular account. | Yes  |
| keypairAlias | string | Categorize and manage your keys with an alias name. | Yes |

### Content Properties

| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :---- |
| deployToServers | array | [Array list of servers and their user names](#serverEntityRequest) | Yes |
| publicKey | string | The SSH publicKey to be deployed for the servers.  | Yes |

### Server Entity <a name="serverEntityRequest"></a>
| NAME         | TYPE   | DESCRIPTION                         | REQ. |
| :------------ | :------ | :----------------------------------- | :--- |
| serverId | string | Server Id for which the key to be deployed. | Yes |
| usernames | array | Array of server usernames to be authorized with the key. | Yes |

    JSON 
    "deployToServers": [
    	{
      		"serverId": "UC1ACCTUBUSVR04",
      		"usernames": ["username1", "username2"]
    	}

### Example
    JSON
    {
	  	"deployToServers": [
	    	{
	      		"serverId": "UC1ACCTUBUSVR04",
	      		"usernames": [ "root"]
	    	}
	    ],
		"publicKey" : "ssh-rsa CYXYXHXY3NzaC1yc2EAAAADAQABAAABAQCzlVmtYqqf5xIZSfrfUVHtznl661/GWr5yNrGwUQiRiGHXKeS1L05lD/XNpm3RVNwpo5hOwN++8MqnSxktCphmoHYjaNgMaKk98184uhPzjWNOl++r3uIrkAssPHPNNgibROnJuxkz+JTqewfU1e4c4HmnRxlcb6L3HBAssku820gNuL7E2VR418KilQtbmdhqkAEICTtHfgUsg7Loer8BIwJpqhhHkAwRpsEYC4x2fNjfqHmzLhhPWc1x+Bsn3OC1Gju+049z3UzjhD4YjZ4mwZO1cmAflOJwUPLnUeYvUj3D5nGN+4li2lCoOl3aJvmYr9triUlZNSx0Ug42vKgh abc.def@fghijk.com"
    }

## Response

The response will be an object with the key deployed to servers.

### Entity Definition

| Name        | Type   | Description |
| :----------- | :------ | :--- |
| alias | string | The custom alias name provided to categorize your keys. |
| privateKey | string | The SSH privateKey is generated only once, so you have to save the privatekey for future reference. |
| publicKey | string | The SSH publicKey deployed for the servers. |
| deployedServers | array | [Array list of servers and their user names](#serverEntityResponse) |


### Server Entity <a name="serverEntityResponse"></a>
| NAME         | TYPE   | DESCRIPTION                         |
| :------------ | :------ | :----------------------------------- |
| serverId | string | Server Id for which the key(s) is deployed. |
| usernames | array | Array of server usernames to be authorized with the key. |

### Examples

    JSON
    {
	  "alias": "TestGroup",
	  privateKey: "-----BEGIN RSA PRIVATE KEY----- XIEOASASASASBAAKCAQEAjwQqT3qD2ocGJDjVEXrt1SV72mtvco/z9z4poXzGL0qH90+6 VnYTRtyEMrnkxEl4FuRh+B4gWQTvX8x4Nb+KZpfuvo0AG1EX8v9I/T7uTqlh2Zwv jL1wVngrf7Q+qCcwtTFQEnbb5F/dC+FlTowfwleLn08/qHoO/eg+QAhWp7PbPMQN i5qYtEUCxsfhZGMv/SfCTG6zstubWTNJtQjCqpbW1eVFFrtIcvkKOoNCASz+iDdj PS4FD9GRdyzyLYfMUlZHviLAsEZsFMiMyxV4MYdsdjqEOq5ed+GM28YQ9Aq0Tr3B dykoQYkzHeXz1SfqujMPYShuxkGIStke5Y5BVQIDAQABAoIBAQCKBE0IsoU4iQHG Rwpoeie3gRsLaI7/Eikwu07Vx2JDFTwt0UVUV1K3GeyCP5+kRfqcrP5WwkwZXIfd /acsx5I6+/is78ngktv356F6tBaq1w/VP8MroU4eRI5GCZ5GDLwWwGYzy3zd4h2i b3yi1tt3Y6EctxAJ+PEq28vnY6Ss5Y4KoazDdzFwfBSclPBsDQfkFTs0xuh7yDuz VoyY5lPl7U73WKwQjA558CT0fk2VI4hbTU6axBHpCQBXI0JA2LrguUZSSpvo6xVA 4upCLb5eOYkaOKScn5/Ttag5f7AR6Lq2pMs8QFxP4hdB/QBIgrs+Vcr1OjpEAjbA oyUeew0pAoGBAOvf2B8+S0SzZs4aMJdtUgRoAQC3AvsQZ/ow0lLb0CDjhm1ACEk/ SrEykvB+AU5tgITNII+8cCJ4NwfYtqFlhrqV1JQGb6D/ANTm4GW2UchVEnHCxwm7 G7BbLDn/2wgIC+MCUhx53tXEG3winA4vHCr8wNpnT8huficTEIbvzXrzAoGBAJs4 CkyPVf68cqVsgoMbOSU7OTNIfW/YpbWoLe5oQ0IIVx815vGF6z1cTRL5YTamNzli qi21l/zp9Eb+VllxYTP1LHQZCOKnv2aju/zeDky/56tPhdfyOg7pRbqtc3W3m2M+ lFMA2pqR9wQKh/zLlo+0suyZZKlL8zp6ZIknsVSXAoGAOl3co/aNN4XRJaTzazUg +3gk72FZ+nhX0mAsW1aLTOggRn52znE78VcbZyk294o/KB1+NjMh6FWpAGcO4ic2 NMJHIUHUYHJGHJGJHG+Qv0T3oncY3ttODrzfl5YKWMAE928jjy8JVF8qt7lGPsf4yNuFdD72csiHU LYr3ydOQuX8l9lNQXqOOTCMCgYBrZB+EDtvBrmJn36aAzTIBd3NA7xOSccNc5uo4 e7ylEB4vAt0xF6XFQ3oz+YRwChpFQuVZUL3Ch5+yCsB1i8Nj7mp+PN/v6X28puYm swATy+aemRuSaA4RSQYsfVtYA9unk6GNuBaHQRw1mI+zsKwP60ar+gkyNNEpEYtD dcn0KwKBgQCXO6TBtKeI/MVOgrzQR3f9xg6qapypfxxpW/ozAyOPAwtRvFUmfjJ9 jOPvQ1v04V+Fk3uoKtVZISoIr6GHt30a5G37Vqo31R+ZHWpOfJhX5IC9undOKqD5 IaDNaDTkxMlmnn+yVVZrhI4NZwk2aRCl5UxgOm7upM7ezqzt3jM0aA== -----END RSA PRIVATE KEY----- "
	  "publicKey": "ssh-rsa CYXYXHXY3NzaC1yc2EAAAADAQABAAABAQCzlVmtYqqf5xIZSfrfUVHtznl661/GWr5yNrGwUQiRiGHXKeS1L05lD/XNpm3RVNwpo5hOwN++8MqnSxktCphmoHYjaNgMaKk98184uhPzjWNOl++r3uIrkAssPHPNNgibROnJuxkz+JTqewfU1e4c4HmnRxlcb6L3HBAssku820gNuL7E2VR418KilQtbmdhqkAEICTtHfgUsg7Loer8BIwJpqhhHkAwRpsEYC4x2fNjfqHmzLhhPWc1x+Bsn3OC1Gju+049z3UzjhD4YjZ4mwZO1cmAflOJwUPLnUeYvUj3D5nGN+4li2lCoOl3aJvmYr9triUlZNSx0Ug42vKgh abc.def@fghijk.com",
	  fingerprint: "6d:3e:d2:6a:c7:85:58:0b:2f:13:c3:be:e0:bf:20:0c",
	  "deployedServers": [
	    {
	      "serverId": "UC1ACCTUBUSVR04",
	      "usernames": ["root"]
	    }
	  ]
	}