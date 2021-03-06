# sumo-log4j-appender

A Log4J appender that sends straight to Sumo Logic.

Note: For the Log4J 2 appender, please see https://github.com/SumoLogic/sumologic-log4j2-appender

## Installation

The library can be added to your project using Maven Central by adding the following dependency to a POM file:

```
<dependency>
    <groupId>com.sumologic.plugins.log4j</groupId>
    <artifactId>sumo-log4j-appender</artifactId>
    <version>2.5</version>
</dependency>
```

## Usage

### Set up HTTP Hosted Collector Source in Sumo Logic

Follow these instructions for [setting up an HTTP Source](http://help.sumologic.com/Send_Data/Sources/HTTP_Source) in Sumo Logic.

### Log4J Configuration

Be sure to replace the `url` field with the URL after creating an HTTP Hosted Collector Source in Sumo Logic.

`log4j.properties`:

    # Root logger option
    log4j.rootLogger=INFO, sumo

    # Direct log messages to sumo
    log4j.appender.sumo=com.sumologic.log4j.SumoLogicAppender
    log4j.appender.sumo.layout=org.apache.log4j.PatternLayout
    log4j.appender.sumo.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss,SSS Z} [%t] %-5p %c - %m%n
    log4j.appender.sumo.url=<YOUR_URL_HERE>

    # Optional parameters for Metadata
    log4j.appender.sumo.sourceName=<YOUR SOURCE NAME>
    log4j.appender.sumo.sourceHost=<YOUR SOURCE HOST>
    log4j.appender.sumo.sourceCategory=<YOUR SOURCE CATEGORY>

    # Optional parameters for Proxy servers
    log4j.appender.sumo.proxyAuth=<YOUR AUTHTYPE: basic or ntlm>
    log4j.appender.sumo.proxyHost=<YOUR HOSTNAME>
    log4j.appender.sumo.proxyPort=<YOUR PORT>
    log4j.appender.sumo.proxyUser=<YOUR_USERNAME>
    log4j.appender.sumo.proxyPassword=<YOUR_PASSWORD>
    log4j.appender.sumo.proxyDomain=<YOUR_NTLM_DOMAIN>


### Parameters

| Parameter          | Required? | Default Value | Description                                                                                                                                |
|--------------------|----------|---------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| url                | Yes      |               | HTTP collection endpoint URL                                                                                                               |
| sourceName         | No       | "Http Input"              | Source name to appear when searching on Sumo Logic by `_sourceName`
| sourceHost         | No       | Client IP Address              | Source host to appear when searching on Sumo Logic by `sourceHost`
| sourceCategory     | No       | "Http Input"              | Source category to appear when searching on Sumo Logic by _`sourceCategory`
| proxyHost          | No       |               | Proxy host IP address                                                                                                                      |
| proxyPort          | No       |               | Proxy host port number                                                                                                                     |
| proxyAuth          | No       |               | For basic authentication proxy, set to "basic". For NTLM authentication proxy, set to "ntlm". For no authentication proxy, do not specify. |
| proxyUser          | No       |               | Proxy host username for basic and NTLM authentication. For no authentication proxy, do not specify.                                        |
| proxyPassword      | No       |               | Proxy host password for basic and NTLM authentication. For no authentication proxy, do not specify.                                        |
| proxyDomain        | No       |               | Proxy host domain name for NTLM authentication only

## Building

To build:
- Run "mvn clean package" on the pom.xml in the main level of this project.
- To test running a locally built JAR file, you may need to manually add the following dependencies to your project:
```
    <dependencies>
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>

        <dependency>
            <groupId>org.apache.httpcomponents</groupId>
            <artifactId>httpclient</artifactId>
            <version>4.5.2</version>
        </dependency>
    </dependencies>
```

## License

The Sumo Logic client library is published under the Apache Software License, Version 2.0. Please visit http://www.apache.org/licenses/LICENSE-2.0.txt for details.
