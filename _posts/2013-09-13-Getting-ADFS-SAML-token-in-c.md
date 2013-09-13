---
layout: post
category : programming
tagline:
date: 2013-09-13 12:30:00 UTC 
tags : [adfs, c#]
title: Requesting a SAML token from ADFS in C#
---
{% include JB/setup %}

NOTE: The code for my ADFS experiments is available at [github](https://github.com/hoetz/ADFSTokenPlayground)


##The problem

I set out to integrate a new .net web api project (and the client application consuming it) with ADFS authentication. Since I wanted to understand
the nuts and bolts of ADFS tokens & using them with web apis, I chose not to use any "designer tools" in Visual Studio.
Here's what I'd like to achieve:

- client application authenticates for the first time with username/password
- use credentials to request security token from ADFS
- convert the token to JWT format for usage in HTTP headers

##Getting the token
Requesting the token is actually pretty easy once you use a little WCF magic (and know your ADFS endpoint).
Here is the code for my TokenProvider. Please note that I use the excellent "Thinktecture.IdentityModel" nuget package.

```C#
public class ADFSUsernameMixedTokenProvider
    {
        private readonly Uri ADFSUserNameMixedEndpoint;

        /// <summary>
        ///
        /// </summary>
        /// <param name="adfsUserNameMixedEndpoint">i.e. https://adfs.mycompany.com/adfs/services/trust/13/usernamemixed </param>
        public ADFSUsernameMixedTokenProvider(Uri adfsUserNameMixedEndpoint)
        {
            this.ADFSUserNameMixedEndpoint = adfsUserNameMixedEndpoint;
        }

        public GenericXmlSecurityToken RequestToken(string username, string password, string relyingPartyId)
        {
            var factory = new WSTrustChannelFactory(
                    new UserNameWSTrustBinding(SecurityMode.TransportWithMessageCredential),
                     new EndpointAddress(this.ADFSUserNameMixedEndpoint));

            factory.TrustVersion = TrustVersion.WSTrust13;

            factory.Credentials.UserName.UserName = username;
            factory.Credentials.UserName.Password = password;

            var rst = new RequestSecurityToken
            {
                RequestType = RequestTypes.Issue,
                AppliesTo = new EndpointReference(relyingPartyId),
                KeyType = KeyTypes.Bearer
            };
            IWSTrustChannelContract channel = factory.CreateChannel();
            GenericXmlSecurityToken genericToken = channel.Issue(rst) as GenericXmlSecurityToken;

            return genericToken;
        }
    }
```

In the next post I will explain how to convert this token to JWT format.
