---
layout: post
category : programming
tagline:
date: 2015-07-01 17:25:00 UTC 
tags : [aspnet5]
title: Upgrading an ASP.NET 5 MVC app from beta4 to beta5
---
{% include JB/setup %}

ASP.NET 5 Beta 5 is [out now](http://blogs.msdn.com/b/webdev/archive/2015/06/30/asp-net-5-beta5-now-available.aspx), so go get it.
The only thing that really broke for me was my custom configuration source setup.
	//beta4
	public Startup(IHostingEnvironment env)
    {
        // Setup configuration sources.
        Configuration = new Configuration()
                            .AddJsonFile("secret.json");
                            
    }

	//beta5
	public Startup(IHostingEnvironment env, IApplicationEnvironment appEnv)
	{
	// Setup configuration sources.
	Configuration = new Configuration(appEnv.ApplicationBasePath)
	.AddJsonFile("secret.json");
	}
	

I also use this for my integration tests. In this case you could do something like this:

    IConfiguration config = 
        new Configuration(Directory.GetCurrentDirectory())
        .AddJsonFile("secret.json");








