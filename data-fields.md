Elasticsearch enforces strict types of the document fields. If it encounters a field that is not defined in a mapping it will assume a
default type based on the value. If you then send a different value for the same field you can have conflicts and Elastic will drop the document.
Apart from that conflicting values in multiple indexes prevent Kibana from aggregations on the field.

One solution is to ensure clients follow consistent naming schema, and enforce it, so that clients are forced to comform. This is what Elastic
are pushing forward with their ECS. OpenTelemetry have similar approach with their Semantic conventions. Actually Elastic donated they ECS schema and
both are going to be merged into one in the upcoming future.
While having a consistent naming and type for common fields, which is important aspect in data warehousing as well, sometimes it is much easier to allow teams
to ingest their structure logs the way they see fit.

One solution is to have one index per application/team, but in big application that could lead to conflicts as well. Especially for dynamic fields. Another option
is to keep an index per application and log event, but I'm not sure how Elasticsearch will handle so many indexes.

Another approach is to just not index all fields, Elasticsearch allows to mark fields and exclude them from search and aggregations. This way we can agree on a given subset
of fields that we are interested in, and then keep the rest for individual reference. I think first versions of Loki had similar architecture, while the recent ones started
to allow more freedom in indexing.

From client perspective, the idea of structured logging is to have a lot of information and then allow for on demand search and aggregations. If you keep part of the fields
as text you can't do aggregations. It is interesting how people solve that in databases like Clickhouse.

## Links

* https://www.elastic.co/guide/en/ecs/current/ecs-reference.html
* https://opentelemetry.io/docs/concepts/semantic-conventions/
