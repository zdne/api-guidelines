# Asynchronous Tasks
If an API operation is asynchronous, but its progress could be tracked by a client, the response to such an asynchronous operation **MUST** return, in the case of success, the **202 Accepted** status code together with a `application/hal+json` representation of a new **task-tracking resource**. 


## Task Tracking Resource
The task-tracking resource **SHOULD** convey the information about the status of an asynchronous task. 

Retrieval of such a resource using the HTTP GET Request Method **SHOULD** be designed as follows:

1. Task is Still Processing

    Return **200 OK** and representation of the current status.

2. Task Successfully Completed

    Return **303 See Other** together with [HTTP Location Header](https://tools.ietf.org/html/rfc7231#section-7.1.2) with URI or a outcome resource.

3. Task Failed

    Return **200 OK** and `application/problem+json` with the problem detail information on the task has failed.
