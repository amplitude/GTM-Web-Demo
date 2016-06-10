Demo App - Amplitude JS SDK with Google Tag Manager
================

GTM integration on web requires installing our [Javascript SDK](https://github.com/amplitude/amplitude-javascript#setup), and then setting up GTM to trigger SDK functions using custom HTML tags. This demo apps is a proof of concept, with just the 3 most important functionalities implemented (logging events, setting user Id, and setting user properties). Here is our GTM container setup:

###User-Defined Variables (all Data Layer Variables):###
* eventProperties
* eventType
* userId
* userProperties

###Triggers:###
* logEvent: Event equals 'logEvent'
* setUserId: Event equals 'setUserId'
* setUserProperties: Event equals 'setUserProperties'

###Tags:###

logEvent
* type: Custom HTML Tag
* HTML: `<script>amplitude.getInstance().logEvent('{{eventType}}', {{eventProperties}});</script>`
* Fire on trigger: Event equals 'logEvent'

setUserId
* type: Custom HTML Tag
* HTML: `<script>amplitude.getInstance().setUserId('{{userId}}');</script>`
* Fire on trigger: Event equals 'setUserId'

setUserProperties
* type: Custom HTML Tag
* HTML: `<script>amplitude.getInstance().setUserProperties({{userProperties}});</script>`
* Fire on trigger: Event equals 'setUserProperties'

The idea is that when you want to log an event, you push a "logEvent" event to the data layer with the variables for eventType and eventProperties -> activates the logEvent trigger -> activates the logEvent tag -> calls our SDK's logEvent using the `script` tags.

### To run this locally ###

1. Run `npm install`
2. Run `node server.js`
3. In browser, navigate to `http://localhost:9000/amplitudejs-gtm.html`

###
GTM Web Demo: https://github.com/amplitude/GTM-Web-Demo
* Setting up GTM:
* Setting up the handlers: https://github.com/amplitude/GTM-iOS-Demo/blob/master/m2048/M2AppDelegate.m#L20-L34
* Example of setting userId and userProperties: https://github.com/amplitude/GTM-iOS-Demo/blob/master/m2048/Controller/M2ViewController.m#L40-L43
* Example of logging an event: https://github.com/amplitude/GTM-iOS-Demo/blob/master/m2048/State/M2GameManager.m#L208-L209

A lot of the other functionality from the SDK hasn't been implemented (such as logging revenue, user property operations, etc), but this proof of concept demonstrates that GTM integration with Amplitude is possible, and events are being logged with the correct user Ids. Implementing the other functionalities would follow a similar pattern.