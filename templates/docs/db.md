# Database

Buffalo uses [github.com/markbates/pop](https://github.com/markbates/pop) as its default database package for migrations, transactions, basic ORM functionality, and more.

<%= title("Getting Started") %>

Buffalo supports [PostgreSQL](https://www.postgresql.org/) (default), [MySQL](https://www.mysql.com/), and [SQLite3](https://sqlite.org/). When you generate a new Buffalo application you can change this with the `--db-type` flag. It is also possible to skip generation of all database components with the `--skip-pop` flag.

<%= title("database.yml", {name: "configuring"}) %>

When you first generate a Buffalo application a `database.yml` file will be generated for you, based on the type of database that was selected with the `--db-type` flag, with PostgreSQL being the default.

<%= code("yaml") { %>
development:
  dialect: postgres
  database: myapp_development
  user: postgres
  password: postgres
  host: 127.0.0.1
  pool: 5

test:
  url: {{envOr "TEST_DATABASE_URL" "postgres://postgres:postgres@127.0.0.1:5432/myapp_test"}}

production:
  url: {{envOr "DATABASE_URL" "postgres://postgres:postgres@127.0.0.1:5432/myapp_production"}}

<% } %>

**CONFIGURE THIS FILE!**

Make sure to set up the appropriate usernames, passwords, hosts, etc... that are appropriate for the environment that will be running the application. Buffalo **does not** create these databases, or start up any services for you.

In the generated `database.yml` file there is a template helper, `envOr`, that will attempt to find the the ENV var with that name, in this case `DATABASE_URL`, if that ENV does not exist, it will load the "default" string.

<%= title("Creating Databases") %>

Once the `database.yml` has been configured with the appropriate settings, and the database server is running, Buffalo can create all of the databases in the `database.yml` file with a simple command:

<%= code("text") { %>
$ buffalo db create -a
<% } %>

You can also create just one of the configured databases by using the `-e` flag and the name of the database:

<%= code("text") { %>
$ buffalo db create -e test
<% } %>

<%= title("Dropping Databases") %>

Buffalo can drop all of your databases, should you want to, with one command:

<%= code("text") { %>
$ buffalo db drop -a
<% } %>

You can also drop just one of the configured databases by using the `-e` flag and the name of the database:

<%= code("text") { %>
$ buffalo db drop -e test
<% } %>

