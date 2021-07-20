# Demo-is Stack with docker-compose

This compose file aims to be a [WYSIWYG](https://en.wikipedia.org/wiki/WYSIWYG) description of the demo stack. It will pull in docker images with as little configuration as necessary. It is designed to mimic the [k8s-is](https://github.com/wso2/kubernetes-is) helm chart as much as possible to make the maintenence of this demo easier.

## Set up

1. Add any required configurations to the [deployment.toml](../config-volumes/identity-server/deployment.toml).

1. Login to wso2 docker directory

    ```shell
    docker login docker.wso2.com
    ```

1. Start the stack

    ```shell
    docker-compose pull && docker-compose up -d
    ```

1. To shutdown stack. This will allow you to make any config changes

    ```shell
    docker-compose down
    ```

1. Check the update level

    ```shell
    docker image inspect --format '{{ index .Config.Labels "update_level"}}' \
    docker.wso2.com/wso2is:5.11.0.0
    ```

### *Optional* Show the logs of all of the running services

1. clone [docker-elk](https://github.com/deviantony/docker-elk/) repo
1. start the stack following the instructions for the [logspout](https://github.com/deviantony/docker-elk/tree/main/extensions/logspout) extension
1. setup a default kibana `logstash-*` index pattern through the [UI](https://www.elastic.co/guide/en/kibana/current/index-patterns.html) or [CLI](https://github.com/deviantony/docker-elk#on-the-command-line)

1. update the `log4j2.properties` file to publish all app logs as json:
    - update the console appender to log json at a `TRACE` level
      ```
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
      ```
      logger.*.appenderRef.*.ref = <appender_name>
      ```
