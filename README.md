Demo App - Amplitude JS SDK with Google Tag Manager
================

GTM integration on web requires installing our [Javascript SDK](https://github.com/amplitude/amplitude-javascript#setup), and then setting up GTM to trigger SDK functions using custom HTML tags. This demo apps is a proof of concept, with just the 3 most important functionalities implemented (logging events, setting user Id, and setting user properties).

Refer to [Introducing the Amplitude Google Tag Manager (GTM) Template](https://amplitude.com/blog/google-tag-manager-template/) for more guidance.

**Note**:
- Make sure to put the Amplitude JS load snippet and initialize with your API key on every page before you load the Google Tag Manager script.
- It is always suggested to have a custom instance name to avoid naming collision.

### User-Defined Variables (all Data Layer Variables): ###
* eventProperties
* eventType
* userId
* userProperties

### Triggers: ###
* logEvent: Event equals 'logEvent'
* setUserId: Event equals 'setUserId'
* setUserProperties: Event equals 'setUserProperties'

### Tags: ###

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

### Note ###

A lot of the other functionality from the SDK hasn't been implemented (such as logging revenue, user property operations, etc), but this proof of concept demonstrates that GTM integration with Amplitude is possible, and events are being logged with the correct user Ids. Implementing the other functionalities would follow a similar pattern. You can customize your integration based on your setup, for example you can have tags triggered by clicks or page views, but the important thing is that you map it to the correct SDK function in the custom HTML.
