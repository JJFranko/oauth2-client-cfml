# Standalone CFML oAuth 2 Component

A ColdFusion CFC to manage authentication using the OAuth2 protocol.

```This is a modified version of Matt McGifford's oAuth lib from``` [OAuth2 CFC](https://github.com/coldfumonkeh/oauth2/downloads)

A standalone oAuth2 component that should be included in other projects. 

* There are no provider libraries in this repo. 
* The oAuth config for each service is inside that library.

------

The core component, `oauth2.cfc`, can be used as a standalone OAuth2 tool for most providers. That's exactly what this repo is for.

Instantiate the component and pass in the required properties like so:

```
var oOauth2 = new oauth2(
	client_id           = '1234567890',
	client_secret       = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX',
	authEndpoint        = 'http://authprovider.fake/authorize',
	accessTokenEndpoint = 'http://authprovider.fake/token',
	redirect_uri        = 'http://redirect.fake'
);
```

Build the URL that you can then use to redirect the user to the provider for authorization:

```
var strURL = oOauth2.buildRedirectToAuthURL()
```

On your redirect page, once you have received your `code` value from the provider, you can then request the access token like so:

```
var sData = oOauth2.makeAccessTokenRequest( code = url.code );
```

## Providers

The provider components extend the core component to help lighten the load. They simply help to provide correct OAuth2 access to the provider in question as some have different requirements for parameters to send through.

Instantiation for the provider components is the same as the core, although you don't have to send through the `authEndpoint` and `accessTokenEndpoint` values as they are included in the provider components for you.

### Adding to the providers

You can easily create your own additional providers. If you do, please make a pull request to add them back into the Matts' repository for others to benefit,we've included providers into our other libraries for those providers.

To do so, take a look at one of the existing provider components. These extend the core and will always need their own `init`, `buildRedirectToAuthURL` and `makeAccessTokenRequest` methods to make sure the correct required values are sent through to the providers API.

#### Provider Instanciation

```
var oLinkedIn = new providers.linkedIn(
	client_id           = '1234567890',
	client_secret       = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX',
	redirect_uri        = 'http://redirect.fake'
);
```

Testing
----------------
The component has been tested on Adobe ColdFusion 9 and 10 and Lucee 4.5 and 5.2


Download
----------------

### 1.0 - 4 Aug 2018

Separated all providers out of the original library so this repo can be included as a remote repo in projects without pollution.
- Forked core component
- Forked testbox tests from original repo


Matt's versions:
----------------

### 1.1.0 - July 26, 2017

- Updated core oauth2 component
  - streamlined functions
  - removed unnecessary meta data
  - revised `makeAccessTokenRequest` in light of new provider capabilities (sending through custom formfields)

### 1.0.0 - June 03, 2012

- Commit: Initial Release


MIT License

Copyright (c) 2012 Matt Gifford (Monkeh Works Ltd)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

