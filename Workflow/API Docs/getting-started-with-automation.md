{{{ "title": "Getting started with Automation", "date": "08-19-2015", "author": "Shan Sundaram", "attachments": [] }}}

The CenturyLink Cloud Automation actions can be performed via REST API calls. The API works with JSON messages over HTTP. It relies on the standard HTTP verbs including GET, POST, PUT, DELETE, and PATCH.

The URL format of the service is: https://api.ctl.io/v2/automation/{resource}/{account alias}. 
### As an example, 
To retrieve all the Jobs created at the account alias level, you would issue a GET request to https://api.ctl.io/v2/automation/jobs/ALIAS. The HTTP request must include headers Content-Type (set to application/json) and Authorization (set to 'Bearer Token token from authentication API').

### HTTP Response Codes

| HTTP CODE |	DESCRIPTION |
| :--- | :--- |
| `TBD` | `TBD` |