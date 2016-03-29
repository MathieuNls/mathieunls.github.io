---
layout: post
title: Report your client-side errors to Slack.
tags:
- javascript
- slack
- php
- toolwatch
description: Report your js errors to Slack.
---

Errors are inevitable in web-development or development at large.
The first step to fix them is, well, to know about them.
By looking through your server logs or using server monitoring, you'll be able to see server side errors.
But then, what about client side errors, a.k.a, javascript errors?

<!--more-->

At toolwatch, our visitors use a wide-range of browser.
Here's a browser list as reported by Google analytics.

| Browser                  | %       |
|--------------------------|---------|
| Chrome                   | 44,73 % |
| Safari                   | 32,66 % |
| Firefox                  | 8,18 %  |
| Safari (in-app)          | 8,15 %  |
| Internet Explorer        | 2,96 %  |
| Edge                     | 0,96 %  |
| Android Browser          | 0,63 %  |
| Mozilla Compatible Agent | 0,63 %  |
| Opera                    | 0,56 %  |
| UC Browser               | 0,16 %  |
| BlackBerry               | 0,10 %  |
| Coc Coc                  | 0,07 %  |
| Maxthon                  | 0,05 %  |
| Nichrome                 | 0,02 %  |
| Amazon Silk              | 0,01 %  |

Sure, the top four/five are well-known and we do test that everything is awesome on these.
However, testing everything on each and every browser isn't only impractical, it's near impossible.
You could use some third party services such as [Browser shot](http://browsershots.org/) and [BrowserStack](https://www.browserstack.com/) or... use a quick *and dirty?* approach where client side errors get reported to wherever you want.
Here's what we use for reporting js errors in Slack with a php backend.

A simple js script, to include on every page, that posts an `error` variable composed of the file, line, user agent and platform that triggered the error:

{% highlight js %}
<script type="text/javascript">
  window.onerror = function(message, file, line) {
    $.post( "https://"+window.location.hostname+ "/someBackendUrl", { error:  file + "(" + line + "): "
      + message + " ["+navigator.userAgent+","+navigator.platform+"]" })
    .done(function( data ) {
      console.log("logged");
    });
  }
</script>
{% endhighlight %}

Then, on the backend side, a php script the received error to slack:


{% highlight php %}
//Concat the error with the HTTP_HOST, so we know if the error was triggered in stage or prod env.
$data = json_encode(["text"=>$_SERVER['HTTP_HOST']."\r\n".$error]);

//Get environment variable for the slack API key
$ch = curl_init(getenv("SLACK_EXCEPTION"));
//curl magick
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'Content-Length: '.strlen($data))
);
$result = curl_exec($ch);
{% endhighlight %}

Which produces the following in Slack:

<img src="/images/slack-error.png" alt="A slack message received after a client side error">

And, that's it, ~25 lines of code and you won't be able to say you didn't know anymore!
