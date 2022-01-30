# TODO: Standardize Webhooks

There is a reason there are standards for things like the C programming
language, Linux, CommonMark, and various other projects. Webhooks seems
to be one technology that has either not been widely adopted enough yet
to need a standard, or it just slipped through the cracks. Either way, to
avoid the joys of having 20+ different webhook implementations, I am
making a TODO to start an unofficial webhook standard that will hopefully
serve as a base for an officially supported one.

I came across two posts, the second mentions *RESTful Webhooks*, and
both are recommended reads referenced below. The latter also claims to be
dedicated to the development of the standards/guidelines around RESTful
webhooks, but it hasn't been updated in 12 years (at the time of writing
this) and I am unsure at this moment of it has been adopted or not.

GitHub webhooks are a prime example. They support the
`application/x-www-form-urlencoded` `Content-Type` header in addition to
`application/json`, which may or may not be implemented by others.

The oldest reference I've found (by Jeff Lindsay referenced below)
doesn't specify things like `Content-Type`, but I am interested to find
out cases where others are more useful.

Related:

* C programming language standard
	<http://open-std.org/JTC1/SC22/WG14/www/docs/n2310.pdf>
* Linux standard base
	<https://refspecs.linuxfoundation.org/lsb.shtml>
* CommonMark standard
	<https://spec.commonmark.org/current/>
* webhooks.org wiki frontpage
	<https://web.archive.org/web/20120413121142/http://wiki.webhooks.org/w/page/13385124/FrontPage>
* RESTful webhooks
	<https://web.archive.org/web/20120302000920/http://wiki.webhooks.org/w/page/13385128/RESTful%20WebHooks>
* GitHub creating webhooks
	<https://docs.github.com/en/developers/webhooks-and-events/webhooks/creating-webhooks#content-type>
* Introduction to Webhooks
	<https://github.com/oglinuk/zet/tree/master/20220128042822>

Tags:

	#standards #webhooks #c #linux #commonmark
