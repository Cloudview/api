# Authentication

The Cloudview API uses [OAuth 1.0](http://oauth.net/core/1.0/) as it's authentication protocol.

All applications that utilize the Cloudview API must be registered and have an associated OAuth Consumer Key and Secret

## Endpoints

* Temporary Request Token - `https://www.jabbakam.com/oauth/request_token`
* Authorize - `https://www.jabbakam.com/oauth/authorize`
* Permanent Access Token - `https://www.jabbakam.com/oauth/access_token`
* API Root - `https://api.jabbakam.com`

## User Authentication

All API requests must be signed using the OAuth 1.0 signature method. In order to do this, the user must have the OAuth Access Tokens. 

In order to get the Access Token, there are several steps that need to be completed:

1. Get a **Temporary Request Token**  
2. Using the temporary Access request Token, the user must **Authorize** access for the application
3. Once Authorization has been granted, a **Permanent Access Token** must be requested

Now the user has the Access Token, they can request API resources.

### 1. Obtain a Temporary Request Token

See [section 6.1](http://oauth.net/core/1.0/#auth_step1) of the OAuth Protocol.

### 2. Authorize the Application

See [section 6.2](http://oauth.net/core/1.0/#auth_step2) of the OAuth Protocol.

### 3. Obtain the Permanent Access Token

See [section 6.3](http://oauth.net/core/1.0/#auth_step3) of the OAuth Protocol.

## Requesting API Resources

See [section 7](http://oauth.net/core/1.0/#anchor13) of the OAuth Protocol.

### Signature

See [section 9](http://oauth.net/core/1.0/#signing_process) of the OAuth Protocol.


## References

* [OAuth Core 1.0](http://oauth.net/core/1.0/)
* [RFC 5849](http://tools.ietf.org/html/rfc5849)

******************

[Back to main page](../README.md)
