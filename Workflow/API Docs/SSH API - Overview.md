The CenturyLink Cloud Automation's SSH Key Management Service will help you to manage and deploy SSH credentials to machines involved in an automation job. This service enables the job service to gain access to any machine in order to run a task. SSH Key management is also one of the most requested features on CenturyLink Cloud.

These actions can be performed via REST API calls. The API works with JSON messages over HTTP. It relies on the standard HTTP verbs including GET, POST, PUT and DELETE.

The URL format of the service is: https://api.qa.automation.ctl.io/keypairs/{account alias}. 

### As an example, 
To retrieve information of all deployed keypairs created at the account alias level, you would issue a GET request to https://api.qa.automation.ctl.io/keypairs/ALIAS. The HTTPS request must include headers Content-Type (set to application/json) and Authorization (set to 'Bearer Token from authentication API').

### HTTP Response Codes

The service responds to requests using standard [HTTP codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), and if applicable, a JSON payload.

| HTTP CODE |	DESCRIPTION |
| :--- | :--- |
| 200 | OK. Sent when requests are immediately successful. |
| 400 | BAD REQUEST. Sent when something is wrong with the query string or message body. |
| 401 | UNAUTHORIZED. Sent when a bearer token is not provided or an invalid token. |
| 403 | FORBIDDEN. Sent if the request violates the security demands of the service. |
| 404 | NOT FOUND. Sent if the URL points to a non-existent resource. |
| 500 | INTERNAL SERVER ERROR. Sent if the service experiences an error through no fault of the user. |
| 503 | SERVICE UNAVAILABLE. The server is currently unavailable (because it is overloaded or down for maintenance). Generally, this is a temporary state. |
| 504 | GATEWAY TIMEOUT. The server was acting as a gateway or proxy and did not receive a timely response from the upstream server. |
