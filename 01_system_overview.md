# EventIQ – System OverviewPage

## Purpose

**EventIQ** is built to empower website owners—ranging from small businesses to large enterprises—to gain actionable insights from their websites. In today's digital landscape, understanding user behavior is critical to improving conversion, retention, and overall business strategy.

The platform helps answer essential questions:
- What are users doing on your website?
- Where do they drop off?
- Which flows or features are underperforming?
- How can you optimize the user journey?

By tracking and analyzing user interactions such as button clicks, form submissions, payment actions, and custom events, EventIQ offers a full-spectrum view of the customer journey. This enables businesses to align their strategies around real usage patterns and customer needs.

---

## Target Audience

- **Small Business Owners**: Track website engagement without needing complex analytics tools.
- **Product Teams**: Understand drop-off rates and optimize feature flows.
- **Marketers**: Gain conversion and campaign performance insights.
- **Engineers**: Instrument user flows easily and monitor frontend/backend event pipelines.

---

## Key Capabilities

- **Custom Event Tracking** – Capture specific business events like checkout start, trial activation, etc.
- **Behavioral Insights** – See how users navigate key flows such as onboarding, signup, or payments.
- **Real-Time Dashboards** – Visualize metrics like conversion rate, flow health, and event frequency.
- **Session Tracking** – Correlate events across multi-step user journeys.
- **Low-Intrusion SDK** – Lightweight JavaScript SDK for event logging with minimal setup.

---

## Why It Matters

In e-commerce and SaaS platforms, the ability to understand **how** and **why** users interact with your application is a strategic advantage. With EventIQ, you're not just collecting data—you’re deriving **business intelligence** from every click, input, or interaction.

The result: better-informed decisions, improved product flows, and increased revenue through insight-driven user experience.

---

# Requirements – EventIQ

## Functional Requirements

### User Management

1. **User Registration**  
   UsersPage can register using:
    - A valid company email and password.
    - Social logins (Google, GitHub).

2. **First-Time Profile Completion**  
   Upon first login, users are prompted to complete their profile with:
    - First name, last name
    - Company name
    - Profile picture
    - Website URL  
      This form should only appear once and be skipped for returning users.

---

### Event Management

1. **Multi-Project Support**  
   UsersPage can create and manage multiple projects (websites/apps), each associated with a unique `iq_project_key` (public SDK key).

2. **Public SDK Key Design**
    - `iq_project_key` is used by the client SDK to send events.
    - While public, it cannot be used to view or retrieve any data.
    - The system should prevent misuse (e.g., via abuse protection or origin validation).

3. **Event Storage**  
   All incoming events are persisted in a high-throughput database to support analytics, reporting, and AI-based inference.

---

### Analytics & Dashboard

1. **Event Context Enrichment**  
   Every event ingested should be enriched with:
    - IP address (geo-location)
    - Device and browser info
    - Referrer and page URL

2. **Custom Event Actions**  
   UsersPage can define high-level action IDs for common events:
    - e.g., `LOGIN`, `REGISTER`, `PAYMENT`, `PAYMENT_CANCELLED`

3. **Engagement Metrics**
    - **DAU / MAU / WAU**: Daily, weekly, monthly active user trends
    - **Average Session Duration**: Time spent on site per session
    - **Bounce Rate**: Single-event sessions or early exits

4. **Temporal Insights**
    - **Event Heatmaps**: Show peak interaction hours per day/week
    - **Session Drop-Off Analysis**: Identify steps where users leave

5. **Conversion Metrics**
    - **Conversion Rate**: Percentage of users completing desired actions
    - **Drop-off Rate**: Where users exit before completion

6. **Real-Time Dashboard**
    - **Live Event Feed**: Stream of incoming events
    - **Online UsersPage**: Active users in last 5 minutes
    - **Top Live Events**: Most frequent current events
    - **System Health Panel**: Latency, ingestion QPS, failures

---

## Non-Functional Requirements

### Security

- Public SDK keys (`iq_project_key`) should be safely handled.
- Keys must not expose or allow unauthorized access to analytics data.
- Optionally restrict ingestion via origin/domain validation.

---

### Scalability & Availability

- The event ingestion pipeline must support **millions of events per second**.
- High availability is critical — the system should **never drop customer events**.
- **Eventual consistency** is acceptable for downstream analytics, but ingestion must be real-time and reliable.

---

### Real-Time Processing

- Analytics services must support **concurrent access** for dashboard users.
- Real-time metrics (live feed, online users) must update with minimal delay.

---

### Durability & Storage

- Events should be durably stored in a fault-tolerant storage layer (e.g., Kafka, PostgreSQL, ClickHouse, or MongoDB).
- Support long-term retention for historical analysis and AI insights.

