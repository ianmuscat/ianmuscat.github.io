---
layout: post
title: "Solving mixed content issues"
---

A while ago I was observing some HTTP requests fly through Google Chrome Dev Tools' "Network" tab, when I noticed an interesting HTTP header being sent by the browser for each request – `Upgrade-Insecure-Requests: 1`.

It turns out that Google Chrome 43 and newer sends this header automatically. The HTTP request header is closely related to the `Content-Security-Policy: upgrade-insecure-requests` HTTP response header.

The "Upgrade Insecure Requests" Content Security Policy is a [W3 specification](http://www.w3.org/TR/upgrade-insecure-requests){:target="_blank"} that can be used to instruct a browser to automatically upgrade any insecure HTTP requests to the secure HTTPS alternative before the browser does any fetching of resources – essentially it solves annoying [mixed-content](https://developer.mozilla.org/en/docs/Security/MixedContent){:target="_blank"} issues you face when a webpage is served over HTTPS. Even if a single image has a `src` attribute with referencing the HTTP protocol as opposed to the HTTPS protocol, you'll still get the dreaded mixed content warnings in the browser's address bar.

It turns out that the browser sends the `Upgrade-Insecure-Requests: 1` header to indicate to the server that it supports the "Upgrade Insecure Requests" Content Security Policy, and that it is actually preferred.

Ideally, Content Security Policies should be enabled via an HTTP response header which is served by the web server to the browser. However, in cases where this is not possible (as is the case with GitHub pages for instance), you can use the `<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">` tag in your HTML's `<head>` as an alternative.

While this header does help solve mixed content issues, it should not be treated as a silver bullet – you can not just set this header and forget about mixed content issues. For one thing, older browsers might ignore this header and you should still try your best to use [protocol-relative or HTTPS URLs](http://www.paulirish.com/2010/the-protocol-relative-url/){:target="_blank"} where you can.