{{{ "title": "Getting started with Automation", "date": "08-19-2015", "author": "Shan Sundaram", "attachments": [] }}}

The CenturyLink Cloud Automation Job actions can be performed via REST API calls. The API works with JSON messages over HTTP. It relies on the standard HTTP verbs including GET, POST, PUT, DELETE, and PATCH.

The URL format of the service is: https://api.ctl.io/v2/automation/{resource}/{account alias}. 
### As an example, 
To retrieve all the Jobs created at the account alias level, you would issue a GET request to https://api.ctl.io/v2/automation/jobs/ALIAS. The HTTP request must include headers Content-Type (set to application/json) and Authorization (set to 'Bearer Token from authentication API').

### HTTP Response Codes

The service responds to requests using standard [HTTP codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), and if applicable, a JSON payload.

| HTTP CODE |	DESCRIPTION |
| :--- | :--- |
| 200 | OK. Sent when requests are immediately successful. |
| 400 | BAD REQUEST. Sent when something is wrong with the query string or message body. |
| 401 | UNAUTHORIZED. Sent when a bearer token is not provided. |
| 403 | FORBIDDEN. Sent if the request violates the security demands of the service. |
| 404 | NOT FOUND. Sent if the URL points to a non-existent resource. |
| 500 | INTERNAL SERVER ERROR. Sent if the service experiences an error through no fault of the user. |
| 503 | SERVICE UNAVAILABLE. The server is currently unavailable (because it is overloaded or down for maintenance). Generally, this is a temporary state. |
| 504 | GATEWAY TIMEOUT. The server was acting as a gateway or proxy and did not receive a timely response from the upstream server. |