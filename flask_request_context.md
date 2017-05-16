# Flask Context

### Application Context
[Flask Documentation: Application Context](http://flask.pocoo.org/docs/0.12/appcontext/)
### Request Context (context locals)
[Flask Documentation: Request Context](http://flask.pocoo.org/docs/0.12/reqcontext/)

#### The Request Cycle

1. Before each request, before_request() functions are executed. If one of these functions return a response, the other functions are no longer called. In any case however the return value is treated as a replacement for the view’s return value.
2. If the before_request() functions did not return a response, the regular request handling kicks in and the view function that was matched has the chance to return a response.
3. The return value of the view is then converted into an actual response object and handed over to the after_request() functions which have the chance to replace it or modify it in place.
4. At the end of the request the teardown_request() functions are executed. This always happens, even in case of an unhandled exception down the road or if a before-request handler was not executed yet or at all (for example in test environments sometimes you might want to not execute before-request callbacks).
