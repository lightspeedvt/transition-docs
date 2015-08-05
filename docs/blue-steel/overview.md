#Blue-Steel Introduction

"Blue Steel" is/was the code-name for the HTML based "Training Center" component of the LightSpeed VT platform. It was originally built to be a feature-complete recreation of the previous Flash-based Training Center.  

Due to the lack of a suitable "Single-Page App" framework at the time of development a custom solution was developed and remains in use today. The core of the functionality is based on [KnockoutJS](http://knockoutjs.com) and makes heavy use of client-side templates and two-way data binding.  

There are a number of third party libraries and utilities as well as a healthy dose of custom Javascript. This documentation will aim to provide a general outline of the inner-workings and thought process behind Blue Steel's development.

***

###3rd Party Tools

| Name | Usage |
|------|-------|
| [jQuery](http://jquery.com)  | XHR Requests, DOM selection, Animation, Utility Methods (`$.extend`, etc) |
| [jQueryAddress](http://www.asual.com/jquery/address/) | URL Routing, Deeplinking |
| [Class.extend](http://ejohn.org/blog/simple-javascript-inheritance/) | Classical Inheritance |
| [TweenMax](http://www.greensock.com) | Animation |
| [JS Signals](http://millermedeiros.github.com/js-signals/)| Event Delegation |
| [Yepnope](http://yepnopejs.com) | Asset Loading (CSS, HTML, JS, Images) |

***

###Deployment
The files are located in the `/tc/` directory of the main LightSpeed VT application. There is currently no build step involved and all assets load asynchronously via YepNope and custom extensions.

***

###Local Development
The application can be run locally using static assets. The recommended configuration is to map a virtual host to the `/tc/` directory and use the domain `http://bluesteel.lightspeedvt.com` which will allow certain domain specific things (like fonts) to load correctly.  
  
The JSON services are replicated in the `/tc/data/static/` directory and can be manipulated for testing purposes.

***

###Boilerplate vs. Non-Boilerplate
Blue-Steel was initially developed before the Boilerplate and had it's own separate set of requirements. Once the Boilerplate was implemented there were some shared resources so a few alternative files were created to support the transition, they are listed in the following table:

**Original File:** `themes/lsvt/main.html`  
**Boilerplate File:** `themes/lsvt/main-boilerplate.html`

This file defines the "outer" page structure of the application. When Boilerpate is OFF, it renders the navigation and other global elements which the Boilerplate provides.

**Original File:** `index-boilerplate.cfm`  
**Boilerplate File:** `index-legacy.cfm`

The `legacy` file includes the html, head and body tags which are removed in favor of includes inside the `boilerplate` file.
