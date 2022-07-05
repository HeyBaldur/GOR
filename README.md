
# GOR (Generic Operation Response)

GOR by its acronym (Generic Operation Response) is a useful way to work with generic responses that speed up the evaluation of server responses. 
This helps developers to display better information in the responses that come from an HTTP request, such as GET, POST, DELETE or UPDATE.

## How does it work?

Once we install the GOR package, we can use it as follows:

```
/// <summary>
/// Here we are returning 3 important things 
/// 1. Validation if there is an error
/// 2. A message to user or to the UI developer
/// 3. Status server code which it will be 200, 404, 500...
/// </summary>
/// <returns></returns>
public async Task<GenericOperationResponse<string>> DoSomething()
{
    // Write your logic here

    return new GenericOperationResponse<string>(false, "Message to user or front-end developer", HttpStatusCode.OK);
}
```
We also use the `ENUM HttpStatusCode` to indicate the response from the server.

## HTTP response status codes

The HttpStatusCode enumeration contains the values of the status codes defined in RFC 2616 for HTTP 1.1. 
The status of an HTTP request is contained in the HttpWebResponse.StatusCode property.
If the HttpWebRequest.AllowAutoRedirect property is false, the following enumeration values cause an exception to be thrown:

- Ambiguous
- Found
- MultipleChoices
- Redirect
- RedirectKeepVerb
- RedirectMethod
- SeeOther
- TemporaryRedirect

Another example:

```
public async Task<GenericOperationResponse<string>> DoSomething()
{
    try
    {
        // This can be any other model
        string response = "My DB response"; 

        return new GenericOperationResponse<string>(response, "Operation was OK", HttpStatusCode.OK);
    }
    catch (Exception ex)
    {
        // Here we tell the user or the UI: There is an error, the error and the server code
        return new GenericOperationResponse<string>(true, ex.ToString(), HttpStatusCode.InternalServerError);
    }
}
```

## Why do we use GOR?
Generally in statements like try-catch or other places in the code we also prevent the API from having failures and stop working for no reason, that's why we create GOR and so we can map everything that really happens during execution.

An excellent recommendation is also to use `ILogger` to have better control.
