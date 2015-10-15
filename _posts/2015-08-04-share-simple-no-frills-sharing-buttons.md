---
layout: post
title: "'Share' – Simple, no-frills sharing buttons"
---

!['Share' - Simple, no-frills sharing buttons](/public/img/2015-08-04-share-simple-no-frills-sharing-buttons/cover.jpg)

I don't understand why every sharing plugin or widget I've come across needs to be so complicated, load a ton of JavaScript and/or just be downright ugly.

I decided to make my own super simple, no-frills sharing buttons.

The icons are SVGs, so that avoids having another couple round-trips to the server and has the added benefit of playing nice with retina or other hi-DPI displays since they're vectors. No server-side voodoo, all done in JavaScript. Since to me only Facebook, Twitter and (perhaps) Google+ are the only relevant social networks around, I've just limited it to the big three, but you can easily extend it to fit your requirements.

If you want to use this, just make sure to swap out your site's *postamble* (that's the bit at the end) of your site's `<title>` tag and substitute your Twitter username. You can also run it through a minifier to compress it further if you like.

<script src="https://gist.github.com/ianmuscat/46958b29ba38b9630b6f.js"></script>
 