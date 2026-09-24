# Products

These are the only products Sales Navigator may suggest. Details were checked against the linked InfluxData product pages in September 2026. Check the page before quoting a price or limit to a customer.

## How to pick

1. **Who runs it?**
   - They want us to run it → a Cloud product (step 2).
   - They want to run it themselves → **InfluxDB (self-hosted)**. Pick **Core** or **Enterprise** (step 3).
   - Not sure yet → go by the other answers, and say which answer would change the pick.
2. **Which Cloud product?**
   - Needs their own private setup, a private network connection (AWS PrivateLink or Azure Private Link), or has a large, fast-growing workload → **InfluxDB Cloud Dedicated**.
   - Otherwise (starting small, changing needs, wants to pay only for what they use) → **InfluxDB Cloud Serverless**.
3. **Which self-hosted edition?**
   - Small project, prototype, or edge devices → **InfluxDB 3 Core** (free, open source).
   - Large, always-on production use that needs high availability → **InfluxDB 3 Enterprise**.
4. **Do they need to collect data?** (from servers, apps or devices)
   - Yes → add **Telegraf**.
   - Yes, and they run it on lots of machines and want one place to manage them all, plus support → add **Telegraf Enterprise** instead.
   - They already have a way to collect data → add neither.

Always suggest exactly **one** database product. Telegraf or Telegraf Enterprise is the only add-on.

## The products

| Product | Suggest it when the customer… |
| --- | --- |
| [**InfluxDB Cloud Serverless**](https://www.influxdata.com/products/influxdb-cloud/serverless/) | wants us to run it, is starting small or has changing needs, and wants to pay only for what they use |
| [**InfluxDB Cloud Dedicated**](https://www.influxdata.com/products/influxdb-cloud/dedicated/) | wants us to run it but needs their own private setup, a private network connection, or has a large, fast-growing workload |
| [**InfluxDB** (self-hosted)](https://www.influxdata.com/products/influxdb-overview/) | wants to run it themselves. Core suits small projects and edge devices. Enterprise suits large, always-on production use. |
| [**Telegraf**](https://www.influxdata.com/time-series-platform/telegraf/) | needs a free tool to collect data from servers, apps or devices |
| [**Telegraf Enterprise**](https://www.influxdata.com/products/telegraf-enterprise/) | runs Telegraf on lots of machines and needs one place to manage them all, plus support |

## Talking points

### InfluxDB Cloud Serverless

- We run it. No servers to manage, and they can start in minutes.
- Free tier to start, then pay only for what they use.
- Handles millions of incoming data streams and unlimited series.
- SOC 2 Type II, ISO/IEC 27001 and ISO/IEC 27018 certified.
- Can be bought through AWS Marketplace.
- **Not** for customers who need a private network connection. That's Cloud Dedicated.

### InfluxDB Cloud Dedicated

- We run it, on infrastructure used only by them (single-tenant). We handle setup, patching and backups.
- Private network connection with AWS PrivateLink or Azure Private Link.
- Data encrypted in transit and at rest. SOC 2 Type II, ISO/IEC 27001 and ISO/IEC 27018 certified.
- Uptime SLA, 24/7 monitoring, and a dedicated customer success manager.
- Built for large workloads: millions of data streams and unlimited series.
- Pricing: point them to the [pricing page](https://www.influxdata.com/influxdb-pricing/) or a quote. Don't guess a number.

### InfluxDB (self-hosted)

- **InfluxDB 3 Core**: free and open source (MIT / Apache 2). Runs on a single machine. Good for edge devices, prototypes and smaller workloads. Runs on Linux, Mac, Windows and Docker.
- **InfluxDB 3 Enterprise**: the commercial edition. Adds high availability, multi-node setups, read replicas, long-range data compaction and enterprise security. For large, always-on production use.
- Both are fast (queries in under 10 ms) and handle unlimited series.
- Customers already using open-source InfluxDB can move up to Enterprise when they need high availability or scale.

### Telegraf

- Free, open-source agent that collects data from servers, apps and devices.
- 400+ plugins, including IoT and factory protocols (MQTT, Modbus, OPC-UA), Kubernetes, Docker and Prometheus.
- A single small program. Works on low-power devices, and buffers data so nothing is lost if the connection drops.
- Sends data to InfluxDB or to many other destinations.

### Telegraf Enterprise

- Adds one place to manage many Telegraf agents: central configuration, live view of the whole fleet, and access controls.
- Enterprise support with Gold-level SLAs.
- Tested at 15,000+ agent check-ins per second. Works alongside the agents they already run.
- Free version for trying it out: up to 20 configurations and 100 agents. Beyond that is a good sign they need the paid version.
- Paid packages start at $18,000 per year and grow with the number of agents.
