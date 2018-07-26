# Duct

Duct는 data 기반 아키텍쳐를 사용해 서버사이드 어플리케이션을 빌드하기위한 모듈형 프레임워크입니다.
이는 [Arachne](http://arachne-framework.org/) 의 범위와 비슷하고,
[Integrant](https://github.com/weavejester/integrant)를 기반으로 합니다.
Duct는 청사진 역할을 하는 변하지 않는 컨피그레이션의 구성에 기반해서 어플리케이션을 빌드합니다.
컨피그레이션 파일을 다루거나 쿼리를 통해 정교한 동작을 생성할 수 있습니다.

## 빠르게 시작하기

Lieningen으로 새로운 Duct 프로젝트 만들기:

```bash
lein new duct <your project name>
```

이렇게하면 간단한 Duct프로젝트가 생성됩니다.
profile을 붙여 기능을 확잘할 수도 있습니다.

* `+api`      API 미들웨어와 핸들러 추가
* `+ataraxy`  Ataraxy 라우터 추가
* `+cljs`     ClojureScript 모음과 Hot-loading 추가
* `+example`  예제 핸들러 추가
* `+heroku`   Heroku 배포를 위한 설정 추가
* `+postgres` PostgreSQL 의존성과 데이터베이스 컴포넌트 추가
* `+site`     site 미들웨어, favicon, webjars 등을 추가
* `+sqlite`   SQLite 의존성과 데이터베이스 컴포넌트 추가

예:

```bash
lein new duct foobar +site +example
```

모든 Leiningen 템플릿과 마찬가지로 Duct는 프로젝트와 동일한 이름의 새 디렉토리를 만듭니다.
프로젝트를 실행하고 빌드하는 방법은 프로젝트의 `README.md` 파일에 있습니다.

## Concepts

The structure of the application is defined by an Integrant configuration map.

The configuration map is transformed using modules.

In development, Duct uses Stuart Sierra's [Reloaded Workflow](http://thinkrelevance.com/blog/2013/06/04/clojure-workflow-reloaded).

In production, Duct follows the [Twelve-Factor App](http://12factor.net/) methodology.

Local state is preferred over global state.

Namespaces should group functions by purpose, rather than by layer.

## Overview

Duct is designed to produce a standalone application, logging to STDOUT, with external configuration supplied through environment variables. This approach is common for server-side applications, and works well in environments like [Heroku](https://www.heroku.com/) and [Docker](https://www.docker.com/).

The core of every Duct application is the configuration map, loaded from one or more [edn](https://github.com/edn-format/edn) resources, and interpreted by Integrant. Each key/value pair in the configuration corresponds to a multimethod that can **initiate** the configuration into a concrete implementation.

Before the configuration is initiated, however, it is first transformed. Some keys in the configuration are **modules**; these are pure functions used to update the configuration, adding in new keys and references.

Modules can introduce broad functionality that affects many parts of the application. Because they manipulate an immutable data structure, they are also both transparent and customizable. Anything a module adds can be queried, examined, and if necessary, overridden.

Any I/O to an external service should be accessed through a **boundary** protocol. This not only provides a clear dividing line between what's internal and what's external to the application, it also allows external services to be mocked or stubbed when testing.

## Documentation

* [Getting Started](https://github.com/weavejester/duct/wiki/Getting-Started)
* [Configuration](https://github.com/weavejester/duct/wiki/Configuration)

## Community

* [Google Group](https://groups.google.com/forum/#!forum/duct-clojure)

## File structure

Duct projects are structured as below. Files marked with a \* are kept out of version control.

```text
{{project}}
├── README.md
├── dev
│   ├── resources
│   │   ├── dev.edn
│   │   └── local.edn *
│   └── src
│       ├── dev.clj
│       ├── local.clj *
│       └── user.clj
├── profiles.clj *
├── project.clj
├── resources
│   └── {{project}}
│       ├── config.edn
│       └── public
├── src
│   └── {{project}}
│       ├── boundary
│       │   └── {{boundary}}.clj
│       ├── handler
│       │   └── {{handler}}.clj
│       └── main.clj
└── test
    └── {{project}}
        ├── boundary
        │   └── {{boundary}}_test.clj
        └── handler
            └── {{handler}}_test.clj
```

## License

Copyright © 2017 James Reeves

Distributed under the MIT license.

