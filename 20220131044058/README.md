# GitHub's REST API Example's Need Updating

Recently delving into webhooks has caused me to create a project
involving GitHub's REST API suite for learning. The example in GitHub's
official documentaton for creating a webhook and the results it produces
are as follows.

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/octocat/hello-world/hooks \
  -d '{"name":"name"}'
```

```BASH
{
  "message": "Not Found",
  "documentation_url": "https://docs.github.com/rest/reference/repos#create-a-repository-webhook"
}
```

This is not helpful at all considering that the documentation just above
it says for the `name` parameter to "Use `web` to create a webhook.
Default: `web`. This parameter only accepts the value `web`." It also
states "Each webhook should have a unique `config`.", which the example
does not contain.

One overall thing that I would like to also see is a better job of
describing the `required` and the `optional` parameters/properties. For
example, the `config` `url` property is specified as "**Required.**" in
the documentation for "Update a repository webhook", but not "Create a
repository webhook".

Below are all the examples I found going through all the REST API
documentation, which are identical to the above example for creating a
repository webhook. While some examples are proper, it is not helpful to
me as a developer (and someone learning) to see the same exact example
for multiple APIs.

> I did not try the JavaScript examples, but would also like to see
> examples from each official (and perhaps even third-party) library.

**Checks API: Update a check run**

```BASH
curl \
  -X PATCH \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/octocat/hello-world/check-runs/42 \
  -d '{"name":"name"}'
```

**Enterprise administration API: Create a self-hosted runner group for an enterprise**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/enterprises/ENTERPRISE/actions/runner-groups/42 \
  -d '{"name":"name"}'
```

**Enterprise administration API: Update a self-hosted runner group for an enterprise**

```BASH
curl \
  -X PATCH \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/enterprises/ENTERPRISE/actions/runner-groups/42 \
  -d '{"name":"name"}'
```

**Issues API: Create a label**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/octocat/hello-world/labels \
  -d '{"name":"name"}'
```

**Projects API: Create an organization project**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/orgs/ORG/projects \
  -d '{"name":"name"}'
```

**Projects API: Update a project**

```BASH
curl \
  -X PATCH \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/projects/42 \
  -d '{"name":"name"}'
```	

**Projects API: Create a repository project**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/octocat/hello-world/projects \
  -d '{"name":"name"}'
```

**Projects API: Create a user project**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/user/projects \
  -d '{"name":"name"}'
```

**Projects API: Update an existing project column**

```BASH
curl \
  -X PATCH \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/projects/columns/42 \
  -d '{"name":"name"}'
```

**Projects API: Create a project column**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/projects/42/columns \
  -d '{"name":"name"}'
```

**Releases API: Update a release asset**

```BASH
curl \
  -X PATCH \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/octocat/hello-world/releases/assets/42 \
  -d '{"name":"name"}'
```

**Repositories API: Create an organization repository**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/orgs/ORG/repos \
  -d '{"name":"name"}'
```

**Repositories API: Update a repository**

```BASH
curl \
  -X PATCH \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/octocat/hello-world \
  -d '{"name":"name"}'
```

**Repositories API: Create a repository using a template**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/TEMPLATE_OWNER/TEMPLATE_REPO/generate \
  -d '{"name":"name"}'
```

**Repositories API: Create a repository for the authenticated user**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/user/repos \
  -d '{"name":"name"}'
```

**Teams API: Create a team**

```BASH
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/orgs/ORG/teams \
  -d '{"name":"name"}'
```

**Teams API: Update a team**

```BASH
curl \
  -X PATCH \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/orgs/ORG/teams/TEAM_SLUG \
  -d '{"name":"name"}'
```

**Users API: Update the authenticated user**

```BASH
curl \
  -X PATCH \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/user \
  -d '{"name":"name"}'
```

Related:

* Create a repository webhook REST API
	<https://docs.github.com/en/rest/reference/webhooks#create-a-repository-webhook--code-samples>
* REST API libraries
	<https://docs.github.com/en/rest/overview/libraries>
* Update a repository REST API
	<https://docs.github.com/en/rest/reference/webhooks#update-a-repository-webhook--parameters>
* Create a self-hosted runner group for an enterprise
	<https://docs.github.com/en/rest/reference/enterprise-admin#create-a-self-hosted-runner-group-for-an-enterprise--code-samples>
* Update a self-hosted runner group for an enterprise
	<https://docs.github.com/en/rest/reference/enterprise-admin#update-a-self-hosted-runner-group-for-an-enterprise--code-samples>
* Create a label
	<https://docs.github.com/en/rest/reference/issues#create-a-label--code-samples>
* Create an organization project
	<https://docs.github.com/en/rest/reference/projects#create-an-organization-project--code-samples>
* Update a project
	<https://docs.github.com/en/rest/reference/projects#update-a-project--code-samples>
* Create a repository project
	<https://docs.github.com/en/rest/reference/projects#create-a-repository-project--code-samples>
* Create a user project
	<https://docs.github.com/en/rest/reference/projects#create-a-user-project--code-samples>
* Update an existing project column
	<https://docs.github.com/en/rest/reference/projects#update-an-existing-project-column--code-samples>
* Create a project column
	<https://docs.github.com/en/rest/reference/projects#create-a-project-column--code-samples>
* Update a release asset
	<https://docs.github.com/en/rest/reference/releases#update-a-release-asset--code-samples>
* Create an organization repository
	<https://docs.github.com/en/rest/reference/repos#create-an-organization-repository--code-samples>
* Update a repository
	<https://docs.github.com/en/rest/reference/repos#update-a-repository--code-samples>
* Create a repository using a template
	<https://docs.github.com/en/rest/reference/repos#create-a-repository-using-a-template--code-samples>
* Create a repository for the authenticated user
	<https://docs.github.com/en/rest/reference/repos#create-a-repository-for-the-authenticated-user--code-samples>
* Create a team
	<https://docs.github.com/en/rest/reference/teams#create-a-team--code-samples>
* Update a team
	<https://docs.github.com/en/rest/reference/teams#update-a-team--code-samples>
* Update the authenticated user
	<https://docs.github.com/en/rest/reference/users#update-the-authenticated-user--code-samples>

Tags:

	#needs-updating #github #rest #curl
