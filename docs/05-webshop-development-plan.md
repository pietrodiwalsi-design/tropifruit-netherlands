High-Level Development Plan
===========================

Philippine Dried Fruits -- Netherlands E-Commerce Webshop
---------------------------------------------------------

**Version:** 1.0\
**Date:** June 2026\
**Prepared for:** Peter Van Walsem\
**Based on:** Business Plan + Functional & Non-Functional Requirements

1. Executive Overview
---------------------

### Objective

Build and launch a modern, scalable, API-first e-commerce platform for
importing and selling premium Philippine dried fruits in the Netherlands
(and later EU), supporting both direct-to-consumer (DTC) and B2B
wholesale channels.

### Strategic Alignment

-   **Platform recommendation:** Swell (headless commerce) -- meets 9/10
    Functional Requirements natively
-   **Launch target:** Month 7 (aligned with Business Plan Phase 4)
-   **Architecture:** Headless / API-first to satisfy NFR \#1
    (Scalability) and NFR \#7 (Maintainability)

### Key Success Metrics

-   99.99% uptime (NFR \#2)
-   Zero transaction fees on external gateways (NFR \#4)
-   Full EU food law compliance tagging (FR \#7)
-   Native subscription engine with mixed cart support (FR \#4, FR \#10)

2. Technical Architecture Decision
----------------------------------

### Recommended Stack

  Layer                  Technology                                                Rationale
  ---------------------- --------------------------------------------------------- -----------------------------------------------------------------------------------------
  **Frontend**           Swell + Custom Dutch storefront (Next.js or Hydrogen)     Full Dutch localization, mobile-first
  **Backend Commerce**   Swell (headless)                                          Native subscriptions, unlimited variants, 230+ currencies, separate billing/fulfillment
  **Payment**            Mollie or Adyen (Netherlands)                             Low fees, strong EU compliance, iDEAL support
  **Tax & Duty**         Avalara or native EU VAT handling                         Automated HS-code based import duty + 21% VAT
  **Logistics**          DHL/FedEx API integration                                 Real-time rates, AWB generation, tracking
  **Inventory**          Swell multi-location (NL warehouse focus)                 Prevent overselling, expiry/clumping alerts
  **Supplier Portal**    Swell + custom lightweight portal or Google Sheets sync   Purchase orders, document upload, status updates

**Why Swell over Shopify Plus?** - Native subscriptions (no ReCharge
fees) - Unlimited variants (critical for size/flavor/organic combos) -
Separate billing & fulfillment scheduling - Zero transaction fees on
external gateways - 170+ language support for Dutch

3. Phased Development Plan
--------------------------

### Phase 0: Foundation & Setup (Months 1--2)

**Goal:** Legal entity, platform selection, supplier onboarding

**Development Tasks:** - Register Dutch BV or sole proprietorship +
obtain EORI number - Create Swell account + configure EUR pricing +
Dutch/English locales - Set up payment gateway (Mollie) and test
transactions - Define product data model (SKU, HS codes, allergens,
certifications, origin, supplier ID) - Establish supplier onboarding
checklist (CPRS, FDA LTO, CPR, HACCP, lab reports)

**Deliverables:** - Swell store skeleton (EUR, Dutch language) - Product
attribute schema document - Supplier portal requirements finalized

### Phase 1: Core Commerce & Compliance (Months 3--4)

**Goal:** Build minimum viable catalog with full regulatory compliance

**Development Tasks:** - Implement product catalog with EU labeling
attributes (FR \#7) - Ingredients, allergens, country of origin,
supplier details, certifications - Configure wholesale customer groups +
volume pricing (FR \#2) - Set up multi-location inventory (NL warehouse)
with low-stock alerts (FR \#8) - Implement automated tax/duty
calculation at checkout (FR \#6) - Mobile-responsive storefront (NFR
\#9) - Basic compliance document storage (linked to supplier profiles)
(NFR \#3)

**Deliverables:** - Working product catalog (10--15 SKUs) - Wholesale vs
retail pricing logic - Tax & duty calculation in checkout -
Mobile-optimized UI

### Phase 2: Subscriptions & Mixed Cart (Months 5--6)

**Goal:** Enable recurring revenue model and flexible purchasing

**Development Tasks:** - Activate native subscription engine (FR \#4) -
Weekly / Monthly / Quarterly intervals - Flexible billing + separate
fulfillment scheduling (FR \#5) - Mixed cart support (one-time +
subscription in single order) (FR \#10) - Subscription management
dashboard for customers - Email notification flows (order confirmation,
shipping, subscription renewal) - Pre-order / backorder logic for
international sourcing delays

**Deliverables:** - Subscription product types live - Mixed cart
checkout flow - Customer subscription management portal - Automated
email sequences

### Phase 3: Logistics Integration & Supplier Portal (Month 6--7)

**Goal:** Connect physical supply chain to digital platform

**Development Tasks:** - Integrate DHL/FedEx API (FR \#9) - Real-time
shipping rates - Air Waybill generation - Customer tracking page - Build
lightweight Supplier Portal (FR \#3) - Purchase order receipt - Status
updates (raw material, production, shipment) - Document upload
(commercial invoice, packing list, phytosanitary cert, lab reports) (NFR
\#8) - Inventory sync between supplier updates and NL warehouse stock

**Deliverables:** - Live shipping rates + tracking - Supplier portal
(MVP) - Document upload + audit trail

### Phase 4: Launch & Optimization (Month 7+)

**Goal:** Public launch + continuous improvement

**Development Tasks:** - Final Dutch language review + cultural QA -
Payment security audit (NFR \#5) - High availability & monitoring setup
(NFR \#2) - Analytics & reporting dashboard (sales, subscriptions,
inventory turnover) - Customer data export / portability (NFR \#10) -
A/B testing framework for conversion optimization

**Deliverables:** - Public Dutch webshop live - Monitoring & alerting in
place - Analytics dashboard - Data export functionality

4. Feature Priority Matrix
--------------------------

  Priority                        Feature                                                     Requirement       Phase     Effort
  ------------------------------- ----------------------------------------------------------- ----------------- --------- --------
  **P0 (Must have for launch)**   Multi-currency (EUR) + Dutch localization                   FR \#1            Phase 1   Medium
  **P0**                          Wholesale pricing + B2B customer groups                     FR \#2            Phase 1   Medium
  **P0**                          EU compliance tagging (allergens, origin, certifications)   FR \#7            Phase 1   High
  **P0**                          Native subscriptions                                        FR \#4            Phase 2   High
  **P0**                          Mixed cart (one-time + subscription)                        FR \#10           Phase 2   Medium
  **P0**                          NL warehouse inventory tracking                             FR \#8            Phase 1   Medium
  **P0**                          Tax/duty automation (HS codes)                              FR \#6            Phase 1   Medium
  **P1 (Launch + 3 months)**      DHL/FedEx integration                                       FR \#9            Phase 3   High
  **P1**                          Supplier portal + document upload                           FR \#3, NFR \#8   Phase 3   High
  **P1**                          Separate billing & fulfillment scheduling                   FR \#5            Phase 2   Medium
  **P2 (Post-launch)**            Advanced analytics & reporting                              NFR \#10          Phase 4   Medium
  **P2**                          Mobile app / PWA (future)                                   NFR \#9           Future    High

5. Non-Functional Requirements Coverage
---------------------------------------

  NFR                                         How Addressed                                       Phase
  ------------------------------------------- --------------------------------------------------- -------------
  **Scalability (NFR \#1)**                   Swell headless/API-first architecture               Phase 0
  **High Availability (NFR \#2)**             Swell SLA + monitoring (99.99% target)              Phase 4
  **Regulatory Data Compliance (NFR \#3)**    Supplier-linked document storage + audit trail      Phase 1 & 3
  **Zero Transaction Fees (NFR \#4)**         External gateway (Mollie/Adyen) via Swell           Phase 0
  **Payment Security (NFR \#5)**              PCI-compliant gateway + security audit              Phase 4
  **Usability & Localization (NFR \#6)**      Dutch-first UI, mobile responsive                   Phase 1
  **Maintainability (NFR \#7)**               Native Swell features (no heavy plugin reliance)    All phases
  **Document Upload Reliability (NFR \#8)**   Supplier portal with file size allowances           Phase 3
  **Mobile Accessibility (NFR \#9)**          Responsive design + PWA consideration               Phase 1
  **Data Ownership (NFR \#10)**               Swell data export + full customer/product control   Phase 4

6. Timeline Summary (Aligned with Business Plan)
------------------------------------------------

  Business Phase            Webshop Development Phase   Key Milestone                                Target Month
  ------------------------- --------------------------- -------------------------------------------- --------------
  Phase 1--2 (Foundation)   Phase 0--1                  Platform setup + core catalog + compliance   Month 4
  Phase 3 (First Import)    Phase 2                     Subscriptions + mixed cart live              Month 6
  Phase 4 (Market Launch)   Phase 3--4                  Logistics integration + public launch        Month 7
  Phase 5 (Scale)           Ongoing                     Supplier portal, analytics, EU expansion     Month 8--18

7. Risks & Mitigations
----------------------

  Risk                                 Impact   Mitigation
  ------------------------------------ -------- ------------------------------------------------------------
  Customs delays affecting inventory   High     Pre-order logic + separate billing/fulfillment in Swell
  Supplier document upload failures    Medium   Supplier portal with clear file requirements + validation
  Tax/duty miscalculation              High     Early integration with Avalara or thorough HS code testing
  Subscription churn                   Medium   Flexible scheduling + strong onboarding emails
  Platform lock-in                     Low      Swell allows full data export + headless flexibility

8. Recommended Next Steps
-------------------------

1.  **Week 1--2:** Finalize Swell account + payment gateway selection
    (Mollie vs Adyen)
2.  **Week 3--4:** Define complete product attribute schema + HS codes
    for dried mangoes
3.  **Month 2:** Begin supplier portal wireframing + document upload
    requirements
4.  **Month 3:** Start Phase 1 development (catalog + compliance
    tagging)
5.  **Month 5:** Freeze subscription requirements and begin Phase 2

**Document prepared by Moshe (OpenClaw) -- June 2026**\
**Source:** Philippine Dried Fruits Netherlands Business Plan + Dried
Fruit Import E-Commerce System Requirements
