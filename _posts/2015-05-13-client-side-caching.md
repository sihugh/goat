---
layout: post
title: Client side caching and blob caching
categories: performance
description: Handover summary of caching strategies
---

## Key Bits ##
 - Cache on client side to take load off database, web front ends and networks.
 - The trade-off is that content may no longer be up to date.
 - Published pages are cached for 3 minutes in Browse and not cached in Auth
 - Content in “_layouts” is cached for 365 days
  -- Use this for content that will only change at release intervals (due to the fact that it is stored separately on each web front end so is a pain to update)
  -- Use the “Fingerprint.Tag()” method in the “Utility” project to ensure that the newest versions of layouts files are served.
  -- Easy to update source files in Dev!
  -- Not subject to Blob Cache
 - Some content in libraries is cached for 1 day
  -- Use this for content that you may need to update between releases (due to the fact that you only have to modify it in one place)
  -- A pain to update source files in Dev!
  -- Subject to Blob Cache

## Cache-Control Header ##

The Cache-Control header has two elements to it:
 - public / private
  -- This states whether or not proxy servers between the web server and the client should serve this content to different users requesting the same resource.
 - max-age=(a time in seconds)
  -- How long the end client should store and use this cached version for.


## Pages Behaviour ##

Pages contain most of the information (i.e. the text) that the rendered result displays.  When an author is modifying the page, they must see the “real” version of the content.  We are more able to cache content for consumers.

Pages are also the things that all the other assets are linked to (e.g. images, scripts, styles etc.).

 - Page caching is configured in “/_layouts/sitecachesettings.aspx”
 - Browse is set to cache for 3 minutes (I think we could be more aggressive with this).
 - Browse is set by default to “ServerAndPrivate” (results in the same as “private”).  We should set this to “public”!
 - Auth is set to not cache (which makes sense)

## Layouts Behaviour ##

 - The cache expiration is configured on the virtual directory in IIS and is set to 365 days.
  -- Uses the following header “Cache-Control: max-age=31536000”
  -- This is “public” by default which means that proxies can serve the same resource to multiple people without hitting the server
 - Content is stored solely on the file system
 - This may be over-ridden by using a “cache-busting” version tag when you link to assets (i.e. in the master page or page layouts)
  -- My version of this is in Fingerprint.cs in the Utility project or in this Gist (also linked below).

## Libraries Behaviour ##
 - Does not cache by default
 - “Blobcache” is enabled in web.config which caches gif, jpg, png, css, js and xml files which come from document libraries for 1 day (86400 seconds).
  -- Blob cache is a designated area on each front end where SharePoint may store content which matches the blob cache configuration.
  -- It saves round trips to the database, but requires “flushing” when we make updates.  (Use the site maintenance tool)
  -- We could configure it to cache more file types than we do… e.g. all image types
 - This can have some weird results ( http://www.sharepointnutsandbolts.com/2009/05/optimization-blob-caching-and-http-304s.html )

## Custom Pages ##

You can set your own headers, for which you’ll need to determine caching relevance.  For example, “alerts” are cached for 2 minutes client side.

## Useful Links ##

http://madskristensen.net/post/cache-busting-in-aspnet (Inspiration for my Fingerprint.cs below)

http://www.sharepointnutsandbolts.com/2009/06/my-checklist-for-optimizing-sharepoint.html

https://technet.microsoft.com/en-us/library/cc770229.aspx#BLOB (Blob cache settings)

{% gist 020c160a6e02318aa934 %}
