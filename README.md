# [momentjs](http://momentjs.com/ "momentjs") demo to showcase problem with localized names of months and days #

----------

All pages use same snippet of javascript bound to onclick of button:

```javascript
moment.locale('sk');
alert(moment("6-25-1995", "MM-DD-YYYY").format('dddd, MMMM Do YYYY, h:mm:ss'));
```

Which essentially does this :

- switch momentjs to Slovak locale
- alert parsed date of 25th of December 1995 to day, month day. year, hours:minutes:seconds

The problem lies in encoding of received .js file and what we can do about it.

# the project structure #

This demo consists of these HTML files :

- index.html - root page with links to each demo page,
- localconvertedfile.html - using local moment-with-locales-with-signature.js that has been converted to BOM,
- localforcedutf.html - using original moment-with-locales-orig.js but with property charset="utf-8" in script tag,
- localoriginalfile.html - using original moment-with-locales-orig.js - the very same was as momentjs has in their docs : [browser script tag link](http://momentjs.com/docs/#/use-it/browser/),
- remotefile.html - loading hosted momentjs file with Content-Type:application/javascript; charset=utf-8 headers.

and JS files :

- moment-with-locales-orig.js - original momentjs with locales downloaded from here [http://momentjs.com/downloads/moment-with-locales.js](http://momentjs.com/downloads/moment-with-locales.js) originally encoded as UTF8 without [BOM - byte order mark](http://en.wikipedia.org/wiki/Byte_order_mark).
- moment-with-locales-with-signature.js - the very same file but converted to UTF8 [BOM - byte order mark](http://en.wikipedia.org/wiki/Byte_order_mark).

# making it work #
So essentially there are 3 ways how can we make momentjs with locale versions of names work :

1. use response header Content-Type	set to :application/javascript; charset=utf-8 (usually this is just application/javascript),
2. convert momentjs to UTF8 with BOM,
3. use original file with content header just set to application/javascript but set charset="utf-8" in script tag.

# hosted files #
You can also play with this project hosted here : [loc.rostacik.net](loc.rostacik.net)

Dušan