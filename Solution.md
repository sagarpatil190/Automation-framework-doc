Proposed Solution: Campaign Propagation and Visibility Validation Framework

Solution Overview

To address campaign propagation and visibility issues, we propose building a centralized, configuration-driven validation framework that automatically verifies campaign data across Backend Systems, APIs, and Customer-Facing UI layers.

The framework will provide end-to-end validation of campaign propagation by tracing a campaign from its source configuration in the backend system through downstream APIs and finally to the customer-facing pages where it is expected to be displayed.

The solution will enable early detection of campaign visibility issues, reduce manual verification effort, and provide faster root cause identification.

---

High-Level Architecture

Campaign Management System
           │
           ▼

Campaign Data Collector
           │
           ▼

Campaign Validation Engine
           │

 ┌─────────┼─────────┐

 ▼         ▼         ▼

Backend    API       UI
Validation Validation Validation

 └─────────┼─────────┘

           ▼

      Reporting Layer

           ▼

    Alerting & Monitoring

---

Core Components

1. Campaign Data Collector

Responsible for retrieving campaign information from backend systems.

Data collected:

- Campaign ID
- Campaign Name
- Campaign Status
- Campaign Duration
- Mapped Hotels
- Supplier Associations
- Campaign Rules
- Discount Information

Output:

{
  "campaignId":"CMP123",
  "campaignName":"Summer Sale",
  "mappedHotels":[
      "H001",
      "H002"
  ]
}

This serves as the source of truth for all validations.

---

2. API Validation Layer

Each customer-facing page is powered by a dedicated API.

Examples:

Search Page  → Search API
Results Page → Results API
Details Page → Details API
Cart Page    → Cart API
Order Page   → Order API

The framework will validate whether campaign information is correctly propagated to the corresponding APIs.

Examples:

- Campaign present in Search API
- Campaign present in Details API
- Campaign discount values match backend configuration
- Campaign status propagated correctly

This layer helps identify backend propagation failures before UI validation begins.

---

3. UI Validation Layer

Validate customer-facing rendering of campaign information.

Pages covered:

- Search Results
- Hotel Details
- Room Selection
- Cart
- Checkout
- Booking Confirmation

Validation examples:

- Campaign badge visible
- Campaign banner displayed
- Promotional text accurate
- Discount percentage correct
- Campaign shown on all mapped hotels

This layer validates actual customer experience.

---

4. Network-Based Validation Strategy

Instead of maintaining separate API and UI test datasets, the framework will leverage Playwright network interception.

Approach:

1. Open page
2. Capture API response used by UI
3. Compare API response against backend campaign configuration
4. Validate rendered UI

Benefits:

- Validates actual production traffic
- Eliminates duplicate API authentication logic
- Reduces maintenance effort
- Improves traceability

---

Execution Flow

Campaign Validation Journey

Fetch Campaign
      │
      ▼

Get Mapped Hotels
      │
      ▼

Validate Search API
      │
      ▼

Validate Search UI
      │
      ▼

Validate Details API
      │
      ▼

Validate Details UI
      │
      ▼

Generate Report

---

Configuration-Driven Design

The framework will not require campaign-specific test scripts.

Example configuration:

{
  "campaignType":"HotelPromotion",
  "pages":[
      "search",
      "details"
  ],
  "validations":[
      "campaignBadge",
      "campaignBanner",
      "discount"
  ]
}

This allows support for new campaign types without code changes.

---

Device Coverage

Supported platforms:

- Desktop
- Tablet
- Mobile

Validation will verify that campaign visibility is consistent across supported customer experiences.

Where UI implementations differ, device-specific page objects will be maintained while sharing common validation logic.

---

Reporting Framework

The framework will generate detailed validation reports containing:

Campaign Summary

Campaign: Summer Sale
Campaign ID: CMP123

Mapped Hotels: 500
Validated Hotels: 500
Passed: 492
Failed: 8

Failure Details

Hotel ID: H021

Backend:
PASS

Search API:
PASS

Details API:
PASS

Search UI:
FAIL

Reason:
Campaign badge missing

This enables rapid root cause analysis.

---

Alerting & Monitoring

Validation can be executed:

- On-demand
- Scheduled
- Post-deployment
- Post-campaign creation

Alerts will be triggered when:

- Campaign propagation failures detected
- Missing campaign visibility identified
- API discrepancies found
- Validation thresholds exceeded

Notification channels:

- Email
- Slack
- Teams

---

Scalability Considerations

The framework will support:

- Multiple campaigns
- Multiple suppliers
- Thousands of hotels
- Parallel execution
- Multiple environments

Execution can be distributed across workers to reduce validation time and support large-scale production monitoring.

---

Expected Benefits

1. Automated end-to-end campaign validation.
2. Reduced manual verification effort.
3. Faster identification of campaign visibility issues.
4. Improved confidence in campaign launches.
5. Reduced customer-facing campaign defects.
6. Scalable validation across campaigns, suppliers, hotels, and devices.
7. Clear separation of Backend, API, and UI validation layers for easier troubleshooting.

---

Future Enhancements

Phase 2:

- AI-powered visual validation of campaign banners and badges.

Phase 3:

- Real-time campaign health dashboard.

Phase 4:

- Automatic anomaly detection and proactive alerting.

Phase 5:

- Self-healing validation workflows and intelligent failure classification.
