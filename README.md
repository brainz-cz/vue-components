# vue-components
A collection of Brainz-made Vue components


#### Lettering:
```
<lettering>{{string}}</lettering>
```
![](https://media.giphy.com/media/jKXAxtNZCajAU2eIml/giphy.gif)

#### RevealImage:
Reveal image using animation upon reaching viewport. Accepts {{treshold}} (offset) parameter. Default treshold is 0.
```
<reveal-image
    src="{{src}}"
    alt="{{alt}}"
    :threshold="{{threshold}}"
/>
```

![](https://media.giphy.com/media/oynxvWgScg0z9XQLmT/giphy.gif)

#### MailTo
Vue component for ```<a href="mailto:...">...</a>```
```
<mail-to to="general@cobaltindustries.com" />

<mail-to to="general@cobaltindustries.com">Contact us</mail-to>

<mail-to
    to="general@cobaltindustries.com"
    subject="subject content"
    body="body content"
    cc="example@example.com"
/>

<mail-to
    to="general@cobaltindustries.com"
    :cc="['example@example.com', 'example2@example.com']"
/>
```