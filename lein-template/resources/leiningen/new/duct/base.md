# README

FIXME: description

## Developing

### Setup

When you first clone this repository, run:

```bash
lein duct setup
```

This will create files for local configuration, and prep your system for the project.

Next connect the repository to the [Heroku](https://www.heroku.com/{{/heroku?}}) app:

```bash
heroku git:remote -a FIXME
```

### Environment

To begin developing, start with a REPL.

```bash
lein repl
```

Then load the development environment.

```text
user=> (dev)
:loaded
```

Run `go` to prep and initiate the system.

```text
dev=> (go)
:duct.server.http.jetty/starting-server {:port 3000}
:initiated
```

By default this creates a web server at [http://localhost:3000](http://localhost:3000).

When you make changes to your source files, use `reset` to reload any modified files and reset the server. Changes to CSS or ClojureScript files will be hot-loaded into the browser.

```text
dev=> (reset)
:reloading (...)
:resumed
```

If you want to access a ClojureScript REPL, make sure that the site is loaded in a browser and run:

```text
dev=> (cljs-repl)
Waiting for browser connection... Connected.
To quit, type: :cljs/quit
nil
cljs.user=>
```

### Testing

Testing is fastest through the REPL, as you avoid environment startup time.

```text
dev=> (test)
...
```

But you can also run tests through Leiningen.

```bash
lein test
```

## Legal

Copyright ©  FIXME

