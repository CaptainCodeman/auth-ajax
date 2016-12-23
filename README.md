# \<auth-ajax\>

[`<iron-ajax>`](https://beta.webcomponents.org/element/PolymerElements/iron-ajax)
with added auth header handling, token management and some convenient JWT role checks.

The aim is to allow your app to authenticate users using whatever system you want
([firebase auth](https://firebase.google.com/docs/auth/) works great!) and then have
an easy way to hook into using the auth tokens (which really should be [JWT](https://jwt.io/))
if / when accessing your own API and also to adapt the UI based on user roles.
