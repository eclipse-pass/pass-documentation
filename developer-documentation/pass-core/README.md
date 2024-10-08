# Pass Core

## Summary

This module is a Spring Boot and Elide application which provides HTTP APIs.

PASS has a single page JavaScript user interface based on Ember. The UI interacts with pass-core through HTTP APIs.

The HTTP APIs are JSON:API for CRUD and search on the PASS data model, a custom file API to handle binaries, a custom DOI API, a custom metadata schema API, a custom user service API, and a custom policy service API. The pass-core component runs these APIs, handles authentication, sends messages to queues, and mediates access to static HTTP resources.

Several additional services run on the backend. [Data loaders](../data-loaders) periodically update PASS with the latest information about institutional grants, journal metadata, and PubMed central publications. A deposit service turns submissions to PASS into deposits to repositories like DSpace and PubMed Central. A notification service sends email to users about events. The deposit and notification services monitory message queues. The deposit service also polls PASS for objects it needs to update.

Elide provides a JSON:API based interface to the data model and persists the data model to a database. Both the UI and backend services interact with the data model using JSON:API.

## Knowledge Needed / Skills Inventory

PASS Core covers a lot of technological and research domains. Basic understanding of grants, manuscript submission workflows, and the understanding of the technologies below will be beneficial to the development of Pass Core.

* **Programming Languages**
  * [Java 17+](https://www.oracle.com/java/technologies/downloads/)
* **Frameworks**
  * Knowledge of Spring Boot framework
  * Familiarity with [Elide](https://elide.io/) for data model management and JSON services
* **API Development**
  * Creating and managing RESTful APIs
  * JSON specification

## Technologies Utilized

* [Java 17+](https://www.oracle.com/java/technologies/downloads/)
* [Spring Boot](https://spring.io/projects/spring-boot)
* [Elide](https://elide.io/)
* [Docker](https://www.docker.com/products/docker-desktop/)
* [Amazon SQS](https://aws.amazon.com/sqs/)

## Technical Deep Dive

### Data Model

The [data model](./model/) holds all the information needed to associate users with grants and manage deposits to repositories.

### Building

Java 17, Maven 3.8, and Docker are required.

```shell
mvn clean install
```

This will produce an executabler jar `pass-core-main/target/pass-core-main.jar` and a docker image `ghcr.io/eclipse-pass/pass-core-main`.

#### Running the local build

```shell
java -jar pass-core-main/target/pass-core-main.jar
```

By default, an in memory database is used.

You can verify it is running by making a request like:

```shell
curl -u backend:moo localhost:8080/data/grant
```

#### Running with Docker

To run pass-core in a full local environment use pass-docker. But for testing focused on pass-core, there is a docker environment which just runs pass-core and Postgres. See the pass-core-main/docker-compose.yml. You will have to set the pass-core image version manually. You may also need to adjust environment variables in `pass-core-main/.env`.

In pass-core-main run:

```shell
docker compose up -d
```

### Configuration

The application is configured by its `pass-core-main/src/main/resources/application.yaml` which in turn references a number of environment variables.

By default, pass-core-main, will run with an in memory database. In order to use Postgres, switch to the production profile and set the database environment variables as below.
The liquibase changelog located `pass-core-main/src/main/resources/db/changelog/changelog.yaml` will create the pass-core database schema if needed.

If `PASS_CORE_USE_SQS` is `true`, then pass-core will attempt to connect to Amazon SQS. The connection must be configured with `AWS_REGION`, `AWS_ACCESS_KEY_ID`, and `AWS_SECRET_ACCESS_KEY`. The AWS credentials are also needed if the file service S3 backend is used.

Otherwise, a connection to an ActiveMQ broker can be configured by setting `SPRING_ACTIVEMQ_BROKER_URL`. If `PASS_CORE_EMBED_JMS_BROKER` is true, then an embedded ActiveMQ broker will be started using that url. This can be useful to set tcp transport for connecting containers in a docker environment. The default is an embedded broker using vm transport.

**Environment Variables:**

* spring_profiles_active=production
* AWS_REGION=us-east-1
* AWS_ACCESS_KEY_ID=xxx
* AWS_SECRET_ACCESS_KEY=xxx
* PASS_CORE_APP_LOCATION=classpath:app/
* PASS_CORE_APP_CSP=default-src 'self';
  * Value of Content-Security-Policy set on responses.
* PASS_CORE_DATABASE_URL=jdbc:postgresql://postgres:5432/pass
* PASS_CORE_DATABASE_USERNAME=pass
* PASS_CORE_DATABASE_PASSWORD=moo
* PASS_CORE_PORT=8080
* PASS_CORE_LOG_DIR=${java.io.tmpdir}/pass-core
* PASS_CORE_USER=backend
* PASS_CORE_PASSWORD=moo
* PASS_CORE_USE_SQS=false
* PASS_CORE_EMBED_JMS_BROKER=true
* PASS_CORE_SUBMISSION_QUEUE=pass-submission
* PASS_CORE_DEPOSIT_QUEUE=pass-deposit
* PASS_CORE_IDP_METADATA=classpath:saml2/idp-metadata.xml
* PASS_CORE_INSTN_CHG_LOG=file:////tmp/instn-changelog.yaml
* PASS_CORE_DEFAULT_LOGIN_SUCCESS=/app/
* PASS_CORE_LOGOUT_SUCCESS=/app/
* PASS_CORE_LOGOUT_DELETE_COOKIES="JSESSIONID /"
  * Whitespace separated list of cookie name followed by path to delete on logout.
* PASS_CORE_SP_ID=https://sp.pass/shibboleth
* PASS_CORE_SP_ACS=http://localhost:8080/login/saml2/sso/pass
* PASS_CORE_LOGIN_PROCESSING_PATH=/login/saml2/sso/pass
* PASS_CORE_SP_KEY=classpath:saml2/sp-key.pem
* PASS_CORE_SP_CERT=classpath:saml2/sp-cert.pem
* PASS_CORE_SUBMISSION_EVENT_QUEUE=pass-submission-event
* PASS_CORE_USERTOKEN_KEY=xxx
  * If not present, one is generated. See the [user service](api/user-service.md) for how to create manually.
* PASS_CORE_JAVA_OPTS=""
  * Used by the Docker image to pass arguments to Java
* PASS_CORE_BASE_URL=http://localhost:8080
  * Used when services send URLs to the client such as relationship links.

The environment variables in `pass-core-main/.env` are intended to be used for local testing of pass-core in isolation.

### Access control

SAML 2.0 and HTTP basic authentication are supported. An authenticated user is either authorized with a `BACKEND` or `SUBMITTER` role.

A user that does a SAML login is mapped to a PASS user using locator ids. The provided SAML properties of the user
are interpreted using the spring property `pass.auth.attribute-map`. The user is assigned the `SUBMITTER` role.

There is a single `BACKEND` user specified who logs in using HTTP basic.

The `BACKEND` role can do everything. The `SUBMITTER` role is restricted to creating and modifying certain objects in the data model.
The `SUBMITTER` has full access to all other services. 

Details are available in the [Authentication and Authorization section](authentication-authorization.md).

### SAML configuration

The `PASS_CORE_SP_KEY` and `PASS_CORE_SP_CERT` environment variables set the location of the keys used by pass-core to encrypt SAML communication.
Use `PASS_CORE_SP_ID` to set the identifier of the pass-core SP, `PASS_CORE_IDP_METADATA` to set the location where IDP metadata can be retrieved,
`PASS_CORE_SP_ACS` for the Assertion Consumer Service of the SP and `PASS_CORE_LOGIN_PROCESSING_PATH` to set the path for handling login from the IDP.
Note that `PASS_CORE_SP_ACS` is a URL which must match the path specified in `PASS_CORE_LOGIN_PROCESSING_PATH`.

The defaults are set such that the integration tests can run against a [SimpleSAMLphp based IDP](https://github.com/kenchan0130/docker-simplesamlphp/) using resources included in `saml2/`. These defaults should not be used in production.

The image can be run with:

```shell
docker run --name=idp -p 8090:8080 -e SIMPLESAMLPHP_SP_ENTITY_ID=https://sp.pass/shibboleth -e SIMPLESAMLPHP_SP_ASSERTION_CONSUMER_SERVICE=http://localhost:8080/login/saml2/sso/pass -e SIMPLESAMLPHP_IDP_BASE_URL=http://localhost:8090/   -v ./pass-core/pass-core/main/src/main/resources/saml2/authsources.php:/var/www/simplesamlphp/config/authsources.php -d kenchan0130/simplesamlphp
```

Note the volume mount which is set the user information appropriately for PASS.

### CSRF protection

Requests which have side effects (not a GET, HEAD, or OPTIONS and any request to /doi) are protected from CSRF through the use of a token. The client must provide a cookie XSRF-TOKEN and set a header X-XSRF-TOKEN to the same value. Clients can use any value they want. Browser clients will have the cookie value set by responses and so must first make a non-protected request.

### APIs 

#### App `/app/`

The PASS application is available at `/app/` and `/` is redirected to `/app/`. Requests are resolved against the location given by the environment variable `PASS_CORE_APP_LOCATION`. If a request cannot be resolved, then `/app/index.html` will be returned.  This allows the user interface to handle paths which may not resolve to files.

#### User `/user/`

The [user API](api/user.md) provides information about the logged in user.

#### DOI `/doi/`

The [DOI API](api/doi.md) provides the ability to interact with DOIs.

#### File `/file/`

The [file API](api/file.md) provides a mechanism to persist files.

#### Policy `/policy/`

The [policy API](api/policy.md) indicates what repositories are publication should be pushed to.

#### Metadata Schema

The [metadata schema API](api/metadata-schema.md) provides JSON schemas to describe PASS submission metadata.

#### JSON API

JSON API is deployed at the `/data/` endpoint. All of our data model is available, just divided into attributes and relationships. Note that identifiers are now integers, not URIs.
See the [Elide docs](https://elide.io/pages/guide/v6/10-jsonapi.html) for information on how Elide provides support for filtering and sorting.

See the `/swagger/` endpoint for auto-generated documentation.

You can directly make request with the UI and see what happens. Note when doing a POST to create an object, be sure to edit the type field to have the correct object type and delete the id field to have the id auto-generated.

### Examples

#### Creating a RepositoryCopy

```shell
curl -v -u backend:moo -H "X-XSRF-TOKEN:token" -H "Cookie:XSRF-TOKEN=token" -X POST "http://localhost:8080/data/repositoryCopy" -H "accept: application/vnd.api+json" -H "Content-Type: application/vnd.api+json" -d @rc1.json
```

*rc1.json:*
```JSON
{
  "data": {
    "type": "repositoryCopy",
    "attributes": {
      "accessUrl": "http://example.com/path",
      "copyStatus": "accepted"
    }
  }
}
```

#### Patch a Journal

Add a publisher object to the publisher relationship in a journal. Note that both the journal and publisher objects must already exist.

```shell
curl -u backend:moo -H "X-XSRF-TOKEN:token" -H "Cookie:XSRF-TOKEN=token" -X PATCH "http://localhost:8080/data/journal/1" -H "accept: application/vnd.api+json" -H "Content-Type: application/vnd.api+json" -d @patch.json
```

*patch.json:*
 ```JSON
 {
  "data": {
    "type": "journal",
    "id": "1",
    "relationships": {
      "publisher": {
        "data": {
          "id": "2",
          "type": "publisher"
        }
      }
    }
  }
}
```

### Messages

Messages are JSON objects emitted to a JMS broker as text messages. The different types of messages are sent to different queues specified
by the indicated by the environment variables `PASS_CORE_SUBMISSION_QUEUE`, `PASS_CORE_SUBMISSION_EVENT_QUEUE`, and `PASS_CORE_DEPOSIT_QUEUE`.

When a Submission is created or modified and the submitted field is true, then a SubmissionReady event is emitted.
The id of the Submission will be set in the `submission` field of the message.

When a SubmissionEvent is created, then the a SubmissionEvent message will be sent.
The id of the SubmissionEvent will be set in the `submission-event` field of the message. If the `eventType` field is `APPROVAL_REQUESTED_NEWUSER`,
then an `approval-link` field will be set in the field of the message with a link to be sent to a user.

When a Deposit is created or modified, then a DepositStatus event is emitted.
The id of the Deposit will be set in the `deposit` field of the message.

**Example messages:**

```JSON
{
    "type": "SubmissionReady",
    "submission": "1"
}
```
```JSON
{
    "type": "DepositStatus",
    "deposit": "1"
}
```
```JSON
{
    "type": "SubmissionEvent",
    "submission-event": "1",
    "approval-link": "http://example.com/passui?userToken=xxxx"
}
```

### Debugging problems

To get more information, try changing the logging levels set in `pass-core-main/src/main/resources/logback-spring.xml`.
You might also try setting properties like `-Dlogging.level.org.eclipse.pass=DEBUG`.

The [Elide Docs](https://elide.io/pages/guide/v6/12-audit.html) provide more information on logging and debugging.

## Next Steps / Institution Configuration

### Environmental Variable Setup
PASS is designed to be flexible and can be easily configured using the environment variables in this section and the environment variables mentioned in the [API section](./api) as well.

Key variables to consider include:

* PASS Admin and URLs:

```text
PASS_CORE_BASE_URL=[your-base-url]
PASS_CORE_USER=[your-username]
PASS_CORE_PASSWORD=[your-password]
PASS_CORE_APP_LOCATION=[url-of-front-end]
```

* Database Configuration: Set up the database connection details for PostgreSQL:

```text
PASS_CORE_DATABASE_URL=jdbc:postgresql://[your-database-host]:5432/[database-name]
PASS_CORE_DATABASE_USERNAME=[your-username]
PASS_CORE_DATABASE_PASSWORD=[your-password]
```

* SAML Authentication: Provide the institution-specific values for SAML configurations:

```text
PASS_CORE_IDP_METADATA=classpath:saml2/[institution-idp-metadata].xml
PASS_CORE_SP_ID=https://[your-domain]/shibboleth
PASS_CORE_SP_CERT=classpath:saml2/[institution-sp-cert].pem
PASS_CORE_SP_KEY=classpath:saml2/[institution-sp-key].pem
PASS_CORE_SP_ACS=http://[your-domain]:8080/login/saml2/sso/pass
```

* AWS Configuration (if using SQS or S3):

```text
AWS_REGION=[aws-region]
AWS_ACCESS_KEY_ID=[aws-access-key]
AWS_SECRET_ACCESS_KEY=[aws-secret-key]
PASS_CORE_USE_SQS=true

# If using S3 bucket for the file service
PASS_CORE_FILE_SERVICE_TYPE=S3
PASS_CORE_S3_BUCKET_NAME=[your-bucket-name]
PASS_CORE_S3_REPO_PREFIX=[your-prefix-name]
```

Review and adjust the other environment variables (e.g., queues, ports, CSP policies) as necessary to suit the institution's security and operational policies.

## Database Setup

If using a new PostgreSQL instance, ensure the schema is correctly initialized. The liquibase changelog `(src/main/resources/db/changelog/changelog.yaml)` will handle the schema setup automatically. Verify that:

* The schema is created correctly.
* Any institution-specific schema changes or extensions are applied.

## Custom Policy Configuration

Institutions may have specific deposit and submission policies. Configure these by following the instructions in the [Policy API section](./api/policy.md). This will ensure that the appropriate rules and repositories are applied based on your institutional guidelines.

## Institution-Specific Metadata Schema
If your institution has specific metadata requirements for submissions, you may need to customize the metadata schema using the instructions in the [Metadata Schema API section](./api/policy.md). This section will introduce you to the metadata schema and will assist in creating a metadata schema to match your institutional standards.