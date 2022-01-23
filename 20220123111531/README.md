# Enterprise Golang: REST Interface

When dealing with enterprise-level software, you have to be mindful of
the system(s) that you deal with. It is easy to write code that becomes
technical debt, or a hinderance to progress. For example, if you're build
a website, you want to be able to handle 1000s if not 10000s or 100000s
of concurrent web requests. It is very easy to write software that has
pitfalls due to various reasons, and one most common is dependencies.

This is the first of various "Enterprise Golang" projects to showcase
what I consider to be enterprise-level (Golang specific) software. The
implemention in this case is a REST interface and a minimal web UI. The
scenario for the project is a digital library.

The current state has the following dependencies.

```
github.com/go-chi/chi/v5 v5.0.7 (for the router)
github.com/go-chi/cors v1.2.0 (for CORS)
github.com/mattn/go-sqlite3 v1.14.8 (for the database)
github.com/stretchr/testify v1.7.0 (for testing)
gopkg.in/yaml.v3 v3.0.0-20210107192922-496545a6307b (for configuration)

github.com/davecgh/go-spew v1.1.0 // indirect
github.com/pmezard/go-difflib v1.0.0 // indirect
```

Containerization/virtualization of some form is a must for
enterprise-level, and the project uses Docker.

Since the project uses Docker containers and there are two containers
involved, we need container orchestration. There are two options
available, using the `init` shell script, or Docker Compose.

The interface currently supports five CRUD opertions: `create`,
`retrieve`, `retrieve all`, `update`, and `delete`.

With the first code review documented, it is time for a coding sprint.

Related:

* restful-go
	<https://github.com/oglinuk/restful-go>
* restful-go first code review
	<https://github.com/oglinuk/restful-go/tree/master/docs/code-reviews/1642914462>
* Representational State Transfer (REST)
	<https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm>
* Chi Router
	<https://github.com/go-chi/chi>
* Chi CORS
	<https://github.com/go-chi/cors>
* Go SQLite3
	<https://github.com/mattn/go-sqlite3>
* Testify
	<https://github.com/stretchr/testify>
* Docker
	<https://www.docker.com/>
* Docker Compose
	<https://docs.docker.com/compose/>

Tags:

	#enterprise #golang #rest #chi #testify #shell #docker #docker-compose #code-review
