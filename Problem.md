Problem Statement: Campaign Propagation and Visibility Validation Framework

Background

The platform supports multiple marketing campaigns that are configured and managed through an internal backend campaign management system. Campaigns can be applied to specific hotels, destinations, suppliers, or booking journeys and are expected to be reflected accurately across customer-facing channels.

Once a campaign is configured in the backend system, the data propagates through multiple backend services and APIs before being rendered on various frontend pages such as Search Results, Hotel Details, Cart, and Booking Confirmation pages.

Currently, there is no automated mechanism to validate whether campaign configurations created in the backend are correctly propagated and displayed across all impacted hotels and customer touchpoints.

Problem

Campaign visibility issues are often discovered manually or after customer reports. A campaign may be correctly configured in the backend but fail to appear on the frontend due to issues in data propagation, API responses, caching, supplier mappings, indexing services, or UI rendering.

Examples include:

- Campaign applied to hotels but not displayed in search results.
- Campaign badge missing on hotel detail pages.
- Incorrect campaign text or discount values shown to customers.
- Campaign visible on some devices but not others.
- Campaign data available in backend systems but missing from downstream APIs.
- Campaign visible for some hotels while missing for other mapped hotels.

These issues can directly impact customer experience, marketing effectiveness, conversion rates, and revenue.

Current Challenges

- Manual verification of campaign visibility is time-consuming and error-prone.
- Campaigns are dynamic and change frequently.
- Multiple suppliers contribute hotel inventory and content.
- Different APIs power different frontend pages.
- Mobile and desktop experiences may follow different UI flows.
- Large-scale validation across thousands of hotels is not feasible manually.
- Root cause identification is difficult because failures may occur in backend systems, APIs, or frontend rendering layers.

Objective

Build a scalable, configuration-driven production validation framework that automatically verifies campaign propagation from backend systems to customer-facing applications.

The framework should:

1. Retrieve campaign configuration and hotel mappings from backend systems.
2. Validate campaign presence in downstream APIs.
3. Validate campaign visibility on customer-facing pages.
4. Verify campaign content such as badges, banners, labels, and promotional messaging.
5. Support multiple campaigns, suppliers, devices, and booking flows.
6. Execute validations at scale with parallel execution.
7. Generate actionable reports identifying impacted hotels and failure points.
8. Enable faster root cause analysis by distinguishing backend, API, and UI failures.

Success Criteria

- Automated validation of campaign visibility across all mapped hotels.
- Significant reduction in manual verification effort.
- Early detection of campaign propagation issues before customer impact.
- Clear reporting of failures at backend, API, and UI layers.
- Support for large-scale campaign validation in production environments.
- Reusable and extensible framework capable of supporting future campaign types and business requirements.
