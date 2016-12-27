_[Demo and API docs](http://captaincodeman.github.io/auth-ajax/)_

## \<auth-ajax\>

[`<iron-ajax>`](https://beta.webcomponents.org/element/PolymerElements/iron-ajax)
with added auth header handling, token management and some convenient JWT role checks.

The aim is to allow your app to authenticate users using whatever system you want
([firebase auth](https://firebase.google.com/docs/auth/) works great!) and then have
an easy way to hook into using the auth tokens (which really should be [JWT](https://jwt.io/))
if / when accessing your own API and also to adapt the UI based on user roles.

### Why do I need this?

There are lots of examples that show how to add an auth bearer token to an `<iron-ajax>`
request, so it's easy ... right? The problem is that many examples just stick to the simple
"happy-path scenario" where the auth token is alwas valid and never expires.

But if your auth bearer tokens never expire then you have a problem! Best practice mandates
that they do, otherwise access can never be revoked (for whoever gets hold of the access token)
unless you add some server-side checks ... which means you are no longer using bearer
tokens, just a regular session key, which can seriously impact backend scalability.

OK, so you need to use both an access token AND a refresh token. Now the challenge becomes
how to handle updating the token when required and making any AJAX requests wait until it
has completed. The examples don't usually show that part.

Which is why this element might be useful ...

It adds a promise to the token refresh mechanism which the `<iron-ajax>` requests can wait
on. It also triggers the token refresh when the access token is within a configurable 
threshold of its expiry time (because there's no sense sending a request that will probably
fail if clocks are a few minutes askew).

### What else does it do?

The other great benefit of using a [JSON Web Token](https://jwt.io/) (JWT) as the auth bearer 
token is that the client can also use it. Information such as user name or avatar image can be 
embedded and used in the UI to show the user status. If roles are available, these can be used 
to show or hide certain features or options or otherwise customize the UI based on user permissions.

So, there is also an `<auth-role>` element which acts as an auth-based dom-if template which
can display content based on auth status or whether the auth token contains certain roles.

## What about Firebase auth?

Firebase auth is quick and easy (and definitely recommended) and you don't need this element
if you are only using the Firebase hosted services (e.g. the realtime database). But if you 
want to integrate Firebase auth with an existing API then you may still find it helpful.

If your API is already expecting an auth token then chances are you can't just send the
firebase-issued token to it. Instead, you can authenticate using firebase but then create a
custom token which can contain any additional claims / roles your server needs. You'll also
be able to take advantage of the `<auth-role>` element to customize the UI based on the 
role permissions.

### Demo

I have created a separate [Go library for Custom Firebase Auth](https://github.com/CaptainCodeman/go-firebase)
which shows how to issue custom tokens on the serve and a [Demo](http://www.captaincodeman.com/auth-ajax/components/auth-ajax/demo/)
which uses Firebase auth + Google signin with custom token issuing to show how roles can be
added to a firebase token for use on both the server and client.