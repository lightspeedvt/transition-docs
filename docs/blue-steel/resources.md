#Resources
Other than composing modules and rendering the ui, loading and sending data is one of the core functions of the application. It's pretty simple but has some important things to keep in mind when using external resources.

***

###Example Request
```js
app.loadResource( "course", {
    data: {id:id},
    success: configLoaded,
    abort: false,
    showError: false,
});
```

***

###API
The `loadConfig` method supports three arguments:  

- **resourceName**  
The name of a resource from the JSON config

- **configObject**  
A config object that conforms to the [jQuery AJAX api](http://api.jquery.com/jquery.ajax/) and has a few extra properties (detailed below)

- **notifyApp**  
Boolean - By default when a resource is loaded the ui will be covered and a loading animation shown. Passing `false` will prevent it from showing.

***

###Config Properties
The config object has a few special properties that you can pass:

- **abort**  
Boolean - By default, loading a resource will "abort" any previous calls that are pending. Passing `false` will prevent that behavior.

- **showError**  
Boolean - By default, server faults will be shown. Passing `false` will suppress them.

***

###Errors
The server can send back custom error messages that will be displayed in a modal dialog. This is achieved by setting an `error` object in the JSON response. They look like this:

```json
"error" : {
    "type" : "NoAccess",
    "message" : "Oops! You don't have access to this content...",
    "detail" : "This content is not currently available for your account. Sorry about that!",
    "showReload" : false
}
```

***

###Redirects
In some cases you may want to redirect the user when they load a resource. To do so simply add a `redirect` property to the JSON response. This will change the url and proceed as expected.

```json
"redirect" : "trainingcenter/course/courseid"
```
