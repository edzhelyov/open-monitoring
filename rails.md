# Rails monitoring

## Libraries
1. Set all libraries log_level to WARN
2. Collect these logs and monitor them – daily, weekly or set notifications. You can use some error tracker services that catch logs as well.

## Span and events

Events is the more generic concept that includes standard logs, traces and everything that happens in the app.
From OpenTelemetry terminology Event is something that happened without a duration and Span has duration. In reality the Span has one starting event
and one ending event. The typical log line emitted is an Event.

From our standpoint we care about the basic units of work like requests, background jobs, crons and message bus communication when present.
The ability to trace them and have meaningful default attributes will cover 80% of our debugging needs.
