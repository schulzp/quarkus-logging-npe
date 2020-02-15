# Quarkus 1.2.0 Logging Issue MWE

1. `mvn clean package docker:build docker:run`
2. Startup is suspended until debugger is connected on port `5005`

```text
quarkus-logging-npe> exec java -Dquarkus.http.host=0.0.0.0 -Djava.util.logging.manager=org.jboss.logmanager.LogManager -XX:MaxDirectMemorySize=10M -XX:MaxMetaspaceSize=73144K -XX:ReservedCodeCacheSize=240M -Xss1M -Xmx143943K -server -Djava.awt.headless=true -agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=*:5005 -XX:+ExitOnOutOfMemoryError -cp . -jar /deployments/app.jar
quarkus-logging-npe> Listening for transport dt_socket at address: 5005
quarkus-logging-npe> Exception in thread "main" java.lang.RuntimeException: Failed to start quarkus
quarkus-logging-npe> 	at io.quarkus.runner.ApplicationImpl.doStart(ApplicationImpl.zig:202)
quarkus-logging-npe> 	at io.quarkus.runtime.Application.start(Application.java:87)
quarkus-logging-npe> 	at io.quarkus.runtime.Application.run(Application.java:210)
quarkus-logging-npe> 	at io.quarkus.runner.GeneratedMain.main(GeneratedMain.zig:41)
quarkus-logging-npe> Caused by: java.lang.NullPointerException
quarkus-logging-npe> 	at io.quarkus.runtime.logging.LoggingSetupRecorder.createNamedHandlers(LoggingSetupRecorder.java:138)
quarkus-logging-npe> 	at io.quarkus.runtime.logging.LoggingSetupRecorder.initializeLogging(LoggingSetupRecorder.java:105)
quarkus-logging-npe> 	at io.quarkus.deployment.steps.LoggingResourceProcessor$setupLoggingRuntimeInit11.deploy_0(LoggingResourceProcessor$setupLoggingRuntimeInit11.zig:103)
quarkus-logging-npe> 	at io.quarkus.deployment.steps.LoggingResourceProcessor$setupLoggingRuntimeInit11.deploy(LoggingResourceProcessor$setupLoggingRuntimeInit11.zig:122)
quarkus-logging-npe> 	at io.quarkus.runner.ApplicationImpl.doStart(ApplicationImpl.zig:68)
quarkus-logging-npe> 	... 3 more
```
