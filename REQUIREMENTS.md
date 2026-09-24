# Sales Navigator: Requirements

## What is it?

Sales Navigator is an **internal tool for the InfluxData sales team**. Salespeople use it as their sales script, either **during a sales call** or **when writing emails** to a customer.

The salesperson enters what the customer needs. The tool then:

1. Suggests **one specific product** that fits.
2. Shows **real customer stories** that back up the suggestion.

## How it works

1. **Ask the questions.** The tool suggests which question to ask next, based on what the customer has said so far.
2. **Enter the answers.** The salesperson types or picks the customer's answers.
3. **Get the suggestion.** The tool names one product and explains why in a sentence or two.
4. **Share a story.** The tool shows 1–3 customer stories from companies like this one, with links.
5. **Follow up.** The tool writes a short follow-up email the salesperson can copy, edit and send.

## Questions the tool asks

These are the questions the tool can ask. They are **not a fixed script**. The tool uses AI to pick the next question adaptively, based on what the customer has already said:

- **Skip what's answered.** If the customer already said it, don't ask again.
- **Follow the conversation.** If the customer jumps to budget or security, go there, then come back.
- **Ask what matters most.** Put first the questions whose answers would change the product pick.
- **Dig in when needed.** Ask a short follow-up if an answer is vague or opens a new need.
- **Stop when ready.** Suggest a product once there's enough to pick one. Name any open questions.

The groups below run roughly from big picture down to timeline and budget, but the order is a guide, not a rule.

### About the project

1. What are you trying to do? (For example: monitor servers, collect sensor or IoT data, track equipment, real-time analytics.)
2. What industry are you in?
3. What's prompting this now? What isn't working today?

### What they use today

4. Are you using any open-source InfluxData products today, such as InfluxDB or Telegraf?
5. Are you using any other time series or real-time database products? If so, which ones, and how is it going?

### Their data

6. How much data do you work with today (for example, data points per second or per day), and how fast is it growing?
7. Where does your data come from (servers, devices, apps), and how many machines do you collect it from?

### How they want to run it

8. Do you want us to run it for you in the cloud, or will you run it yourselves?
9. Do you need your own private setup, or extra security like a private network connection?

### Timeline and budget

10. Are you working toward a timeline or deadline?
11. Is there budget set aside for this project?
12. Who is championing this project, and who else is involved in the decision to buy?

## Products it can suggest

| Product | Suggest it when the customer… |
| --- | --- |
| [**InfluxDB Cloud Serverless**](https://www.influxdata.com/products/influxdb-cloud/serverless/) | wants us to run it, is starting small or has changing needs, and wants to pay only for what they use |
| [**InfluxDB Cloud Dedicated**](https://www.influxdata.com/products/influxdb-cloud/dedicated/) | wants us to run it but needs their own private setup, a private network connection, or has a large, fast-growing workload |
| [**InfluxDB** (self-hosted)](https://www.influxdata.com/products/influxdb-overview/) | wants to run it themselves. Core suits small projects and edge devices. Enterprise suits large, always-on production use. |
| [**Telegraf**](https://www.influxdata.com/time-series-platform/telegraf/) | needs a free tool to collect data from servers, apps or devices |
| [**Telegraf Enterprise**](https://www.influxdata.com/products/telegraf-enterprise/) | runs Telegraf on lots of machines and needs one place to manage them all, plus support |

The tool always picks **one** database product. It can add Telegraf or Telegraf Enterprise when the customer needs to collect data.

## Customer stories

The tool only uses stories from these InfluxData pages:

- [Customers](https://www.influxdata.com/customers/)
- [Partners](https://www.influxdata.com/partners/)
- [Blog](https://www.influxdata.com/blog/) (the "Use Cases" posts)

It picks stories from the same industry or with the same kind of need as the customer. Each story shows the company name, what they did, one headline result, and a link.

A few to start with:

| Company | Industry | What they did |
| --- | --- | --- |
| [Eutelsat OneWeb](https://www.influxdata.com/customer/eutelsat) | Space | Satellite data at 1 million data points per second |
| [Seadrill](https://www.influxdata.com/customer/seadrill) | Energy | Saved $55 million by monitoring offshore rigs |
| [Texas Instruments](https://www.influxdata.com/customer/texas-instruments) | Manufacturing | Tracks 1.5 million factory data points per day |
| [Vonage](https://www.influxdata.com/customer/vonage) | Communications | Monitors a global service with 99.999% uptime |
| [Capital One](https://www.influxdata.com/customer/capital-one) | Finance | Keeps its systems visible and running |

## Example

> A customer says: *"We run battery storage sites and collect sensor data. We don't want to manage servers, and our security team needs a private connection."*
>
> **Suggestion:** InfluxDB Cloud Dedicated (they want it run for them and need a private connection), plus Telegraf to collect the sensor data.
>
> **Stories:** Seadrill (energy)

## Must-haves

- Only InfluxData employees can use it (sign-in required).
- It's quick and simple enough to use while talking to a customer.
- The questions are non-linear. The tool uses AI to decide, adaptively, which question to ask next.
- The follow-up email is a draft. The salesperson always reviews it before sending.
