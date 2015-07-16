# Portable RestSharp #

[![Join the chat at https://gitter.im/FubarDevelopment/restsharp.portable](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/FubarDevelopment/restsharp.portable?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This is some kind of a RestSharp port to PCL.

# [BSD 2-Clause License](LICENSE.md) #

# News #

Version 3.0.0 will come soon and it will contain **breaking changes** for the authenticators:

* The ```IRestRequest.Credentials``` property moved to ```IRestClient.Credentials```
* Credentials for authenticators are specified using the ```IRestClient.Credentials``` property
* New core library that contains all interfaces and other generic stuff
* New interface for proxies
* New interfaces that are an abstraction of the HttpClient and its request/response messages
* Uses now a RestSharp project compatible Method enumeration for HTTP requests and
  all constructors taking a HttpMethod are flagged as obsolete
* The API will change again soon!

# Changes #

## 3.0.0 alpha 4 ##

* Moved all interfaces and other generic stuff into a separate core library
  that doesn't have any dependencies
* New interfaces that are an abstraction of the HttpClient and its 
  request/response messages
* New interface for proxies
* Uses now a RestSharp project compatible Method enumeration for HTTP requests and
  all constructors taking a HttpMethod are flagged as obsolete
* The IAuthenticator, ISerializer, IEncoding, and IDeserializer interfaces were
  moved to the RestSharp.Portable namespace

## 3.0.0 alpha 3 ##

* Revamped authenticator interfaces
  * Provide a way to process the ```Www-Authenticate``` header
  * Make HTTP Basic/Digest authenticators work with ```Proxy-Authenticate``` header
  * Credentials property moved from ```IRestRequest``` to ```IRestClient```
  * The NTLM authenticator is not needed anymore, because the the credentials from 
    the ```IRestRequest``` are automatically used in the ```HttpClientHandler``` which handles
    the Basic/Digest/NTLM authentication automatically
  * All authenticators should query the credentials passed to the authenticator
  * New ```AuthenticationChallengeHandler``` which selects one of the registered
    authenticators in response to a ```Www-Authenticate``` or ```Proxy-Authenticate``` challenge.
* New Gitter OAuth 2.0 client

## 2.4.3 ##

* Bugfix for issue [#23](https://github.com/FubarDevelopment/restsharp.portable/issues/23).
  Thanks to [GeirGrusom](https://github.com/GeirGrusom)

## 2.4.2 ##

* Bugfix for issue [#25](https://github.com/FubarDevelopment/restsharp.portable/issues/25).
  We're using asynchronous locking now.

## 2.4.1 ##

* Bugfix for issue [#24](https://github.com/FubarDevelopment/restsharp.portable/issues/24)
  which should allow using both OAuth 1.0 and 2.0 in Android apps.

## 2.4.0 ##

* New ```Timeout``` property to fix issue [#13](https://github.com/FubarDevelopment/restsharp.portable/issues/13) with [CancellationTokenSource.CancelAfter](https://msdn.microsoft.com/de-de/library/hh194678%28v=vs.110%29.aspx)

## 2.3.2 ##

* Fixes concurrent requests on the same RestClient (fixes [#19](https://github.com/FubarDevelopment/restsharp.portable/issues/19), 
  bug introduced with [#11](https://github.com/FubarDevelopment/restsharp.portable/issues/11))

## 2.3.1 ##

* Fixes issue [#18](https://github.com/FubarDevelopment/restsharp.portable/issues/18)
  * All DateTime(Offset) HTTP header values are encoded as described in RFC 1123 after conversion to UTC/GMT
* All data is converted to a string using the en-US culture (might be a breaking change)

## 2.3.0 ##

* Fixes issue [#17](https://github.com/FubarDevelopment/restsharp.portable/issues/17)
  * New IsSuccess property for IRestResponse

## 2.2.0 ##

* Fixes issue [#15](https://github.com/FubarDevelopment/restsharp.portable/issues/15)
  * Add the ability to provide a custom timestamp provider
* Fixes issue [#16](https://github.com/FubarDevelopment/restsharp.portable/issues/16)
  * Remove superfluous "?" when using URL segment parameters in the query string

## 2.1.1 ##

* Fixed broken SL5 support (thanks to P2SH)

## 2.1.0 ##

* Fixes issue [#11](https://github.com/FubarDevelopment/restsharp.portable/issues/11)
  * IRestClient now derives from IDisposable
  * HttpClient is kept alive until the RestClient gets disposed
  * Default HTTP header parameters are set for the
    HttpClient
* Fixes issue [#12](https://github.com/FubarDevelopment/restsharp.portable/issues/12)
  * Workaround for the 32k limit of EscapeDataString
  * Custom class for URL encoding that's
    used as fall-back, when the user wants to use 
    EscapeDataString with a byte array (which isn't supported).
* Avoid rebuilding the Basic Authentication header for each request 

## 2.0.3 ##

* Fixed NuGet dependency for the OAuth 1.0 package
* Fixed some problems found by FxCop

## 2.0.2 ##

* Fixed NuGet package for Xamarin.iOS (upload using nuget instead of NPE)

## 2.0.1 ##

* Fixed Microsoft.Bcl and Microsoft.Bcl.Build dependencies
* Assemblies are now CLSCompliant (except PCL and SL5, which don't support this attribute)

## 2.0.0 ##

* Removed all deprecated methods
* Starting from this version, I'll use [Semantic Versioning 2.0.0](http://semver.org/)
* Optimizing NuGet dependencies for several platforms
* Clear Accept HTTP header parameter for the SL5 platform for GET requests ([Issue #9](https://github.com/FubarDevelopment/restsharp.portable/issues/9))
* Add Deflate encoding

## 1.9.1 ##

* OAuth2AuthorizationRequestHeaderAuthenticator should only check for Authorization
  header parameter
* Better handling of refresh tokens in the OAuth2AuthorizationRequestHeaderAuthenticator

## 1.9.0 ##

* Increased compatibility with the original RestSharp project
	* BuildUri instead of BuildUrl (deprecated)
	* Added AddJsonBody, AddXmlBody, AddQueryParameter, AddObject
* Graceful handling of duplicate parameters
  (might be a breaking change)
* Dispose HttpClient, HttpRequestMessage and the HttpResponseMessage

## 1.8.5 ##

* BuildUrl adds a "/" between a base URL and resource 
  if neither of them is empty and the "/" is missing
* Fix BOM for XmlDataContractSerializer
* Better support for OAuth2 refresh tokens by supporting
  a HTTP 401 by the OAuth2 authenticator (when a refresh 
  token was set)

## 1.8.4 ##

* Support for parameters in IRestClient.BaseUrl
* Signed OAuth1/OAuth2 assemblies
* Increased compatibility for empty IRestClient.BaseUrl

## 1.8.3 ##

* Workaround for NuGet pack bug

## 1.8.2 ##

* Encodings for parameters (get/post/url/query)

## 1.8.1 ##

* Async. authenticators
* New OAuth2 package

## 1.8.0 ##

* Cancellable requests
* New OAuth 1.0 package

# Supported platforms

* .NET Framework 4
* .NET for Windows Store apps
* .NET Native
* Windows Phone 8 and 8.1
* Silverlight 5
* Portable Class Libraries
* Xamarin Android
* Xamarin MonoTouch / iOS

# Small example

The following is an example to get the ticker from the bitstamp.net website.

## The result class
```csharp
public class TickerResult
{
	public decimal Last { get; set; }
	public decimal High { get; set; }
	public decimal Low { get; set; }
	public decimal Volume { get; set; }
	public decimal Bid { get; set; }
	public decimal Ask { get; set; }
}
```

We use the class with:

```csharp
using (var client = new RestClient(new Uri("https://www.bitstamp.net/api/")))
{
    var request = new RestRequest("ticker", HttpMethod.Get);
    var result = await client.Execute<TickerResult>(request);
}
```

# Community Support #

The support for community projects can be found in my [subreddit /r/FubarDev](http://www.reddit.com/r/FubarDev/).

# Professional Support #

You can get professional support here: [Fubar Development Junker](https://www.fubar-dev.de)
