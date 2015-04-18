Processing.js and Intel XDK for Windows Phone

In a nutshell, Html Canvas + Apache Cordova backend responsive for Processing.js. Add in Web Audio API for sound handles. Load as a target for Windows 8 phone through Intel XDK.

** noted bug, initalizing and internet permission could use optimizing on some device to prevent white screen skip. 


Blank Intel XDK and Apache Cordova Project Template
===================================================

Copyright © 2012-2015, Intel Corporation. All rights reserved.

See [LICENSE.md](<LICENSE.md>) for license terms and conditions.

Use this template as a starting point for an Intel XDK or Apache Cordova hybrid
mobile app. One key file (`init-dev.js`) contains the initialization code needed
to detect the Cordova device ready, Intel XDK device ready and document ready
events in a way that allows you to run your app in a variety of environments.
This init code works:

-   with the the Intel XDK Emulate tab

-   in the Intel XDK App Preview application (Test tab)

-   in the Intel XDK App Preview Legacy application (Test tab)

-   in the App Preview Crosswalk container (Debug tab)

-   with the weinre debug script (Test tab)

-   in an app built using the Intel XDK legacy container (aka AppMobi container)

-   in an app built using the Apache Cordova container

When `init-dev.js` completes execution it issues a custom "`app.Ready`" event.
Use this event to start your application, rather than waiting on "device ready"
or "document ready" or "window load" or similar events. You should not have to
modify anything in `init-dev.js` to use this code. Also, `init-dev.js` has been
written so that it is not dependent on any external libraries or specific
webviews. It has been tested with the following webviews and browsers:

-   Android 2.3, 4.0-4.3, 4.4 and 5.0

-   iOS 6, 7 and 8

-   Windows 8 and 8.1 Phone

-   Windows 8 "Modern"

-   Crosswalk 7, 10 and 11

-   Chrome Desktop Browser thru version 40

-   Internet Explorer 10 and 11

Converting a Web App to a Cordova App
-------------------------------------

This blank project works well for converting an existing web app into a hybrid
app. One of the biggest issues encountered when porting a web app to a hybrid
app is resolving the init sequence of the web app with the init sequence
required of a hybrid HTML5 app. This gets especially difficult when large
third-party libraries are part of the app. Due to the additional burden of
initializing the underlying native code layer, developers sometimes have trouble
getting their code that runs in a desktop browser to initialize in an HTML5
hybrid webview. Frequently this is due to the significant difference in
resources between the desktop browser and the mobile webview (e.g., less memory,
lower performance and a reduced feature set).

When converting an existing web-based app into a Cordova app, try to trigger the
execution of your application off of the `app.Ready` event generated by the
included `init-dev.js` file in this template. It will fire after document ready
and the Cordova device ready events have triggered. This insures that your
Cordova APIs are usable and your DOM is ready. The time to get to this point can
vary widely, depending on the device and number and size of JavaScript libraries
that make up your application. It is not unusual to take 2-5 seconds (or longer
for very large apps) to reach the ready state.

Initializing Your Cordova App
-----------------------------

See the included `init-app.js` and `app.js` for an example of one way to start
an app using the custom "`app.Ready`" event described above. These files are
optional and can be discarded or rewritten to suit your needs. Also, there is
nothing particularly important about the `app.css` file, it contains a few
global CSS definitions that are commonly applied to older Android devices, but
certainly is not the "end all" for configuring the CSS in your hybrid HTML5
webview application.

There are many comments in the files in this template. Please read those
comments for details and further documentation. In particular, see the comments
in the `index.html` file for recommendations on where to load your third-party
libraries relative to your application code and the special hybrid libraries
(`intelxdk.js`, `cordova.js` and `xhr.js`).

There are also a large number of `console.log()` messages contained within
`init-dev.js`. They can be used to debug initialization problems and understand
how this init file works. It is highly recommended that you leave those
`console.log()` messages in your app, they will not unduly slow down or burden
your application. Set `dev.LOG = true` to enable the `console.log()` messages
embedded within the `init-dev.js` file.

Project File Information
------------------------

The `icon.png` and `screenshot.png` files are not required by your project. They
are included for use by the Intel XDK template/demo panel and have no use within
a real app. You can safely delete them from your project directory.

You can build a *Cordova web app* from this template that can be submitted to a
store using the "Cordova Hybrid Mobile App Platforms" build tiles (for
Crosswalk, Android, iOS and Windows). The `intelxdk.config.additions.xml` file
can be used to include options that control your *Cordova web app* builds. For
example, you can enable remote debug of an Android or Crosswalk Cordova app with
Chrome DevTools by adding the appropriate preferences to this file.

The Intel XDK does not include a mechanism to convert your "Standard HTML5 +
Cordova Project" into a "Standard HTML5 Project." The simplest way to convert a
Cordova project into a Standard project is to create a new "Standard" project
from the appropriate template and copy your files from this project into that
new project.

The `cordova.js` script is needed to provide your app with access to Cordova
APIs. To add Cordova APIs to your application you must add the corresponding
Cordova plugins. See the *Plugins* section on the **Projects** tab.

**IMPORTANT:** the `intelxdk.js` and `xhr.js` script files are not automatically
included in this template, as they have been in past versions. Those files are
only needed for apps built using the legacy AppMobi build containers on the
**Build** tab, which have been deprecated. We encourage you to use the Cordova
containers for all new applications. These script files can be added by hand, if
you require them, as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<script src="intelxdk.js" id="xdkJSintelxdk_"></script>
<script src="cordova.js" id="xdkJScordova_"></script>
<script src="xhr.js" id="xdkJSxhr_"></script>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The id tags are there to help future versions of the Intel XDK precisely
identify these special lines in your `index.html` file; your application does
not need to reference them.

The `xhr.js` file's purpose was to provide external domain access to your mobile
web app. In a Cordova web app this is controlled via the *Domain Access
Whitelist* in the *Build Settings* section of the **Projects** tab. For details
regarding how to specify your domain whitelist see this Cordova doc page:
<http://cordova.apache.org/docs/en/4.0.0/guide_appdev_whitelist_index.md.html#Whitelist%20Guide>

End Notes
---------

BTW: the "`dev`” prefix refers to "device" in this context, not "develop,"
because it grew out of a desire to build a more reliable and flexible "device
ready" detector for Cordova apps.

A "lite" version of this template is available here:
<https://github.com/gomobile/template-blank-cordova-project-lite>
