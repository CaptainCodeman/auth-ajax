_[Demo and API docs](http://captaincodeman.github.io/auth-ajax/)_

## \<auth-ajax\>

[`<iron-ajax>`](https://beta.webcomponents.org/element/PolymerElements/iron-ajax)
with added auth header handling, token management and some convenient JWT role checks.

The aim is to allow your app to authenticate users using whatever system you want
([firebase auth](https://firebase.google.com/docs/auth/) works great!) and then have
an easy way to hook into using the auth tokens (which really should be [JWT](https://jwt.io/))
if / when accessing your own API and also to adapt the UI based on user roles.

## Custom Tokens

Adding the firebase auth token to your own API requests is relatively simple. But
if you want to add your own custom roles you need to issue your own custom token.

Reasons why you would want this include using the auth token as a true Bearer token
so that no session or database lookups are required (i.e. just check the token roles
to authorize the request) and also to be able to adapt the UI based on permissions.

I have created a separate [Go library for Custom Firebase Auth](https://github.com/CaptainCodeman/go-firebase).

This is used in the demo with `operator` role automatically assigned when you sign in.

## Demo

Try the [Demo](http://www.captaincodeman.com/auth-ajax/components/auth-ajax/demo/)