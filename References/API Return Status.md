### References

#### [Back to official documents](../README.md) | [Country Code](Country%20Code.md) | [ISO 3166](ISO%203166.md)

### API Return Status

| Status Code | Description           | Meaning                                                                                                     |
| ----------- | --------------------- | ----------------------------------------------------------------------------------------------------------- |
| 200         | OK                    | The request was successful.                                                                                 |
| 201         | Created               | The request was successful, and a resource was created.                                                     |
| 204         | No Content            | The request was successful, but there is no content to send in the response.                                |
| 400         | Bad Request           | The request could not be understood or was missing required parameters.                                     |
| 401         | Unauthorized          | Authentication failed or user does not have permissions for the requested operation.                        |
| 403         | Forbidden             | Authentication succeeded, but the authenticated user does not have access to the requested resource.        |
| 404         | Not Found             | The requested resource could not be found.                                                                  |
| 500         | Internal Server Error | An error occurred on the server.                                                                            |
| 502         | Bad Gateway           | The server was acting as a gateway or proxy and received an invalid response from the upstream server.      |
| 503         | Service Unavailable   | The server is currently unavailable (because it is overloaded or down for maintenance).                     |
| 504         | Gateway Timeout       | The server was acting as a gateway or proxy and did not receive a timely response from the upstream server. |
