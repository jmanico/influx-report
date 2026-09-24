# Competitors

Use this file when a customer says they use, or are looking at, another database or monitoring tool. It helps the salesperson compete **on facts**.

Each section was built from InfluxData's own comparison pages and blog, then checked against the competitor's own site in September 2026. Where InfluxData's page was out of date or went too far, the claim is under **Don't say**. Competitors change their products. Re-check a section before relying on it if it's more than a few months old.

## Rules for every competitor

- **No FUD.** Never make up a weakness. Never say a competitor is failing, unsafe, abandoned or going away. Never guess their prices or plans.
- **Only what's here.** Don't add weaknesses from memory. If a product isn't in this file, say so and use the general questions below.
- **Ask, don't tell.** Pain questions let the customer name the problems. That lands better than any claim.
- **Works alongside is a win.** If InfluxDB can sit next to their current tool, lead with that. Replacing isn't the only way in.
- **No speed contests.** InfluxData has no current benchmark against any competitor below. Don't say "faster than X". Offer a proof of concept on the customer's own data.
- **DB-Engines.** InfluxData's pages say InfluxDB ranks #1 in the DB-Engines time series category. The score changes every month. Check [db-engines.com](https://db-engines.com/en/ranking/time+series+dbms) before saying it, and never quote the score.
- **Don't say** "most widely deployed time series database in the world". It can't be checked.
- **Be precise about editions.** InfluxDB 3 Core runs on one machine. High availability and multi-node are in InfluxDB 3 Enterprise and the Cloud products ([overview](https://www.influxdata.com/products/influxdb-overview/)).
- **No PromQL.** InfluxDB 3 queries use SQL or InfluxQL. It has no native Prometheus remote-write endpoint. Prometheus data comes in through Telegraf. Don't cite influxdata.com/prometheus/. It describes older versions.
- **Old benchmarks are out.** Blog benchmarks from the InfluxDB 1.x years (for example vs Graphite or Elasticsearch) don't describe today's product. Don't quote them.
- **Switch stories** must also be in `stories.md`. Use their numbers exactly as `stories.md` has them.

## General pain questions

Use these when the product isn't listed below, or to open any competitor conversation:

- "What made you start looking now?"
- "How is it keeping up as your data grows?"
- "How much of your team's time goes into running and tuning it?"
- "How long do you need to keep data, and what does that cost today?"
- "Who else needs to query this data, and how do they do it?"

---

## Time series databases

### TimescaleDB

- **Also called:** Timescale, Tiger Data, Tiger Cloud
- **What it is:** An open-source PostgreSQL extension for time series. The company renamed itself Tiger Data in June 2025. Its managed service is Tiger Cloud. The extension is still called TimescaleDB.
- **Where it's strong:** It's plain PostgreSQL: full SQL, joins with business data, and the whole Postgres ecosystem. Teams that already run Postgres like it.
- **Say:**
  - InfluxDB is built only for time series: data that arrives all the time and rarely changes. InfluxDB 3 Enterprise scales out across nodes. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-timescaledb/))
  - Unlimited cardinality and queries on recent data in under 10 ms. ([overview](https://www.influxdata.com/products/influxdb-overview/))
  - A built-in Python processing engine for transforms, anomaly detection and forecasting. ([overview](https://www.influxdata.com/products/influxdb-overview/))
  - Telegraf's 400+ plugins handle data collection.
- **Ask:**
  - "How are you scaling writes beyond one Postgres server today?"
  - "How much time goes into tuning chunks, compression and vacuum as data grows?"
- **If they say:**
  - *"We already know Postgres and SQL."* InfluxDB 3 uses standard SQL, plus InfluxQL. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-timescaledb/))
  - *"It's one database for everything."* That's fair. InfluxDB is the better fit when most of the workload is time series.
- **Don't say:**
  - That TimescaleDB has multi-node or distributed hypertables. InfluxData's page says so, but Timescale dropped multi-node after version 2.13.
  - That TimescaleDB needs outside tools for data retention. It has built-in retention policies.
  - "Timescale Cloud". Say Tiger Cloud.
  - That TimescaleDB is simply "Apache 2.0". It's dual-licensed: an Apache 2.0 edition and the Timescale License.
- **Switch stories:** WideOpenWest (WOW!) chose InfluxDB Enterprise over Timescale after benchmark testing. That was WOW!'s own test on an older InfluxDB. Tell it as their result, not a general claim.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-timescaledb/) · [Tiger Data rename](https://www.tigerdata.com/blog/timescale-becomes-tigerdata) · [Multi-node deprecation](https://github.com/timescale/timescaledb/blob/main/docs/MultiNodeDeprecation.md) · [Retention policy docs](https://www.tigerdata.com/docs/reference/timescaledb/data-retention/add_retention_policy)

### QuestDB

- **What it is:** An open-source (Apache 2.0) column-based time series database that uses SQL. QuestDB Enterprise is the paid edition, run by the customer or as "bring your own cloud" on AWS or Azure.
- **Where it's strong:** Very fast ingest and SQL with time series extensions. Popular for financial market data. It accepts InfluxDB line protocol and the PostgreSQL wire protocol.
- **Say:**
  - Fully managed options: Cloud Serverless (free tier, then pay for what you use) or Cloud Dedicated (single-tenant, private networking). ([Serverless](https://www.influxdata.com/products/influxdb-cloud/serverless/))
  - Telegraf's 400+ plugins, including MQTT, Modbus and OPC-UA.
  - Python processing engine and automatic retention. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-questdb/))
  - SOC 2 Type II, ISO/IEC 27001 and ISO/IEC 27018 on the Cloud products.
- **Ask:**
  - "Do you want someone else to run this fully, or run it in your own cloud account?"
  - "How are you collecting data from devices and servers today?"
- **If they say:**
  - *"QuestDB ingests faster."* Don't argue numbers. Offer a proof of concept on their data.
  - *"We already send it line protocol."* Line protocol is InfluxDB's own format, so moving is low-friction. ([overview](https://www.influxdata.com/products/influxdb-overview/))
- **Don't say:**
  - That QuestDB has a managed cloud service. InfluxData's page says so, but QuestDB's own site lists only Open Source, Enterprise and BYOC.
  - Any QuestDB price. It isn't public.
- **Switch stories:** None yet.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-questdb/) · [QuestDB pricing](https://questdb.com/pricing/) · [QuestDB Enterprise](https://questdb.com/enterprise/)

### TDengine

- **What it is:** An open-source (AGPLv3) time series database aimed at industrial IoT. It comes as TDengine TSDB-OSS, TSDB-Enterprise and TDengine Cloud.
- **Where it's strong:** A "super table" model (one table per device), built-in stream processing, caching and subscriptions. Clustering is included in the open-source edition.
- **Say:**
  - InfluxDB 3 Core is MIT / Apache 2 licensed. ([overview](https://www.influxdata.com/products/influxdb-overview/)) State the licenses as facts and let the customer's legal team weigh them.
  - Telegraf's 400+ plugins, including OPC-UA, Modbus and MQTT, are free. TDengine's own docs put its industrial protocol connectors in Enterprise.
  - Unlimited cardinality, standard SQL plus InfluxQL.
  - Managed Cloud with SOC 2 Type II and ISO certifications.
- **Ask:**
  - "Has your legal team reviewed the license for how you embed or ship the database?"
  - "Which industrial protocols do you need, and are those connectors in the edition you run?"
- **If they say:**
  - *"Clustering is free in TDengine."* True. Be upfront: InfluxDB 3 Core is single-machine. High availability and multi-node are in Enterprise.
  - *"It's built for industrial IoT."* InfluxDB plus Telegraf covers MQTT, Modbus and OPC-UA.
- **Don't say:**
  - "AGPL is risky" or "you can't use it commercially". That's a legal opinion, not a fact.
  - That TDengine lacks clustering or a cloud service. It has both.
- **Switch stories:** None yet.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-tdengine/) · [TDengine product intro](https://docs.tdengine.com/product-intro/) · [TDengine on GitHub](https://github.com/taosdata/tdengine)

### ClickHouse

- **What it is:** An open-source (Apache 2.0) column-based analytics database. ClickHouse Cloud is the managed service.
- **Where it's strong:** Very fast analytical queries over large data. Good for logs, events, real-time reporting and BI.
- **Say:**
  - Built for time series. InfluxQL has built-in downsampling, time windows and gap filling. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-clickhouse/))
  - Unlimited cardinality, and unlimited tables and columns.
  - Automatic retention and hot/cold tiering to object storage.
  - Telegraf for collection, and Python in the database.
- **Ask:**
  - "How do your devices send data: lots of small writes, or batches?"
  - "Who tunes table engines, partitions and materialized views for your time series data?"
- **If they say:**
  - *"We already use ClickHouse for analytics."* That's fine. Keep it for analytics. InfluxDB fits the continuous time series workload.
  - *"It's faster."* No benchmark to share. Offer a proof of concept.
- **Don't say:**
  - That ClickHouse struggles with high write rates. InfluxData's page says so, but ClickHouse's async inserts are built for that case. At most, ask how they batch.
  - That ClickHouse can't do time series.
- **Switch stories:** None yet.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-clickhouse/) · [ClickHouse async inserts](https://clickhouse.com/docs/optimize/asynchronous-inserts)

### kdb+

- **Also called:** KX, KDB-X, kdb Insights, q
- **What it is:** A commercial column-based time series database from KX, queried with the q language. KDB-X is the next generation and adds Python and SQL. kdb Insights is KX's platform.
- **Where it's strong:** Capital markets: tick data, high-frequency trading, and very fast real-time plus historical analytics.
- **Say:**
  - A free, open-source Core (MIT / Apache 2) and published pay-as-you-go Cloud pricing. kdb+ pricing is by quote. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-kdb/))
  - Standard SQL and InfluxQL.
  - 400+ Telegraf integrations and fully managed Cloud options.
- **Ask:**
  - "How easy is it to hire or train people who know q?" (a question, not a claim)
  - "Beyond trading data, where do you have monitoring or IoT data that doesn't need a kdb license?"
- **If they say:**
  - *"kdb is the standard in finance, and it's the fastest."* Don't dispute it. Position InfluxDB for time series work outside the trading hot path.
  - *"KDB-X has SQL and Python now."* True. Compare on how it's run and how it's priced instead.
- **Don't say:**
  - That KX offers a free 32-bit version. That's outdated. KX now offers a free KDB-X Community Edition.
  - The Community Edition's limits. KX's own pages disagree with each other.
  - "q is hard" or "nobody knows q".
  - The 11B Technologies page's line about what kdb+ "would have cost". It's one customer's estimate of a competitor's price.
- **Switch stories:** 11B Technologies chose InfluxDB over Kx kdb+.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-kdb/) · [KDB-X](https://kx.com/products/kdb-x/) · [KX licensing](https://code.kx.com/q/learn/licensing/)

---

## Metrics and observability

### Prometheus

- **What it is:** An open-source (Apache 2) monitoring system that pulls ("scrapes") metrics and uses the PromQL query language. Now on version 3.x.
- **Where it's strong:** The standard for Kubernetes. A single simple program with service discovery, PromQL and built-in alerting. Version 3 added OpenTelemetry (OTLP) ingest and Remote Write 2.0.
- **Say:**
  - Prometheus's own docs say its local storage "is not clustered or replicated". InfluxDB 3 Enterprise adds high availability, multi-node and read replicas. ([overview](https://www.influxdata.com/products/influxdb-overview/))
  - Stores data as compressed Parquet files in object storage, with unlimited cardinality.
  - Handles more than scraped metrics: events and business data, with SQL, InfluxQL and a Python processing engine. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-prometheus/))
- **Ask:**
  - "How long do you need to keep metrics, and where do they live today?"
  - "Do you track events or business data that isn't a scraped metric?"
- **Works alongside:** Keep Prometheus. Telegraf scrapes the same endpoints, or receives Prometheus remote write, and sends the data to InfluxDB for long-term storage. InfluxData's blog suggests customers "continue using Prometheus as their primary source for metrics." ([blog](https://www.influxdata.com/blog/boost-monitoring-stack-prometheus-node-influxdb/))
- **If they say:**
  - *"Our dashboards and alerts are all PromQL."* Keep them in Prometheus. Add InfluxDB for long-term and non-metric data. Be clear that InfluxDB queries use SQL or InfluxQL, not PromQL.
  - *"It's free."* InfluxDB 3 Core is free and open source too.
- **Don't say:**
  - That InfluxDB 3 accepts Prometheus remote write natively or supports PromQL. It doesn't.
  - That Prometheus "can't do long-term storage". Its docs say it can keep years of data with the right setup.
- **Switch stories:** Mumu moved business metrics off Prometheus to InfluxDB 3 Core. NetApp evaluated Prometheus, then standardized on InfluxDB (say "evaluated", since they never ran it). Index Exchange runs Prometheus for 24-hour short-term storage and InfluxDB for longer-term retention, a good "works alongside" example.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-prometheus/) · [InfluxData blog](https://www.influxdata.com/blog/boost-monitoring-stack-prometheus-node-influxdb/) · [Telegraf Prometheus input](https://docs.influxdata.com/telegraf/v1/input-plugins/prometheus/) · [Prometheus storage docs](https://prometheus.io/docs/prometheus/latest/storage/)

### VictoriaMetrics

- **What it is:** An open-source (Apache 2.0) time series database that works with Prometheus. Single-node or cluster, with a paid Enterprise edition.
- **Where it's strong:** MetricsQL builds on PromQL, and it drops into Grafana in place of Prometheus. Accepts many formats: Prometheus remote write, InfluxDB line protocol, Graphite, OTLP.
- **Say:**
  - Standard SQL plus InfluxQL, and a Python processing engine. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-victoria/))
  - Compute and storage are separate, with Parquet files on object storage.
  - Fully managed options: Cloud Serverless and Cloud Dedicated.
- **Ask:**
  - "Who besides your SRE team needs to query this data, and in what language?"
  - "Do you want to run it yourselves, or have it run for you?"
- **If they say:**
  - *"It already takes our line protocol."* True. What InfluxDB adds is SQL, the processing engine and fully managed Cloud options.
- **Don't say:** That it's weak on cardinality or performance. There's no current evidence of that.
- **Switch stories:** None yet.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-victoria/) · [VictoriaMetrics docs](https://docs.victoriametrics.com/victoriametrics/)

### Grafana Mimir

- **Also called:** Grafana Cloud Metrics, Grafana Enterprise Metrics
- **What it is:** Grafana Labs' open-source (AGPLv3), horizontally scalable, Prometheus-compatible long-term metrics store on object storage.
- **Where it's strong:** Grafana says it's "100% Prometheus compatible" and "tested to 1 billion active series". Fits tightly with the Grafana stack.
- **Say:**
  - A general time series database, not metrics-only: SQL, InfluxQL, row-level deletes and a Python processing engine. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-mimir/))
  - InfluxDB 3 Enterprise: high availability, multi-node, read replicas, long-range compaction.
  - Telegraf's 400+ plugins, including MQTT, Modbus and OPC-UA for IoT data.
- **Ask:**
  - "How much effort goes into running Mimir's services?"
  - "Do you have IoT, sensor or event data that doesn't fit a Prometheus model?"
- **If they say:**
  - *"We're all-in on Grafana."* InfluxDB works with Grafana. Eutelsat OneWeb runs InfluxDB 3 Enterprise, Telegraf and Grafana. ([story](https://www.influxdata.com/customer/eutelsat))
- **Don't say:**
  - That Mimir "doesn't scale".
  - The license as written on InfluxData's page ("APGL"). It's AGPLv3.
- **Switch stories:** None yet.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-mimir/) · [Grafana Mimir](https://grafana.com/oss/mimir/)

### Graphite

- **What it is:** An open-source (Apache 2.0) metrics store and grapher (Carbon and Whisper), first released in 2008. Its docs say it does not collect data for you.
- **Where it's strong:** Simple and well known, with a rich function library. Many older tools already send Graphite format.
- **Say:**
  - Tags, "unlimited tables and columns", SQL plus InfluxQL. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-graphite/))
  - Telegraf does the collecting Graphite doesn't: 400+ plugins.
  - Telegraf reads the Graphite format, so existing senders can feed InfluxDB. ([docs](https://docs.influxdata.com/telegraf/v1/data_formats/input/graphite/))
- **Ask:**
  - "How do you handle tags and dimensions today?"
  - "How much time goes into keeping Carbon and Whisper running?"
- **If they say:**
  - *"It works fine."* Fair. Share a switch story. Hulu and Wayfair both moved off Graphite as they grew.
- **Don't say:**
  - The old benchmark numbers from InfluxData's blog. They're from InfluxDB 1.x.
  - "Graphite is abandoned". If asked, state the fact only: the latest graphite-web release is 1.1.10 (May 2022).
  - Don't confuse the customer **Graphite Energy** with the Graphite database.
- **Switch stories:** Hulu, Wayfair.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-graphite/) · [Telegraf Graphite format](https://docs.influxdata.com/telegraf/v1/data_formats/input/graphite/) · [Graphite overview](https://graphite.readthedocs.io/en/latest/overview.html)

### Datadog

- **What it is:** A SaaS observability platform: infrastructure monitoring, APM, logs, synthetics and more.
- **Where it's strong:** One vendor for everything, with "1,000+ built-in integrations" (Datadog's own page). Quick to start.
- **Say:**
  - A purpose-built time series database you can run yourself or have us run, with SQL plus InfluxQL. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-datadog/))
  - Cloud Serverless: free tier, then pay only for what you use, with unlimited series. ([Serverless](https://www.influxdata.com/products/influxdb-cloud/serverless/))
  - Apps that send DogStatsD can send to InfluxDB through Telegraf's statsd plugin. ([docs](https://docs.influxdata.com/telegraf/v1/input-plugins/statsd/))
- **Ask:**
  - "How predictable is your bill as custom metrics grow?"
  - "Do you need to own your raw data, or keep it long-term?"
- **Works alongside:** InfluxDB can sit beside Datadog for high-volume or long-term metrics.
- **If they say:**
  - *"We need APM and logs in one place."* True. InfluxDB is a time series database, not a full APM suite. Position it for metrics next to Datadog.
- **Don't say:**
  - Any savings figure (such as "70% lower bill"). No current InfluxData page backs one with a named customer.
  - Any Datadog price, or that it's "closed source" as a flat statement.
  - "600 integrations". Datadog now says 1,000+.
- **Switch stories:** None yet.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-datadog/) · [Datadog integrations](https://www.datadoghq.com/product/platform/integrations/) · [Telegraf statsd](https://docs.influxdata.com/telegraf/v1/input-plugins/statsd/)

### Elasticsearch

- **Also called:** Elastic, ELK, Elastic Stack
- **What it is:** A distributed search and analytics engine, strongest at logs and full-text search.
- **Where it's strong:** Powerful full-text search and horizontal scale. It also has time series data streams (TSDS).
- **Say:**
  - Purpose-built for time series: columnar storage and time series SQL functions. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-elasticsearch/))
  - Eutelsat OneWeb replaced Elasticsearch for satellite telemetry.
- **Ask:**
  - "How are storage cost and query speed holding up as your metric volume grows?"
  - "Are metrics and logs sharing one cluster?"
- **Works alongside:** Keep Elastic for logs and search. Put metrics and telemetry in InfluxDB. Eutelsat's story says Elasticsearch "excels at JSON and logs".
- **Don't say:**
  - That Elasticsearch isn't open source. Since 2024 it's also offered under AGPLv3.
  - That it has no time series features. TSDS exists.
  - The old benchmark numbers from InfluxData's blog. They're from InfluxDB 1.x.
- **Switch stories:** Eutelsat OneWeb.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-elasticsearch/) · [Eutelsat story](https://www.influxdata.com/customer/eutelsat) · [Elastic licensing FAQ](https://www.elastic.co/pricing/faq/licensing) · [Elastic TSDS](https://www.elastic.co/docs/manage-data/data-store/data-streams/time-series-data-stream-tsds)

### Zabbix, Nagios and other legacy monitoring tools

- **What they are:** Long-standing open-source monitoring and alerting tools.
- **Note:** This section has no InfluxData comparison page behind it. Use the general pain questions, then a switch story.
- **Switch stories:** RingCentral replaced Zabbix after outgrowing it. Index Exchange moved DevOps monitoring off Zabbix.

---

## Cloud services

### Amazon Timestream

- **Two different products. Ask which one.**
  - **Timestream for LiveAnalytics** is AWS's own engine. AWS closed it to new customers on 6/20/25. AWS says existing workloads aren't affected and it keeps investing in them. AWS recommends new customers "evaluate Amazon Timestream for InfluxDB as an alternative".
  - **Timestream for InfluxDB** is InfluxDB run by AWS: InfluxDB 2.x, and since October 2025 InfluxDB 3 Core and Enterprise. The Enterprise license is billed through AWS Marketplace, and AWS provides the support.
- **Where it's strong:** Native AWS IAM, VPC and billing.
- **Say:**
  - A customer on Timestream for InfluxDB **already runs InfluxDB**. This is partner territory, not a rip-out. ([InfluxData page](https://www.influxdata.com/products/timestream-for-influxdb/))
  - InfluxData positions Cloud Dedicated for teams that want InfluxData's own experts, with 24/7 support and support SLAs. ([InfluxData page](https://www.influxdata.com/products/timestream-for-influxdb/))
  - Cloud Serverless can be bought through AWS Marketplace, so it can use committed AWS spend. ([pricing](https://www.influxdata.com/influxdb-pricing/))
- **Ask:**
  - "Which Timestream are you on, LiveAnalytics or Timestream for InfluxDB?"
  - "Who do you call when you need InfluxDB expertise, and how is that working?"
- **If they say:**
  - *"We're on LiveAnalytics and it works."* That's fair. AWS says existing workloads aren't affected. For new work, AWS itself points to InfluxDB.
  - *"We buy everything through AWS."* They can keep doing that. Cloud Serverless is on AWS Marketplace.
- **Don't say:**
  - That LiveAnalytics is "end of life" or "shutting down". AWS only closed it to new customers.
  - That Timestream for InfluxDB has no high availability. Enterprise clusters span Availability Zones.
  - That Timestream for InfluxDB is only 2.x. It offers InfluxDB 3 too.
  - Anything about AWS pricing.
- **Note:** Timestream for InfluxDB isn't in `products.md`, so don't suggest it. Still pick one product with the "How to pick" steps.
- **Switch stories:** None yet.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-awstimestream/) · [InfluxData: Timestream for InfluxDB](https://www.influxdata.com/products/timestream-for-influxdb/) · [InfluxData blog](https://www.influxdata.com/blog/aws-influxdata-announce-influxdb3-on-amazon-timestream/) · [AWS: LiveAnalytics availability change](https://docs.aws.amazon.com/timestream/latest/developerguide/AmazonTimestreamForLiveAnalytics-availability-change.html)

### Azure Data Explorer

- **Also called:** ADX, Kusto, KQL
- **What it is:** Microsoft's managed big-data analytics service for logs and telemetry, queried with KQL.
- **Where it's strong:** High-volume ingest and rich KQL time series functions (anomaly detection, forecasting). Connects natively to Power BI and Grafana.
- **Say:**
  - Built for time series, with columnar Parquet storage on object storage. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-azuredataexplorer/))
  - Standard SQL plus InfluxQL, so no new query language to learn.
  - Cloud Dedicated supports Azure Private Link. Cloud Serverless is on Azure Marketplace. ([pricing](https://www.influxdata.com/influxdb-pricing/))
- **Ask:**
  - "How do your teams feel about KQL compared with SQL?"
  - "How does Microsoft Fabric fit into your plans for this data?"
- **If they say:**
  - *"We're all-in on Azure."* Cloud Dedicated runs with Azure Private Link, and Cloud Serverless is on Azure Marketplace.
- **Don't say:**
  - That ADX is being retired. Microsoft has a migration guide to Fabric but hasn't announced a retirement.
  - The "200 MB per second per node" figure on InfluxData's page. It isn't on Microsoft's current overview.
- **Switch stories:** None yet.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-azuredataexplorer/) · [Microsoft ADX overview](https://learn.microsoft.com/en-us/azure/data-explorer/data-explorer-overview)

### Snowflake and Google BigQuery

- **What they are:** Cloud data warehouses for BI and large batch analysis.
- **Where they're strong:** Huge-scale SQL analytics and a big BI ecosystem. Both have time series SQL functions.
- **Say:**
  - Real-time, low-latency queries on fresh data. ([BigQuery comparison](https://www.influxdata.com/comparison/influxdb-vs-bigquery/), [Snowflake comparison](https://www.influxdata.com/comparison/influxdb-vs-snowflake/))
  - With Apache Iceberg, InfluxDB data can be queried from Snowflake with "no ETL required" (Enterprise, Cloud Serverless and Cloud Dedicated). ([open data access](https://www.influxdata.com/features/open-data-access/))
- **Ask:**
  - "How fresh does the data need to be for alerts and dashboards?"
  - "What does it cost to run frequent, small time-range queries in the warehouse?"
- **Works alongside:** "InfluxDB does not replace data lakes or data warehouses but works in concert with them." ([blog](https://www.influxdata.com/blog/unleashing-real-time-insights-pairing-influxdb-data-lakes-warehouses/)) Keep the warehouse for BI. Use InfluxDB for real-time.
- **If they say:**
  - *"All our data lives in Snowflake."* Keep it there for BI. InfluxDB handles real-time, and Iceberg shares the data back.
- **Don't say:**
  - That they can't do time series. Both have time series functions.
  - That the Iceberg integration works with BigQuery. InfluxData's pages name Snowflake only.
  - Anything about warehouse pricing.
- **Switch stories:** None yet.
- **Sources:** [InfluxData: Snowflake](https://www.influxdata.com/comparison/influxdb-vs-snowflake/) · [InfluxData: BigQuery](https://www.influxdata.com/comparison/influxdb-vs-bigquery/) · [Open data access](https://www.influxdata.com/features/open-data-access/) · [Snowflake time series docs](https://docs.snowflake.com/en/user-guide/querying-time-series-data)

---

## Industrial historians

### AVEVA PI System

- **Also called:** OSIsoft PI, OSI Pi, PI Server, AVEVA PI Data Infrastructure
- **What it is:** The long-standing industrial data historian, now sold by AVEVA.
- **Where it's strong:** Deep connections to plant equipment, Asset Framework for modeling assets, and a very large installed base in industry.
- **Say:**
  - InfluxDB captures "the high-resolution, high-frequency process data that traditional historians compress, downsample, or age out." ([comparison](https://www.influxdata.com/comparison/influxdb-vs-osipi/))
  - Open formats (Parquet, SQL) and Telegraf's OPC-UA, Modbus and MQTT plugins.
- **Ask:**
  - "What data do you compress or drop today because of historian cost or tag limits?"
  - "How easily can your data science or cloud teams get at the historian data?"
- **Works alongside:** InfluxData recommends running InfluxDB next to the historian. PI stays in place for established OT workflows, regulated data and SCADA, and InfluxDB takes the workloads it can't handle. ([historian workloads](https://www.influxdata.com/historian-workloads/))
- **If they say:**
  - *"PI is our system of record."* Keep it. Stream data to both. PI stays the system of record, and InfluxDB adds real-time and high-resolution analytics. ([blog](https://www.influxdata.com/blog/modernize-your-historian-6-signs/))
  - *"Migration is too risky."* Most teams add InfluxDB alongside PI rather than replacing it. ([blog](https://www.influxdata.com/blog/modernize-your-historian-6-signs/))
- **Don't say:**
  - "Proprietary black box", "slow" or "costly".
  - Anything about PI pricing. It's quote-based.
- **Switch stories:** Teréga replaced OSI Pi with InfluxDB Cloud. Ausgrid replaced its OSIsoft PI historian.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-osipi/) · [Historian workloads](https://www.influxdata.com/historian-workloads/) · [InfluxData blog](https://www.influxdata.com/blog/modernize-your-historian-6-signs/) · [AVEVA PI Data Infrastructure](https://www.aveva.com/en/products/pi-data-infrastructure/)

---

## General-purpose databases

### MongoDB

- **What it is:** A general-purpose document database with a special collection type for time series.
- **Where it's strong:** A flexible document model that app teams know well. Its time series collections improve query efficiency and cut disk use compared with normal collections.
- **Say:**
  - Built for time series at every layer, with compressed columnar storage on object storage. ([comparison](https://www.influxdata.com/comparison/influxdb-vs-mongodb/))
  - SQL, queries on recent data in under 10 ms, unlimited cardinality.
  - Telegraf for collection.
- **Ask:**
  - "How is performance holding up as data and device counts grow?"
  - "How do you handle retention and downsampling today?"
- **If they say:**
  - *"We want one database for everything."* That's fair for app data. InfluxDB fits when data arrives all the time and rarely changes.
- **Don't say:** That MongoDB can't do time series. It has native time series collections.
- **Switch stories:** None yet.
- **Sources:** [InfluxData comparison](https://www.influxdata.com/comparison/influxdb-vs-mongodb/) · [MongoDB time series docs](https://www.mongodb.com/docs/manual/core/timeseries-collections/)

### PostgreSQL, MySQL and SQL Server

- **Also called:** "our regular database", relational database, RDBMS
- **What they are:** Transactional SQL databases, often already running for the customer's apps.
- **Where they're strong:** Mature, well known, and great for business and app data.
- **Say:**
  - Built for time series ingest, compression and time-range queries. ([Postgres](https://www.influxdata.com/comparison/influxdb-vs-postgres/), [MySQL](https://www.influxdata.com/comparison/influxdb-vs-mysql/), [SQL Server](https://www.influxdata.com/comparison/influxdb-vs-sqlserver/))
  - Retention that automatically expires old data after a set time.
  - It's still SQL, so the team's skills carry over.
- **Ask:**
  - "What happens to table size and query speed as sensor or metric volume grows?"
  - "How much time goes into partitioning, indexing and purging old data?"
- **Works alongside:** Keep the relational database for app data. Use InfluxDB for time series.
- **If they say:**
  - *"We know SQL and don't want another database."* InfluxDB 3 speaks SQL natively.
- **Don't say:**
  - That Postgres lacks custom SQL functions. InfluxData's page says so, but it has user-defined functions and extensions.
  - That MySQL "will struggle" without the page's own caveat: "unless highly customized."
- **Switch stories:** Hyperion Six moved off PostgreSQL.
- **Sources:** the three InfluxData comparison pages above.
