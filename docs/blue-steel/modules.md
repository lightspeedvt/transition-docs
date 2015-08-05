#Modules
A "module" is composed of a viewmodel and view. In the application, modules are typically top-level only and control or compose their own children/submodules.

***

###Convention Over Configuration
Modules are composed by the application at run-time based on a few factors:  

- `modules` Configuration Object
- URL/Deeplink Value
- "Theme" Path

***

###Configuring Modules
The [JSON configuration](configuration) contains a `modules` property that looks like this:

```json
    "modules": {
        "trainingcenter": {
            "category": {
                "version": "5.216.0",
                "name": "category-redux"
            }
            ...
        }
    }
```  
<br>

**Module Configuration Attributes:**  

- **Path**  
The **path** to the config object is related directly to the url routing system. In the example above, when the url `#/trainingcenter/category` is accessed, the "category" module will be loaded and displayed.  

- **Version**  
The `version` property is appended to all asset requests and serves to "cache-bust" files. It's **vitally important** that you update this value when releasing updates to production. Failure to do so could cause errors for users that have the previous version cached.  
  
- **Name**  
The `name` property allows the application to load files that are not directly correlated to the module name. This is helpful when you want to load a different module based on server-side logic. The current example would be the "topic style" categories menu which is used on a per client basis.

***

###Defining a Module
When the application's url is changed it will look for a corresponding module definition based on the configuration. If the module has not been defined it will attempt to load a javascript file from the `js/modules` directory.  
  
Building off of our configuration above, that file would be: `js/modules/trainingcenter/category.js`.  
  
Inside `category.js` we will define the module like so:

```js
defineModule( "trainingcenter/category", function( app, model ) {
    // Any methods or properties that you add to the "model" instance here
    // will be available to your view for data-binding
}
```

***

###Configuring The ViewModel
The `model` argument contains your viewmodel instance. The following methods are predefined and should be overridden in order for you module to work:

```js
model.initialize = function(deeplink) {
    // This method is called before the module is rendered and is typically
    // used to load a resource and configure the view model
    // The "deeplink" argument is an array of the url parts *after* the module name
    // If we accessed #/trainingcenter/category/foo/bar it would be ['foo','bar']
};

model.onDeeplink = function(deeplink) {
    // This method is called if the url is changed after rendering
    // AND the module name/path does NOT change
    // Based on the code above the change could be #/trainingcenter/category/new/deeplink
};

// This method should be called once your configuration and any
// additional assets have been fully loaded.
// It supports a float value from 0-1 and can be used for preloading
model.setPercentLoaded(1);
```

***

###Configuring The View
Views are HTML fragments that are bound to the ViewModel and rendered to the page. The JSON configuration contains a `themes` property that looks like this:

```json
    "themes": {
        "default": {
            "path": "themes/lsvt/"
            ...
        }
    }
```
The active theme is set to "default" unless specified in the `data-theme` attribute of the `<script>` tag. See the [Overview Page](overview/#initialization) for more information.  
  
Once the active theme has been determined the application will load your views from the `path` property. This allows you to create a completely new front end while using the core of the application logic and module definitions.  
  
The convention used to locate views is `theme path + module name + .html` which would cause our "category" example to be located here: `themes/lsvt/trainingcenter/category.html`

***

###Anatomy of a View
Views are simply HTML using Knockout's template syntax. They are bound to the viewmodel and have access to its methods and properties.
>Running through <http://learn.knockoutjs.com> can help you learn the syntax and better understand templates.

***

###Loading View-Specific Assets
Views also provide a special "preload" comment that allows you to preload files related to your view. These files can be anything YepNope supports, images, css, javascript etc. You'll need to place it on the first line of your template like so:
```html
<!-- preload: assets/category.js, assets/category.css -->
```
Note that any images within the css files will be preloaded as well and your module will not be rendered until this process has been completed. Paths are relative to the current template's location.  
  
  ***

###Extending ViewModels
Views should load an additional .js file (via the preload comment) that will extend/decorate the viewmodel. The intention here is that views should be animated and will need to notify the application when they are complete.

```js
(function(){
    var app = lsvt.core.Application.getInstance(); // Get the app instance
    var view = new lsvt.core.View("trainingcenter/category"); // Create a view instance
    var model = app.getModel( "trainingcenter/topics" ); // Get the viewmodel instance
    
    // Add methods, etc to the viewmodel
    model.myViewSpecificFunctionality = function() {
        $('.someViewElement').doSomethingSpecial();
    };

    view.rendered.add(function(){
        // Do some transitioning in, or target specific elements
    });

    view.ended.add(function(){
        // Do some transitioning out, or cleaning up then
        view.complete();
    });
    
})();

```
