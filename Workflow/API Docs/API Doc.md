The CenturyLink Cloud Automation actions can be performed programmatically via API. The API is RESTful and works with JSON messages over HTTP. It relies on the standard HTTP verbs including GET, POST, PUT, DELETE, and PATCH.

The URL format of the service is: https://api.ctl.io/v2/automation/{resource}/{account alias}. As an example, to retrieve all the Jobs created at the account alias level, you would issue a GET request to https://api.ctl.io/v2/automation/jobs/ALIAS. The HTTP request must include headers Content-Type (set to application/json) and Authorization (set to 'Bearer bearer token from authentication API' .

### HTTP Response Codes

| HTTP CODE |	DESCRIPTION |
| :--- | :--- |
| TBD | TBD |
