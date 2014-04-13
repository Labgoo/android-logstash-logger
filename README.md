android-logstash-logger
=======================

This is a logger service who sends logs to a server.
Current implementation sends the logs in udp.

The logger has two operational modes:
- active : send every log as it comes to the server
- silent : write the logs to files. file per day for MAX_LOG_DAYS (7 is the default now).
 
When changing the log mode from silent to active the log files are flushed to the server.

Configuration steps:
- change the package name to match your project
- set LOGSTASH_SERVER_URL to the logstash server address
- set LOGSTASH_UDP_JSON_PORT set the udp port
- in AndroidManifest.xml add in the application scope:
  <service android:name=".log.LoggerService" />

Work method:
communication with the service is done through intents. currently there are 2 type of actions:
- ACTION_LOG : log a string
- ACTION_SET_MODE: sends with an exrta int EXTRA_MODE which should be either LogMod.silent or LogMod.active
