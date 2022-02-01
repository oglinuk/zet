# Getting Started: GitHub REST API

One key and massive difference between a good and great platform is being
integrable (capable of being integrated). Fortunately GitHub is one of
the great ones who provide an extensive REST API suite. This zet is going
to cover how to get started using it.

The first thing stated in the documentation is very important in my opinion. "Most applications will use an existing wrapper library in the language of your choice, but it's important to familiarize yourself with
the underlying API HTTP methods first." I absolutely agree with the
mindset of learning the underlying structure of something before using
abstractions.

The first example is `curl https://api.github.com/zen`, which gave me the
following result.

```BASH
Anything added dilutes everything else.
```

The next example is a showcase of getting a user's GitHub profile. Here
is Linus Torvalds.

```BASH
HTTP/2 200
server: GitHub.com
date: Mon, 31 Jan 2022 03:10:17 GMT
content-type: application/json; charset=utf-8
cache-control: public, max-age=60, s-maxage=60
vary: Accept, Accept-Encoding, Accept, X-Requested-With
etag: W/"130168f9a0dbc3e48a314469d119c5239cdbc7d804a72a5fa46b1d269e9966de"
last-modified: Fri, 20 Aug 2021 23:59:05 GMT
x-github-media-type: github.v3; format=json
access-control-expose-headers: ETag, Link, Location, Retry-After, X-GitHub-OTP, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Used, X-RateLimit-Resource, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval, X-GitHub-Media-Type, X-GitHub-SSO, X-GitHub-Request-Id, Deprecation, Sunset
access-control-allow-origin: *
strict-transport-security: max-age=31536000; includeSubdomains; preload
x-frame-options: deny
x-content-type-options: nosniff
x-xss-protection: 0
referrer-policy: origin-when-cross-origin, strict-origin-when-cross-origin
content-security-policy: default-src 'none'
x-ratelimit-limit: 60
x-ratelimit-remaining: 52
x-ratelimit-reset: 1643599409
x-ratelimit-resource: core
x-ratelimit-used: 8
accept-ranges: bytes
content-length: 1327
x-github-request-id: D5CC:0853:18886B8:19F95A6:61F75319

{
  "login": "torvalds",
  "id": 1024025,
  "node_id": "MDQ6VXNlcjEwMjQwMjU=",
  "avatar_url": "https://avatars.githubusercontent.com/u/1024025?v=4",
  "gravatar_id": "",
  "url": "https://api.github.com/users/torvalds",
  "html_url": "https://github.com/torvalds",
  "followers_url": "https://api.github.com/users/torvalds/followers",
  "following_url": "https://api.github.com/users/torvalds/following{/other_user}",
  "gists_url": "https://api.github.com/users/torvalds/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/torvalds/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/torvalds/subscriptions",
  "organizations_url": "https://api.github.com/users/torvalds/orgs",
  "repos_url": "https://api.github.com/users/torvalds/repos",
  "events_url": "https://api.github.com/users/torvalds/events{/privacy}",
  "received_events_url": "https://api.github.com/users/torvalds/received_events",
  "type": "User",
  "site_admin": false,
  "name": "Linus Torvalds",
  "company": "Linux Foundation",
  "blog": "",
  "location": "Portland, OR",
  "email": null,
  "hireable": null,
  "bio": null,
  "twitter_username": null,
  "public_repos": 6,
  "public_gists": 0,
  "followers": 151529,
  "following": 0,
  "created_at": "2011-09-03T15:26:22Z",
  "updated_at": "2021-08-20T23:59:05Z"
}
```

The documentation states to take note of `x-ratelimit-limit` and
`x-ratelimit-remaining`, as unauthenticated clients can only make `60`
requests per hour. Also any header with a prefix of `x-` is a custom
header, like `x-github-media-type`.

In order to be able to do more requests per hour (and to access some
APIs), we need to authenticate. GitHub supports OAuth, but that is beyond
the scope of this zet and will be in a zet of it's own.

Repositories are the next topic covered, and the resource to get a
repositories details is as follows with the results.

`curl -i https://api.github.com/repos/rwxrob/zet`

```BASH
{
  "id": 363533137,
  "node_id": "MDEwOlJlcG9zaXRvcnkzNjM1MzMxMzc=",
  "name": "zet",
  "full_name": "rwxrob/zet",
  "private": false,

	...

  "visibility": "public",
  "forks": 13,
  "open_issues": 6,
  "watchers": 117,
  "default_branch": "main",
  "temp_clone_token": null,
  "network_count": 13,
  "subscribers_count": 24
}
```

To authenticate, we need to generate a *personal access token (PAT)*,
which can be done by going to `settings -> developer settings -> personal
access token`. For now we will just make authenticated requests by the
curl command with the `-u` option and passing the PAT as an environment
variable called `GHPAT`. The command to get the authenticated user's
information looks like and outputs the following.

This is a good time to talk a little about security and being mindful as
some of the scopes you can select allow for full access to things. An
example is `delete_repo`, which "grants access to delete adminable
repositories". Interesting side note (referenced below) is that "a
deleted repository can be restored within *90 days*, unless the
repository was part of a fork network that is not currently empty."


An important rule of thumb when creating the PAT (or dealing with
permissions in general) is *least privilege*, meaning *only give the
sufficient amount of permissions to operate.*

`curl -i -u oglinuk:$GHPAT https://api.github.com/user`

```BASH
HTTP/2 200
server: GitHub.com
date: Tue, 01 Feb 2022 01:02:58 GMT
content-type: application/json; charset=utf-8
content-length: 1313
cache-control: private, max-age=60, s-maxage=60
vary: Accept, Authorization, Cookie, X-GitHub-OTP
etag: "e2671e00a14f1becb9112c461cd2f04edd85ed0d1a76d35846be799ec8a39cfc"
last-modified: Sun, 02 Jan 2022 14:31:29 GMT
x-oauth-scopes: notifications, public_repo, repo:status
x-accepted-oauth-scopes:
github-authentication-token-expiration: 2022-02-08 01:00:09 UTC
x-github-media-type: github.v3; format=json
x-ratelimit-limit: 5000
x-ratelimit-remaining: 4999
x-ratelimit-reset: 1643680978
x-ratelimit-used: 1
x-ratelimit-resource: core
access-control-expose-headers: ETag, Link, Location, Retry-After, X-GitHub-OTP, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Used, X-RateLimit-Resource, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval, X-GitHub-Media-Type, X-GitHub-SSO, X-GitHub-Request-Id, Deprecation, Sunset
access-control-allow-origin: *
strict-transport-security: max-age=31536000; includeSubdomains; preload
x-frame-options: deny
x-content-type-options: nosniff
x-xss-protection: 0
referrer-policy: origin-when-cross-origin, strict-origin-when-cross-origin
content-security-policy: default-src 'none'
vary: Accept-Encoding, Accept, X-Requested-With
x-github-request-id: B972:1FC5:1DDB8CE:3D42B5B:61F886C2

{
  "login": "oglinuk",
  "id": 19831804,
  "node_id": "MDQ6VXNlcjE5ODMxODA0",
  "avatar_url": "https://avatars.githubusercontent.com/u/19831804?v=4",
  "gravatar_id": "",
  "url": "https://api.github.com/users/oglinuk",
  "html_url": "https://github.com/oglinuk",
  "followers_url": "https://api.github.com/users/oglinuk/followers",
  "following_url": "https://api.github.com/users/oglinuk/following{/other_user}",
  "gists_url": "https://api.github.com/users/oglinuk/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/oglinuk/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/oglinuk/subscriptions",
  "organizations_url": "https://api.github.com/users/oglinuk/orgs",
  "repos_url": "https://api.github.com/users/oglinuk/repos",
  "events_url": "https://api.github.com/users/oglinuk/events{/privacy}",
  "received_events_url": "https://api.github.com/users/oglinuk/received_events",
  "type": "User",
  "site_admin": false,
  "name": "Daniel",
  "company": null,
  "blog": "https://fourohfournotfound.com",
  "location": null,
  "email": null,
  "hireable": null,
  "bio": null,
  "twitter_username": null,
  "public_repos": 85,
  "public_gists": 0,
  "followers": 17,
  "following": 35,
  "created_at": "2016-06-09T05:47:28Z",
  "updated_at": "2022-01-02T14:31:29Z"
}
```

I am going to end the zet here as I want to shift to using Go and the
`google/go-github` library with OAuth.

Related:

* GitHub Docs: Getting started with the REST API
	<https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api>
* GitHub Docs: Scopes for OAuth Apps
	<https://docs.github.com/en/developers/apps/building-oauth-apps/scopes-for-oauth-apps>
* go-github
	<https://github.com/google/go-github>
* OAuth zet
	<TODO>

Tags:

	#curl #github-rest-api #least-privilege
