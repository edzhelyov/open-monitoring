# open-monitoring
A small repository to keep organized information about common monitoring and performance metrics.

## Logging

Ruby stdlib: https://docs.ruby-lang.org/en/master/Logger.html

* https://devdocs.io/ruby~3.2/syslog
* https://datatracker.ietf.org/doc/html/rfc5424
* https://api.rubyonrails.org/ Search for "log"
* https://guides.rubyonrails.org/v7.2/error_reporting.html
* https://guides.rubyonrails.org/v7.2/debugging_rails_applications.html#the-logger
* https://discuss.rubyonrails.org/t/proposal-a-fully-featured-web-debug-toolbar-panel-that-knows-about-rails-and-turbo/84803/4
* https://github.com/MiniProfiler/rack-mini-profiler
* https://github.com/discourse/logster
* https://github.com/discourse/loggerstash
* https://github.com/orgs/discourse/repositories?language=&q=log&sort=&type=all
* https://en.wikipedia.org/wiki/Tracing_(software)#Event_logging
* https://logger.rocketjob.io/index.html
* https://github.com/dwbutler/logstash-logger

Theory

* https://uptrace.dev/glossary/structured-logging
* https://uptrace.dev/opentelemetry/logs

### Field definition

* https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html
* https://github.com/open-telemetry/semantic-conventions/tree/main/docs/general

## APM client libraries

* AppSignal
* Sentry
* OpenTelemetry
* Datadog
* NewRelic
* (Amazon X-Ray)[https://aws.amazon.com/xray/]

## Metrics

* StatsD
* Prometheus
* OpenTelemetry

# Collecting signals

In theory everything is event. Logs are one specific event, and spans are events with duration, or start and end event. Aggregations on events are in forms of metrics.

Events that are so small it's no reasonable to collect them often are gathered by periodic sampling in the form of metrics – CPU load, Memory usage, etc.
For the rest of the events metrics can be calculated from the raw data, this is approach that is present in the Otel Collector where you can configure what metrics to
calculate from the upcoming data. This approach is not very common.

Signal, as defined by OpenTelemetry, are mainly used for introspection about what was the state and what happened in a system. For these a UI is needed to be able to visualize
the data in the form of tables, graphs and the ability to search and group it.

## Dashboards

For different types of signals there is well established set of default Dashboards which are really good to have automatically. Think of CPU, Free disk, I/O, etc. And number
requests, latency, throughtput. If your UI support such auto dashboards it makes your life much easier, instead of you thinking about what is nice to have visualized in the
first place.

## Alarms

The other important aspect of collecting observability data is to get notified when problems occur. For this it's better if you get predefined alarms for most common
infrastructure issues.

# Databases

When you have a database a few important things to consider are:

* Having backups, a daily backup with 7 days retantion is a good starting point.
* What is your data loss window in case of a crash. It's the time between disk sync and or replica sync.
* Do you have replication?
* Alarms about running out of disk, memory and cpu utilization above 90%.
