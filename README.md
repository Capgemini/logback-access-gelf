LOGBACK-ACCESS-GELF - A GELF Appender for Logback Access
==========================================

Use this appender to log access logs to a Graylog2 server via GELF messages.

If you don't know what [Graylog2](http://graylog2.org) is, jump on the band wagon!


Configuring Logback
---------------------

Add the following to your logback-access.xml configuration file.

[src/main/resources/logback.xml](https://github.com/Moocar/logback-gelf/blob/master/src/test/resources/logback.xml)

    <configuration>
        <appender name="GELF" class="com.capgemini.logbackaccess.gelf.AccessLogGelfAppender">
        		<facility>sample-service-access</facility>
        		<graylog2ServerHost>localhost</graylog2ServerHost>
        		<graylog2ServerPort>8003</graylog2ServerPort>
        		<useMarker>true</useMarker>
        		<graylog2ServerVersion>0.9.6</graylog2ServerVersion>
        		<requestURI>true</requestURI>
        		<remoteHost>true</remoteHost>
        		<protocol>true</protocol>
        		<method>true</method>
        		<statusCode>true</statusCode>
        		<contentLength>true</contentLength>
        		<responseContent>true</responseContent>
        		<headers>Test-Header</headers>
        	</appender>

        <root level="debug">
            <appender-ref ref="GELF" />
        </root>
    </configuration>

Properties
----------

*   **facility**: The name of your service. Appears in facility column in graylog2-web-interface. Defaults to "GELF"
*   **graylog2ServerHost**: The hostname of the graylog2 server to send messages to. Defaults to "localhost"
*   **graylog2ServerPort**: The graylog2ServerPort of the graylog2 server to send messages to. Defaults to 12201
*   **graylog2ServerVersion**: Specify which version the graylog2-server is. This is important because the GELF headers
changed from 0.9.5 -> 0.9.6. Allowed values = 0.9.5 and 0.9.6. Defaults to "0.9.6"
*   **chunkThreshold**: The maximum number of bytes allowed by the payload before the message should be chunked into
smaller packets. Defaults to 1000
*   **staticAdditionalFields**: See static additional fields below. Defaults to empty


Static Additional Fields
-----------------

Use static additional fields when you want to add a static key value pair to every GELF message. Key is the additional
field key (and should thus begin with an underscore). The value is a static string.

E.g in the appender configuration:

        <appender name="GELF" class="GelfAppender">
            ...
            <staticAdditionalField>_node_name:www013</staticAdditionalField>
            ...
        </appender>
        ...