# DEMO-IS

This project stands as a simple setup that facilitates a short [SSO with OAuth demo](demos/README.md) and serve as a __Demo Template__ for branching.

## Docker-Compse

The only prerequisite is a working `docker` instance and the `Demo-IS` project directory.

### Set up

1. Login to wso2 docker directory

    ```shell
    docker login docker.wso2.com
    ```

1. Run `bootstrap` scripts to prep for stack. *This can take a long time to download resources*.

    ```shell
    docker-compose -f bootstrap/docker-compose.yml up && docker-compose -f bootstrap/docker-compose.yml down
    ```

    - *optional* only bootstrap what you need

      ```shell
      docker-compose -f bootstrap/components.yml up && docker-compose -f bootstrap/components.yml down
      ```

      ```shell
      docker-compose -f bootstrap/node-apps.yml up && docker-compose -f bootstrap/node-apps.yml down
      ```

      ```shell
      docker-compose -f bootstrap/tomcat-wars.yml up && docker-compose -f bootstrap/tomcat-wars.yml down
      ```

### Run Identity Server

1. Make any required configuration changes to the [deployment.toml](../configs/identity-server/deployment.toml).

- *optional* Add additional `dropins` or `plugins` to `/components`
- *optional* Add additional `sql` scripts to `/configs/mysql/initdb`

1. Start the stack

    ```shell
    docker-compose pull && docker-compose up -d && docker-compose logs -f identity-server
    ```

1. To shutdown stack. This will allow you to make any config changes

    ```shell
    docker-compose down
    ```

- *optional* Check the `WUM 2.0` update level

    ```shell
    docker image inspect --format '{{ index .Config.Labels "update_level"}}' \
    docker.wso2.com/wso2is:5.11.0.0
    ```

### Run Web Apps

- *optional* Modify any webapp details `webapps` directory

1. Start webapps

    ```shell
    docker-compose -f webapps/docker-compose.yml up -d
    ```

#### React Apps

  1. Update React `JS` app configs `webapps/node/asgardeo-react-js-app/src/config.json`

      ```JSON
      {
        "clientID": "<App OIDC client id>",
        "signInRedirectURL": "https://localhost:5000/",
        "serverOrigin": "https://localhost:9443",
        "enablePKCE": false
      }
      ```

  1. Update React `TS` app configs `webapps/node/asgardeo-react-ts-app/src/config.json`

      ```JSON
      {
        "clientID": "<App OIDC client id>",    
        "signInRedirectURL": "http://localhost:3000",
        "serverOrigin": "https://localhost:9443",
        "enablePKCE": false
      }
      ```

### *Optional* Show the logs of all of the running services

1. clone [docker-elk](https://github.com/deviantony/docker-elk/) repo
1. start the stack following the instructions for the [logspout](https://github.com/deviantony/docker-elk/tree/main/extensions/logspout) extension
1. setup a default kibana `logstash-*` index pattern through the [UI](https://www.elastic.co/guide/en/kibana/current/index-patterns.html) or [CLI](https://github.com/deviantony/docker-elk#on-the-command-line)

1. update the `log4j2.properties` file to publish all app logs as json:
    - update the console appender to log json at a `TRACE` level

      ``` toml
      appender.<appender_name>.type = Console
      appender.<appender_name>.name = <appender_name>
      appender.<appender_name>.layout.type = JsonLayout
      appender.<appender_name>.layout.compact=true
      appender.<appender_name>.layout.eventEol=true
      appender.<appender_name>.layout.complete=false
      appender.<appender_name>.layout.properties=false
      appender.<appender_name>.layout.propertiesAsList=false
      appender.<appender_name>.layout.locationInfo=true
      appender.<appender_name>.layout.includeStacktrace=true
      appender.<appender_name>.layout.stacktraceAsString=true
      appender.<appender_name>.layout.includeNullDelimiter=false
      appender.<appender_name>.layout.objectMessageAsJsonObject=true
      appender.<appender_name>.filter.threshold.type = ThresholdFilter
      appender.<appender_name>.filter.threshold.level = TRACE
      ```

    - all other file appenders can be removed

    - Update all `logger appederRef` fields to use the `console appender`

      ``` toml
      logger.*.appenderRef.*.ref = <appender_name>
      ```


## Demo Walkthrough

A simple [Demo](./demo/README.md) is described here

## Quick tips and links

[Container Best practices](https://cloud.google.com/architecture/best-practices-for-operating-containers)
[Docker-is repo](https://github.com/wso2/docker-is)
[Sqaush commit branch and save commit messages](https://gitlab.com/-/snippets/1968617)
[docker aliases](https://github.com/akarzim/zsh-docker-aliases)
[Git ui](https://git-fork.com/)
