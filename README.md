scriptcs
========

# Why should you care?
Write .net apps with a text editor, nuget and the power of Rosyln!

More on why I developed this [here] (http://codebetter.com/glennblock/2013/02/28/scriptcs-living-on-the-edge-in-c-without-a-project-on-the-wings-of-roslyn-and-nuget/)

# Pre-reqs

* Install the [nuget cmdline bootstrapper] (http://nuget.codeplex.com/releases/view/58939)
* Build the project and put scriptcs.exe in your path.

# Quick start
* Open a cmd prompt as admin
* Create a directory "c:\scriptcs_hello" and change to it.
* run "nuget install Microsoft.AspNet.WebApi.SelfHost"
* create a server.csx with your favorite editor. Paste the text below into the file and save.

```csharp
using System;
using System.IO;
using System.Web.Http;
using System.Web.Http.SelfHost;

var address = "http://localhost:8080";
var conf = new HttpSelfHostConfiguration(new Uri(address));
conf.Routes.MapHttpRoute(name: "DefaultApi",
   routeTemplate: "api/{controller}/{id}",
   defaults: new { id = RouteParameter.Optional }
);

var server = new HttpSelfHostServer(conf);
server.OpenAsync().Wait();
Console.WriteLine("Listening...");
Console.ReadKey();
```
* run "scriptcs server.csx"

This will launch a web api host.

# How it works
scriptcs relies on Rosyln for loading loose C# script files. It will automatically discover nuget packages local to the app and load the binaries.

# What's next
* Adding support for pluggable recipe "packs" for different frameworks.

# License 
Apache 2

# Credits
* Special thanks to @filip_woj for being the inspiration behind this with his Roslyn Web API posts.
* Thanks to the Roslyn team who helped point me in the right direction.
