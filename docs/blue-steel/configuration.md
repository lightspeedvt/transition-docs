#Initialization

Upon page load the javascript file `bootstrap.js` is loaded. This file handles the initial preload and "bootstrapping" of the application as well as defining some utility classes and functions.  

Let's take a look at the `script` tag and point out a few things of note:
```
<script id="blue-steel-boot" data-version="5.191.0" data-config="data/static/global.json" src="js/bootstrap.js?5.191.0"></script>
```
| Attribute | Description |
|-----------|-------------|
| `data-version` | Used to cache-bust application files and should be updated if any of the core files are modified|
| `data-config` | Defines the JSON resource that configures the application |
| `src` | Path to bootstrap.js with version number, should be the same as the `data-version` attribute |
| `data-theme` | Defines the "theme" to use for loading module views. See [Configuring The View](modules/#configuring-the-view) for more information. |


#Configuration

The application uses a JSON configuration that is generated server-side via Coldfusion. To see a full example, log in and access the service at `/tc/data/global.cfm?format=json`  

Once the application has loaded the config can be accessed using the following code snippet:

```js
var app = lsvt.core.Application.getInstance();
console.log( app.config );
``` 

***

###Globals

The config service is useful for setting global values that can be used throughout the application or in specific areas. You can see some example globals in the snippet below. 

```json
{
    "allowNavigation": true,
    "allowFavorites": true,
    "allowRatings": true,
    "allowSharing": true,
    "allowEditing": true,
    "showRecent": false,
    "showChapterExtras": true,
    "errors": {
        "assessment": {
            "message": "There was a problem evaluating these answers.",
            "detail": "Please contact <a href='mailto:support@lightspeedvt.com'>support@lightspeedvt.com</a> and provide the first name, last name and email address used for this assessment."
        }
    }
```
***

###Modules

Modules are essentially "pages" inside the application. They are loaded, intialized, and rendered by the application using a *"convention over configuration"* approach. This means that instead of a detailed configuration, you simply follow a few "conventions" in order to get your modules to load and display in the application.

The first convention used in creating a module is to list it inside of the `modules` object of the application config. Typically the only property of the object will be `version` which helps to cache-bust the assets that the module consists of. Below is a small snippet of what that looks like.  

> For more information please view the [Modules Page](modules).

```json
    "modules": {
        "trainingcenter": {
            "category": {
                "version": "5.216.0"
            }
            ...
        }
    }
```
***

###Resources

Resources are the service URLs at which the application sends and receives data. After referencing them in the config you'll use the method `app.loadResource(resourceName, config)` to invoke the service. The configuration object should conform to [jQuery's Ajax API](http://api.jquery.com/jquery.ajax/).

> For more information please view the [Resources Page](resources).

```javascript
app.loadResource( "category", {
    data:{id:id},
    success:configLoaded
});
```

```json
    "resources": {
        "category": "data/category.cfm"
        ...
    }
```
