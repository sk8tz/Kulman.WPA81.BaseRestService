Base REST service for Universal Apps
============================

[![Build status](https://ci.appveyor.com/api/projects/status/tyk3ff6jamxondgh?svg=true)](https://ci.appveyor.com/project/igorkulman/kulman-wpa81-baserestservice)

Base class for a Windows Phone 8, Windows Phone 8.1 XAML and Windows 8.1 REST service implementation.

## Installation

	PM> Install-Package Kulman.WPA81.BaseRestService
	
## Usage

Create your service class and inherit from BaseRestService. The minimum you need to do to make it work is to override the GetBaseUrl() method to set the base url for all the requests. If you need and the GetRequestHeaders() to set the default request headers.

```csharp
public class MyDataService: BaseRestService
{
  protected override string GetBaseUrl()
  {
    return "my base url";
  }
  
  protected override Dictionary<string, string> GetRequestHeaders()
  {
    return new Dictionary<string, string>
    {
      {"Accept-Encoding", "gzip, deflate"},
      {"Accept", "application/json"},
    };
  }
}
```

Now you can use the following methods in your class

```csharp
Task<T> Get<T>(string url);
Task<T> Put<T>(string url, object request);
Task<T> Post<T>(string url, object request);
Task<T> Patch<T>(string url, object request);
Task Delete(string url);
```

Methods in your service may then look like this

```csharp
public Task<List<Account>> GetAccounts()
{
  return Get<List<Account>>("/accounts");
}
 
public Task<Account> UpdateAccount(Account account)
{
  return Patch<Account>("/accounts",account);
}
```

For more information, see my blog post [REST service base class for Windows Phone 8.1 XAML apps](http://blog.kulman.sk/rest-service-base-class-for-windows-phone-8-1-xaml-apps/).
