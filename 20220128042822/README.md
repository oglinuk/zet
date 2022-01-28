# Introduction to Webhooks

First let's understand what a webhook is and why it is useful. Let's say
for our example wanting to keep up-to-date with zettelkasten git
repositories on GitHub. Originally the idea was to *poll* or make a
request to check every so often. You can think of this as having to go
the the website and view the repository manually.

The oldest known mention of webhooks found so far is in a blog post, by a
person named Jeff Lindsay, titled "Web hooks to revolutionize the web".
Revolutionize they did.

"What is the equivalent of the pipe in the age of the web?" ~ Tim OReilly

Jeff goes on to describe webhooks as "essentially user defined callbacks
made with HTTP POST. To support web hooks, you allow the user to specify
a URL where your application will post to and on what events. Now your
application is pushing data out wherever your users want. It's pretty
much like re-routing `STDOUT` on the command line."

This person is ahead of their time, and shows it by going on to say, "The
idea here is to create new infrastructure. New opportunities. I've been
thinking a lot about the possibilities of a web hook enabled web, and it
makes me really excited. Because it's such open ended infrastructure, I'm
sure the possibilities extend well beyond what I can think of. Especially
when combined with our growing ecosystem of APIs and feeds.

Web hooks are easy to implement for application developers. You just
implement a UI or API to let the user specify target URLs, and then
you're just making a standard HTTP POST on events. This is a fairly
trivial operation in most environments, since you already do this to use
other web APIs."

I'm also really excited for the possibilities of webhooks!

One thing not covered is authentication, which from my research is
commonly OAuth2.

Stay tuned for a getting started!

Related:

* Web hooks to revolutionize the web
	<https://web.archive.org/web/20180630220036/http://progrium.com/blog/2007/05/03/web-hooks-to-revolutionize-the-web/>
* OAuth 2.0
	<https://oauth.net/>
* OAuth 2.0 Simplified
	<https://www.oauth.com/>

Tags:

	#webhooks #oauth #unix-philosophy
