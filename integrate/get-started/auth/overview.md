---
title: Authorization Basics | Visual Studio Team Services REST APIs
description: Use basic authentication to get started with the REST APIs for Visual Studio Team Services.
ms.assetid: 255E1E2B-9CB2-4FC3-8495-12DB4149A449
ms.prod: vs-devops-alm
ms.technology: vs-devops-integrate
ms.manager: douge
ms.author: elbatk
ms.date: 08/04/2016
---

# Basic authentication for the REST APIs

These APIs support [OAuth](./oauth.md) for authorization and you should plan to use that. With Oauth your users 
don't have to provide their Visual Studio Team Services credentials to use when the APIs are called.
To get started on your app, though, you can authenticate using personal access tokens.

[!INCLUDE [personal-access-tokens-procedure](../../../docs/git/_shared/personal-access-tokens.md)]

Here's a sample that gets a list of builds using curl.
<br/>
```
curl -u username[:{personalaccesstoken}] https://{account}.visualstudio.com/DefaultCollection/_apis/build/builds
```
<br/>
If you wish to provide the personal access token through an HTTP header, you must first convert it to a Base64 string (the following example shows how to convert to Base64 using C#).  The resulting string can then be provided as an HTTP header in the format:
<br/>
```
Authorization: Basic BASE64PATSTRING
``` 
<br/>
Here it is in C# using the [HttpClient class](http://msdn.microsoft.com/en-us/library/system.net.http.httpclient.aspx).
<br/>
```cs
public static async void GetBuilds()
{
	try
	{
		var personalaccesstoken = "PATFROMWEB";

		using (HttpClient client = new HttpClient())
		{
			client.DefaultRequestHeaders.Accept.Add(
				new System.Net.Http.Headers.MediaTypeWithQualityHeaderValue("application/json"));

			client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic",
				Convert.ToBase64String(
					System.Text.ASCIIEncoding.ASCII.GetBytes(
						string.Format("{0}:{1}", "", personalaccesstoken))));

			using (HttpResponseMessage response = client.GetAsync(
						"https://{account}.visualstudio.com/DefaultCollection/_apis/build/builds").Result)
			{
				response.EnsureSuccessStatusCode();
				string responseBody = await response.Content.ReadAsStringAsync();
				Console.WriteLine(responseBody);
			}
		}
	}
	catch (Exception ex)
	{
		Console.WriteLine(ex.ToString());
	}
}
```
<br/>
When your code is working, it's a good time to switch from basic auth to [OAuth](./oauth.md).

## Q&A

<!-- BEGINSECTION class="md-qanda" -->

#### Q: Can I use basic auth with all of the Visual Studio Team Services REST APIs?

A: No. You can use basic auth with most of them, but [accounts](../../api/shared/accounts.md) and [profiles](../../api/shared/profiles.md) only support [OAuth](./oauth.md).

<!-- ENDSECTION --> 
