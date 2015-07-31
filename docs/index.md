#Introduction
The "Boilerplate" is the most basic component of the LightSpeed VT platform and represents the global UI of the system. It may help to think of it as the "Page Template" of the system. The components of the Boilerplate are as follows:

* **"Hamburger Menu"**  
Can be hidden or shown by the user and contains links to most areas of the system. Intended to provide quick and convenient access for users.

* **Page Header**  
Establishes branding and exposes crucial navigation elements and functionality throughout the system.

* **Page Background**  
Supports and enhances branding and adds visual interest throughout the system.

* **Page Body**  
Displays a distinct backdrop for page content and provides "cookie crumb" navigation functionality for sub-pages.

* **Page Footer**  
Provides links to less-often used areas of the system as well as legal information and additional branding opportunities (logos, etc)

##Projects/Repositories
There are a few different projects that come together to complete the Boilerplate. Each project has it's own README, listed here for convenience:

* [**Javascript Core**](https://github.com/lightspeedvt/boilerplate)  
Boilerplate rendering and core functionality built with KnockoutJS

* [**Legacy Support**](https://github.com/lightspeedvt/boilerplate-legacy-support)  
Javascript and CSS for "legacy" pages within the system.

* [**"Grayline" CSS for Themer 2.0**](https://github.com/lightspeedvt/boilerplate-master)  
Sass framework for generating the Boilerplate's structural CSS.

* [**Sass "Themer"** (deprecated)](https://github.com/lightspeedvt/boilerplate-css)  
Sass framework for generating and applying themes in the LightSpeed VT application.

##Putting It All Together
Each of the projects above has it's own (similar) publishing method. In each case, you'll end up with static files that are published to Amazon S3/Cloudfront.  

After the files are published you'll need to get them into the system. You'll essentially just be updating paths to the newly published files.
