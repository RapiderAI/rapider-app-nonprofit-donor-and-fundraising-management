<!-- Rapider Official App SOW & Specification | App #188: Nonprofit Donor & Fundraising Management (nonprofit-donor-and-fundraising-management) | Domain: IND -->

# #188 Nonprofit Donor & Fundraising Management (`nonprofit-donor-and-fundraising-management`) — Scope of Work (SOW)

- **App Number & Name:** `#188` — Nonprofit Donor & Fundraising Management
- **Proposed App Key:** `nonprofit-donor-and-fundraising-management`
- **Suite / Domain Key & Model Prefix:** `IND` (`Ind*`)
- **Representative Product (`P1`):** Bloomerang
- **Combined Feature Catalog:** [../combined-features/188-nonprofit-donor-and-fundraising-management-features.md](../combined-features/188-nonprofit-donor-and-fundraising-management-features.md)
- **Target Release Posture:** Constituent Retention, Multi-Tender Gift & Sustainer Ledger, Major Gifts & Grants Kanban, Restricted Fund Subledger & Statutory Tax Receipting Microapplication

---

## 1. Executive Outcome & Target Audience

### 1.1 Business Problem Solved
Charities, foundations, NGOs, educational institutions, and cultural nonprofits lose over 55% of first-time donors annually while risking IRS/CRA/Charity Commission audit penalties when fundraising spreadsheets fail to distinguish legal hard credits from DAF/spouse soft credits, miscalculate quid-pro-quo gala deductibility, commingle donor-restricted funds with unrestricted operating cash, or edit issued tax receipts in place. **Rapider Nonprofit Donor & Fundraising Management (`nonprofit-donor-and-fundraising-management`)** unifies donor retention analytics, multi-tender gift & recurring sustainer processing, multi-year pledges, major-gift & institutional grant pipelines, FASB ASC 958 restricted fund subledger handoffs, and tamper-evident tax receipting directly atop canonical Rapider `crm`, `payments`, `subscriptions`, `acc`, `campaigns`, and `events` suites.

### 1.2 Target Personas & Progressive Disclosure
- **SME Fast-Path Defaults (Community Nonprofits, Food Banks, Arts Organizations, 1–15 Staff):** Start immediately with an `Unrestricted General Fund` and clean constituent views linked to `crm`, log card/check/DAF donations, monitor live Donor Retention % and LYBUNT lists, send 48-hour thank-you acknowledgments, and generate compliant single or year-end consolidated tax receipts in one click.
- **Enterprise Progressive Disclosure (National Charities, University/Hospital Foundations, Global NGOs):** Activate FASB ASC 958 / Charities SORP restricted & endowment fund hierarchies (`IndRestrictedFund`), multi-fund split gifts, appreciated stock & in-kind valuations, corporate matching-gift claim pipelines, multi-year enforceable pledge installment schedules with write-off governance, institutional grant compliance deliverables, UK Gift Aid 25% reclaim schedules, and automated GL restriction-release journal handoffs to `acc`.

### 1.3 Measurable Business Outcomes
- **+10–18 Percentage-Point Lift in First-Time Donor Retention:** Sub-48-hour unacknowledged gift queues, generosity scoring, and LYBUNT/SYBUNT stewardship lists convert one-time givers into recurring sustainers.
- **Zero DAF or Quid-Pro-Quo Tax Receipt Violations:** Deterministic receipt rules automatically block tax-deductible receipts on DAF grants (issuing non-tax acknowledgments to the advising donor) and subtract `fairMarketBenefitAmount` on event/gala gifts.
- **100% Restricted Fund & GL Reconciliation:** Balanced `Decimal128` subledger postings to `FinJournalEntry` keep development totals and finance Statement of Activities reconciled to the cent.

### 1.4 Benchmark Summary (`P1`–`P6`)
Synthesizes the retention focus, generosity scoring, DAF attribution, and effortless receipting of **`P1` Bloomerang**, complex soft credits, multi-year pledges, and split-gift rigor of **`P2` Blackbaud Raiser's Edge NXT**, responsive donor signals and P2P fundraising of **`P3` Virtuous**, campaign/fund coding and employer matching of **`P4` DonorPerfect**, canonical CRM householding and grant deliverable management of **`P5` Salesforce Nonprofit Cloud**, and dimensional ASC 958 restricted fund accounting handoffs of **`P6` Sage Intacct Nonprofit**.

---

## 2. In-Scope, Out-of-Scope & Suite Ownership Boundaries

### 2.1 In-Scope Capabilities
1. Constituent donor stewardship profiles (`IndDonorProfile`), retention/LYBUNT/SYBUNT segmentation, anonymity masking, and UK Gift Aid declaration tracking.
2. Multi-tender gift ledger (`IndGiftTransaction` — card/ACH, check, DAF, stock, in-kind), multi-fund splits, quid-pro-quo fair-market-value benefit deduction, tribute/memorial tracking, and hard-vs-soft credit attribution.
3. Multi-year enforceable pledges, installment schedules, recurring sustainer links, and governed write-offs (`IndPledgeCommitment`).
4. Major-gift moves management and institutional grant proposal/award compliance `<rapider-kanban>` (`IndGrantProposal`) plus peer-to-peer fundraiser rollups (`IndPeerFundraiser`).
5. Restricted/unrestricted fund registry (`IndRestrictedFund`) with subledger-to-`acc` (`FinJournalEntry`) gift & restriction-release handoffs.
6. Sequential, immutable void-and-reissue statutory tax receipting (`IndTaxReceipt`).

### 2.2 Out-of-Scope Capabilities (Delegated to Adjacent Rapider Apps)
- **Payment gateway tokenization, ACH clearing, and card dunning execution:** Owned by `payments` (`FinPaymentIntent`) and `subscriptions` (`FinSubscription`).
- **Core General Ledger trial balance, accounts payable disbursements, and audited GAAP balance-sheet generation:** Owned by `acc` (`FinAccount`, `FinJournalEntry`) and `accpayable` (`FinSupplierBill`).
- **Congregational child check-in security badges, worship service orders, and sacramental/pastoral counseling logs:** Owned by `#189 Church & Religious Organization Management`.
- **Broadcast email delivery engines and gala ticket seating check-in:** Owned by `campaigns`/`email` (`MktCampaign`, `MktEmailMessage`) and `events` (`MktEvent`).
- **Standalone custom approval inbox:** Delegated strictly to Rapider Platform Home `WorkItem`s.

### 2.3 Cross-Suite Ownership & Integration Contract

| Domain / App | Owns (Canonical Models) | Integration Contract with `nonprofit-donor-and-fundraising-management` |
| :--- | :--- | :--- |
| **`nonprofit-donor-and-fundraising-management` (`#188` — This App)** | `IndDonorProfile`, `IndRestrictedFund`, `IndGiftTransaction`, `IndPledgeCommitment`, `IndGrantProposal`, `IndPeerFundraiser`, `IndTaxReceipt` | Owns donor retention intelligence, hard/soft gift attribution, pledges, grants, restricted-fund subledger rules, and statutory tax receipts. |
| **Core `crm` App (`CRM` Suite)** | `CrmAccount`, `CrmContact` | Every `IndDonorProfile` binds `crmContactId` or `crmAccountId`; DAF sponsors, foundations, and matching employers are canonical `CrmAccount`s. |
| **`payments` & `subscriptions` (`FIN`)** | `FinPaymentIntent`, `FinSubscription` | Online gifts settle via `FinPaymentIntent`; monthly sustainers link `subscriptionId -> FinSubscription.id`. |
| **`acc` (`FIN` Suite)** | `FinAccount`, `FinJournalEntry` | `IndRestrictedFund` maps to `FinAccount`; settled gifts, pledge receivables, and restriction releases post balanced `FinJournalEntry` batches. |
| **`campaigns` & `events` (`MKT` Suite)** | `MktCampaign`, `MktEvent` | Gifts and P2P pages attribute `appealCampaignId -> MktCampaign.id` and gala/quid-pro-quo events `eventId -> MktEvent.id`. |
| **Rapider Platform Services** | Identity/RBAC, Home `WorkItem`, `projectChannelMessage`, Files | Pledge write-offs and restricted-fund transfers route via Home `WorkItem`s; signed grant agreements & PDF tax receipts reside in Platform Files. |

---

## 3. Primary Web Pages & Sidebar Navigation Architecture

To comply strictly with the **Rapider Minimum 3 Items Sidebar Rule**, all visible pages are organized into **3 sidebar sections (`Overview`, `Giving & Campaigns`, `Funds & Tax Compliance`) containing 3 visible items each (9 visible menu items total)**, while detail and drawer routes set `displayOnMenu: false`.

| # | Route | Page Title | Sidebar Section | Menu Visible | Key Components & UX |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `dashboard` | Fundraising Hub | `Overview` | `true` (Order 1) | KPI cards (`countSWR`), live Donor Retention % gauge, LYBUNT/SYBUNT recovery counters, <48h unacknowledged gift SLA queue, restricted vs. unrestricted chart. |
| 2 | `donors` | Constituent Donors | `Overview` | `true` (Order 2) | Searchable `IndDonorProfile` directory (`findSWR`), `#activeFilterTagsBar` with `Clear all`, generosity score, `<rapider-phone-input>` stewardship mobile, LYBUNT filter pills. |
| 3 | `major-gifts-grants` | Major Gifts & Grants | `Overview` | `true` (Order 3) | `<rapider-kanban>` board across `IDENTIFICATION`, `QUALIFICATION`, `CULTIVATION`, `SOLICITATION_SUBMITTED`, `AWARDED_COMMITTED`, `STEWARDSHIP_REPORTING`, `DECLINED` (`IndGrantProposal`). |
| 4 | `gifts` | Gift & DAF Ledger | `Giving & Campaigns` | `true` (Order 4) | `IndGiftTransaction` ledger, tender badges (`CARD_ACH`, `DAF_GRANT`, `STOCK`, `IN_KIND`), hard/soft credit summary, acknowledgment & receipt status chips. |
| 5 | `pledges-sustainers` | Pledges & Sustainers | `Giving & Campaigns` | `true` (Order 5) | `IndPledgeCommitment` multi-year installment & `FinSubscription` sustainer monitor, past-due installment alerts, matching-gift claim tracker. |
| 6 | `peer-fundraisers` | Peer-to-Peer & Appeals | `Giving & Campaigns` | `true` (Order 6) | `IndPeerFundraiser` captain/team leaderboards linked to `MktCampaign`/`MktEvent`, goal progress bars (`Decimal128`), anonymous-safe recognition preview. |
| 7 | `restricted-funds` | Restricted Funds & GL | `Funds & Tax Compliance` | `true` (Order 7) | `IndRestrictedFund` balances (`UNRESTRICTED`, `PURPOSE_RESTRICTED`, `ENDOWMENT`), mapped `FinAccount`, subledger-to-`FinJournalEntry` posting & release log. |
| 8 | `tax-receipts` | Tax Receipts & Gift Aid | `Funds & Tax Compliance` | `true` (Order 8) | Sequential `IndTaxReceipt` register, batch year-end consolidated statement generator, void-and-reissue action, UK Gift Aid 25% claim export. |
| 9 | `stewardship-analytics` | Retention & Appeal ROI | `Funds & Tax Compliance` | `true` (Order 9) | First-time vs. repeat retention cohorts, campaign cost-to-raise-a-dollar (`MktCampaign`), grant compliance report calendar, light/dark theme charts. |
| 10 | `donor-detail` | Constituent 360 Timeline | *(Hidden)* | `false` | Full `IndDonorProfile` view (`?id=...`), hard vs. soft credit totals, pledges, tax receipts, grounded AI stewardship draft (`projectChannelMessage`), `Back to list`. |
| 11 | `grant-detail` | Grant & Major Gift Dossier | *(Hidden)* | `false` | `IndGrantProposal` award stipulations, linked `IndRestrictedFund` burn rate, milestone deliverables, signed agreement files, `Back to list`. |
| 12 | `gift-drawer` | Record Gift / DAF / Stock | *(Hidden)* | `false` | Sliding drawer capturing payer, tender, multi-fund `Decimal128` splits, quid-pro-quo benefit deduction, soft-credit advisor, `finally` reset & `closePageDrawer()`. |
| 13 | `pledge-drawer` | Create Pledge Schedule | *(Hidden)* | `false` | Sliding drawer configuring multi-year `IndPledgeCommitment`, installment frequency, `IndRestrictedFund` designation, donor `<rapider-phone-input>`, and instant parent refresh. |

### Mandatory Rapider UI Standards Enforced Across All Pages
- **SWR-First Clean Reads:** Initial loads invoke `window.rapiderApi.findSWR` / `countSWR` with zero manual `isDeleted` filter clauses in API payloads and filter `item.isDeleted !== true` in memory.
- **Table Actions & Row Navigation:** Clicking primary identifiers (Constituent Name, Gift Number, Pledge Code, Proposal Title, Receipt Number) navigates to the detail route (`font-semibold text-primary hover:underline cursor-pointer`). **Zero standalone "View" buttons** appear in `Actions`; rows render icon+text **Edit** and icon-only **Delete** (`title="Delete" aria-label="Delete"`).
- **Custom Elements & Contrast:** Stewardship phone inputs use `<rapider-phone-input>`, `#/major-gifts-grants` uses `<rapider-kanban>`, all primary/danger buttons enforce `#ffffff !important` white text, and native browser `alert`/`confirm`/`prompt` are banned.

---

## 4. Canonical Data Models (`Ind*` — 7 Models)

All models belong to the `IND` domain (`Ind*` prefix), omit `projectId`, assign platform UUIDs (`00000000-xxxx-xxxx-xxxx-xxxxxxxxxxxx` in deterministic seeds), store monetary gifts/pledges/benefits/receipts as `Decimal128`, and track concurrency via `version`.

| Model Name | Key Fields & Types | Relationships & External Refs | Invariants & Lifecycle |
| :--- | :--- | :--- | :--- |
| **`IndDonorProfile`** | `id: UUID`, `constituentCode: String`, `donorType: Enum(INDIVIDUAL, HOUSEHOLD, FOUNDATION, CORPORATE, DAF_SPONSOR)`, `displayName: String`, `stewardshipPhone: String (E.164)?`, `lifetimeHardCreditAmt: Decimal128`, `lifetimeSoftCreditAmt: Decimal128`, `firstGiftDate: Date?`, `latestGiftDate: Date?`, `largestGiftAmt: Decimal128`, `currencyCode: String`, `generosityScore: Decimal128 (0..100)`, `retentionCohort: Enum(NEW_FIRST_TIME, REPEAT_ACTIVE, SUSTAINER, LYBUNT, SYBUNT, LAPSED)`, `isAnonymousDefault: Boolean`, `ukGiftAidActive: Boolean`, `ukGiftAidSignedAt: Date?`, `version: Int` | `crmContactId -> CrmContact.id?`, `crmAccountId -> CrmAccount.id?`, `assignedGiftOfficerId -> HrEmployee.id?` | Exactly one of `crmContactId` or `crmAccountId` must be bound as primary legal constituent; `isAnonymousDefault = true` masks `displayName` for non-Finance/non-assigned roles. |
| **`IndRestrictedFund`** | `id: UUID`, `fundCode: String`, `name: String`, `restrictionClass: Enum(UNRESTRICTED_GENERAL, TEMPORARILY_PURPOSE_RESTRICTED, TIME_RESTRICTED, PERMANENT_ENDOWMENT)`, `purposeDescription: String`, `totalContributedAmt: Decimal128`, `releasedOrSpentAmt: Decimal128`, `availableRestrictedBalance: Decimal128`, `currencyCode: String`, `isActive: Boolean`, `version: Int` | `revenueGlAccountId -> FinAccount.id`, `netAssetGlAccountId -> FinAccount.id` | Unique `fundCode`; `releasedOrSpentAmt` on restricted funds cannot exceed `totalContributedAmt` (`availableRestrictedBalance >= 0.00`). |
| **`IndGiftTransaction`** | `id: UUID`, `giftNumber: String`, `receivedAt: DateTime`, `tenderType: Enum(CARD_ACH, CHECK, WIRE, DAF_GRANT, STOCK_SECURITIES, IN_KIND_GOODS, EMPLOYER_MATCH)`, `grossAmount: Decimal128`, `fairMarketBenefitAmount: Decimal128`, `taxDeductibleAmount: Decimal128`, `currencyCode: String`, `fundAllocationsJson: JSON`, `softCreditsJson: JSON`, `tributeType: Enum(NONE, IN_HONOR_OF, IN_MEMORY_OF)`, `tributeHonoreeName: String?`, `isAnonymous: Boolean`, `acknowledgmentStatus: Enum(UNACKNOWLEDGED, ACKNOWLEDGED, NOT_REQUIRED)`, `glPostingStatus: Enum(UNPOSTED, POSTED_TO_GL, REVERSED)`, `status: Enum(PENDING_SETTLEMENT, SETTLED, REFUNDED_VOIDED)`, `version: Int` | `hardCreditDonorId -> IndDonorProfile.id`, `pledgeId -> IndPledgeCommitment.id?`, `grantProposalId -> IndGrantProposal.id?`, `peerFundraiserId -> IndPeerFundraiser.id?`, `paymentIntentId -> FinPaymentIntent.id?`, `appealCampaignId -> MktCampaign.id?`, `eventId -> MktEvent.id?`, `journalEntryId -> FinJournalEntry.id?`, `taxReceiptId -> IndTaxReceipt.id?` | Hard invariants: `sum(fundAllocationsJson.amount) == grossAmount` and `taxDeductibleAmount == max(0, grossAmount - fairMarketBenefitAmount)` unless `tenderType == DAF_GRANT` (where `taxDeductibleAmount == 0.00` for receipting because DAF sponsor already issued tax deduction); `POSTED_TO_GL` gifts cannot be edited in place without a Home `WorkItem` reversal. |
| **`IndPledgeCommitment`** | `id: UUID`, `pledgeNumber: String`, `commitmentType: Enum(FIXED_MULTI_YEAR_PLEDGE, SUSTAINER_RECURRING, MATCHING_CLAIM)`, `pledgedAt: Date`, `totalPledgedAmount: Decimal128`, `paidToDateAmount: Decimal128`, `writtenOffAmount: Decimal128`, `remainingBalanceAmount: Decimal128`, `currencyCode: String`, `installmentFrequency: Enum(MONTHLY, QUARTERLY, SEMI_ANNUAL, ANNUAL, CUSTOM)`, `nextInstallmentDueDate: Date?`, `installmentsJson: JSON`, `status: Enum(ACTIVE, PAST_DUE, FULFILLED, WRITTEN_OFF, CANCELLED)`, `version: Int` | `donorId -> IndDonorProfile.id`, `restrictedFundId -> IndRestrictedFund.id`, `subscriptionId -> FinSubscription.id?`, `writeOffWorkItemId -> WorkItem.id?` | `paidToDateAmount + writtenOffAmount + remainingBalanceAmount == totalPledgedAmount` for fixed pledges; pledge write-offs (`writtenOffAmount > 0`) require Home `WorkItem` approval. |
| **`IndGrantProposal`** | `id: UUID`, `proposalCode: String`, `opportunityType: Enum(INSTITUTIONAL_GRANT, MAJOR_GIFT_ASK)`, `title: String`, `stage: Enum(IDENTIFICATION, QUALIFICATION, CULTIVATION, SOLICITATION_SUBMITTED, AWARDED_COMMITTED, STEWARDSHIP_REPORTING, DECLINED)`, `askAmount: Decimal128`, `awardedAmount: Decimal128?`, `currencyCode: String`, `submissionDeadline: Date?`, `nextComplianceReportDue: Date?`, `deliverablesJson: JSON`, `agreementFileId: UUID?`, `version: Int` | `funderDonorId -> IndDonorProfile.id`, `restrictedFundId -> IndRestrictedFund.id`, `leadOfficerEmployeeId -> HrEmployee.id` | Transitioning `stage` to `AWARDED_COMMITTED` requires `awardedAmount > 0` and binds a target `IndRestrictedFund`. |
| **`IndPeerFundraiser`** | `id: UUID`, `pageSlug: String`, `title: String`, `teamName: String?`, `goalAmount: Decimal128`, `raisedAmount: Decimal128`, `donorCount: Int`, `currencyCode: String`, `status: Enum(ACTIVE, COMPLETED, ARCHIVED)`, `version: Int` | `championDonorId -> IndDonorProfile.id`, `appealCampaignId -> MktCampaign.id`, `restrictedFundId -> IndRestrictedFund.id`, `eventId -> MktEvent.id?` | Gifts through a P2P page record `HARD_CREDIT` to the actual giver and `SOFT_CREDIT` to `championDonorId`. |
| **`IndTaxReceipt`** | `id: UUID`, `receiptSequenceNumber: String`, `receiptScope: Enum(SINGLE_GIFT, ANNUAL_CONSOLIDATED)`, `taxJurisdiction: Enum(US_IRS_501C3, CA_CRA, UK_GIFT_AID, EU_DONATION, NON_DEDUCTIBLE_ACK)`, `taxYear: Int`, `issuedAt: DateTime`, `legalDonorNameSnapshot: String`, `grossGiftTotal: Decimal128`, `benefitValueTotal: Decimal128`, `eligibleTaxDeductibleTotal: Decimal128`, `ukGiftAidReclaimAmt: Decimal128?`, `currencyCode: String`, `goodsOrServicesDisclosure: String`, `status: Enum(ISSUED, VOIDED_REPLACED)`, `voidReason: String?`, `replacedByReceiptId: UUID?`, `pdfFileId: UUID?`, `version: Int` | `donorId -> IndDonorProfile.id`, `giftIds: UUID[]` | Unique sequential `receiptSequenceNumber`; `ISSUED` receipts are strictly immutable — any correction invokes `voidAndReissueTaxReceipt`, marking the original `VOIDED_REPLACED` and creating a new sequential receipt. |

---

## 5. Core End-to-End User Journeys

### Journey 1: DAF Grant vs. Gala Split-Gift Entry & Statutory Receipt Guardrails
1. Gift Processing Specialist opens `#/gifts`, clicks **Record Gift** (`gift-drawer`), and logs a `\$10,000.00` `DAF_GRANT` from `Fidelity Charitable` (`hardCreditDonorId`) advised by constituent `Dr. Maya Lin` (`SOFT_CREDIT`), designated `100%` to `Clean Water Restricted Fund`.
2. `ind.nonprofit.recordGift` credits `\$10,000.00` hard credit to `Fidelity Charitable` and `\$10,000.00` soft credit to `Dr. Maya Lin`, blocks issuing an IRS 501(c)(3) tax-deductible receipt to `Dr. Maya Lin` (`NON_DEDUCTIBLE_ACK` thank-you letter queued instead), and posts a restricted revenue `FinJournalEntry` to `acc`.
3. Next, the specialist logs a `\$500.00` `CARD_ACH` Gala ticket/donation (`eventId -> MktEvent`) with `fairMarketBenefitAmount = \$120.00` dinner value; the command computes `taxDeductibleAmount = \$380.00` (`Decimal128`) and issues sequential receipt `RCPT-2026-004182` disclosing the `\$120.00` quid-pro-quo benefit.

### Journey 2: Major Gift & Foundation Grant Moves Management (`<rapider-kanban>`)
1. Major Gifts Officer opens `#/major-gifts-grants`, filters by `Opportunity Type: "INSTITUTIONAL_GRANT"`, verifies `#activeFilterTagsBar`, and drags `GRT-2026-019 (Gates Regional Literacy Initiative — \$250,000.00)` from `SOLICITATION_SUBMITTED` to `AWARDED_COMMITTED`.
2. The officer links `IndRestrictedFund` (`FND-LIT-2026`), sets `nextComplianceReportDue = 2026-12-15`, and creates a 2-year `IndPledgeCommitment` (`2 x \$125,000.00` installments).
3. Inside `#/grant-detail?id=...`, the officer triggers a grounded AI funder stewardship update in `projectChannelMessage` citing actual restricted spend and milestone KPIs.

### Journey 3: Pledge Write-Off & Restricted Fund Reallocation via Home `WorkItem`
1. Donor requests reallocating a prior `\$5,000.00` gift from `Youth Scholarship Restricted Fund` to `Emergency Relief Restricted Fund` (with signed donor email attached), while a separate uncollectible `\$2,500.00` pledge requires write-off.
2. Both requests are blocked from unilateral CSR execution and generate Rapider Home `WorkItem`s for the Finance Controller & Development Director.
3. Upon approval, reversing and reclassifying `FinJournalEntry` lines post to `acc`, voiding and reissuing any affected `IndTaxReceipt` if tax-deductible terms changed.

### Journey 4: Year-End Consolidated Sustainer Tax Statements
1. In January, Development Operations opens `#/tax-receipts` and triggers **Generate Annual Sustainer Statements** for `taxYear = 2026`.
2. `annualTaxStatementWorkflow` aggregates all unreceipted `SETTLED` monthly `FinSubscription` gifts per `IndDonorProfile`, excludes `DAF_GRANT` items, generates sequential `ANNUAL_CONSOLIDATED` `IndTaxReceipt` PDFs in Platform Files, and updates constituent timelines.

### Journey 5: Record Click-Through Navigation (`Constituent Donors -> Constituent 360 -> Back Restoration`)
1. From `#/donors` filtered to `Retention Cohort: "LYBUNT"` and `Search: "Lin"`, the Development Officer clicks `Dr. Maya Lin`.
2. Router navigates cleanly to `#/donor-detail?id=00000000-0188-0000-0000-000000000210` without `<base href>` 404 diversion, showing both `lifetimeHardCreditAmt` and `lifetimeSoftCreditAmt`, DAF history, and stewardship tasks.
3. Clicking `Back to list` (`#btnGoBack`) returns to `#/donors` with `Retention Cohort: "LYBUNT"` and `Search: "Lin"` preserved in `#activeFilterTagsBar`.

---

## 6. Consolidated Feature Priorities & Work Packages

### `P0` Foundation Work Packages (Must-Have for Initial Release)
- **WP-P0-1 — Constituent Stewardship, Retention & Hard/Soft Attribution (`NFP-001`, `NFP-002`, `NFP-003`):** Deliver `IndDonorProfile` bound to `CrmContact`/`CrmAccount` with `<rapider-phone-input>`, Donor Retention % / LYBUNT / SYBUNT cohorts, and dual hard/soft credit rollups.
- **WP-P0-2 — Multi-Tender Gifts, Quid-Pro-Quo Math, Pledges & Sustainers (`NFP-005`, `NFP-006`, `NFP-007`, `NFP-008`):** Build `IndGiftTransaction` (`FinPaymentIntent` link, multi-fund `Decimal128` splits, benefit deduction), `IndPledgeCommitment` installment schedules, Home `WorkItem` write-offs, and `FinSubscription` sustainer binding.
- **WP-P0-3 — Major Gifts / Grants Kanban & Restricted Fund GL Subledger (`NFP-011`, `NFP-014`, `NFP-015`):** Deliver `<rapider-kanban>` `IndGrantProposal` moves management, `IndRestrictedFund` registry, and balanced `FinJournalEntry` postings to `acc`.
- **WP-P0-4 — Sequential Immutable Tax Receipting (`NFP-016`, `NFP-017`):** Build `IndTaxReceipt` numbering, DAF non-deductible receipt protection, annual sustainer consolidation, and immutable void-and-reissue workflows.

### `P1` Enterprise Scale Work Packages
- **WP-P1-1 — Tribute Giving, Employer Matching, P2P Pages & 48h Stewardship Queue (`NFP-004`, `NFP-009`, `NFP-010`, `NFP-019`):** Add honor/memorial next-of-kin notices, corporate match claim tracking, `IndPeerFundraiser` rollups (`MktCampaign`/`MktEvent`), and <48h unacknowledged gift SLA queues.
- **WP-P1-2 — Grant Milestones, UK Gift Aid & Restricted Diversion Gates (`NFP-012`, `NFP-018`, `NFP-020`):** Deliver grant deliverable calendars, HMRC 25% Gift Aid schedules, and Home `WorkItem` approval gates for restricted-fund reallocations.

### `P2` Adjacent & Grounded AI Work Packages
- **WP-P2-1 — Stewardship AI, Churn Scoring, Appeal ROI & Privacy Masking (`NFP-013`, `NFP-021`, `NFP-022`, `NFP-023`, `NFP-024`):** Deliver grounded AI thank-you/grant briefs in `projectChannelMessage`, sustainer churn alerts, cost-to-raise-a-dollar dashboards, strict anonymous donor masking, and natural-language LYBUNT copilot queries.

---

## 7. Roles, Permissions & Field-Level Governance

| Role | Permitted Actions | Restricted / Field-Level Boundaries |
| :--- | :--- | :--- |
| **Development Associate / Gift Clerk** | Enter `IndGiftTransaction`s, issue standard `IndTaxReceipt`s, send acknowledgments, manage `IndPeerFundraiser` pages. | Cannot write off `IndPledgeCommitment` balances, reallocate posted `IndRestrictedFund` gifts, or edit `ISSUED` tax receipts in place. |
| **Major Gifts / Grants Officer** | Manage assigned `IndDonorProfile` portfolios and `<rapider-kanban>` `IndGrantProposal` pipeline, draft AI stewardship briefs in `projectChannelMessage`. | Cannot modify GL `FinAccount` mappings on `IndRestrictedFund` or unmask `isAnonymous = true` donors outside their assigned portfolio. |
| **Nonprofit Finance Controller** | Configure `IndRestrictedFund` -> `FinAccount` mappings, trigger subledger-to-`FinJournalEntry` postings & restriction releases, approve write-off/reallocation `WorkItem`s, execute `voidAndReissueTaxReceipt`. | Cannot alter immutable donor Gift Aid signature timestamps without new donor documentation. |
| **Volunteer / Event Coordinator** | View `MktEvent` gala check-ins and P2P team progress (`IndPeerFundraiser`) with anonymous gifts masked as `"Anonymous Donor"`. | Zero access to constituent wealth/generosity scores, tax IDs, bank/payment references, or major-gift cultivation notes. |
| **Development Director / Admin** | Full configuration of fundraising appeals, stewardship SLAs, receipt templates, retention analytics, and co-approving high-value `WorkItem`s. | Cannot bypass append-only sequential `IndTaxReceipt` audit logs or post unbalanced GL journals. |

---

## 8. Technical APIs, Guarded Commands, Events & `requiredWorkflows`

### 8.1 Guarded Domain Commands
Every mutating command enforces `idempotencyKey`, `correlationId`, and `expectedVersion`:
- `ind.nonprofit.recordGift` — Validates `Decimal128` fund split conservation, quid-pro-quo / DAF tax-deductibility rules, updates hard/soft credits on `IndDonorProfile`, applies installment payments to `IndPledgeCommitment`, and queues GL posting.
- `ind.nonprofit.issueTaxReceipt` — Generates gapless sequential `IndTaxReceipt` (blocking deductible IRS/CRA receipts on `DAF_GRANT` tenders).
- `ind.nonprofit.voidAndReissueTaxReceipt` — Marks existing `IndTaxReceipt` as `VOIDED_REPLACED` with `voidReason` and atomically issues a new sequential receipt.
- `ind.nonprofit.releaseFundRestriction` — Verifies `availableRestrictedBalance >= amount` on `IndRestrictedFund` and posts ASC 958 restriction-release `FinJournalEntry` to `acc`.

### 8.2 Domain Events Published & Consumed (Kafka)
- **Published:** `ind.nonprofit.giftSettled.v1`, `ind.nonprofit.taxReceiptIssued.v1`, `ind.nonprofit.pledgePastDue.v1`, `ind.nonprofit.grantAwarded.v1`, `ind.nonprofit.fundRestrictionReleased.v1`.
- **Consumed:** `fin.payment.succeeded.v1` / `fin.subscription.renewed.v1` (auto-creates settled `IndGiftTransaction` for recurring sustainers), `mkt.event.registered.v1` (links gala ticket quid-pro-quo benefits).

### 8.3 `requiredWorkflows` (Declared in `app.manifest.json`)
1. `giftSettlementSubledgerAndReceiptWorkflow` — Reconciles `FinPaymentIntent` settlements, updates constituent hard/soft totals & retention cohorts, posts `FinJournalEntry` batches, and triggers 48-hour acknowledgment queues.
2. `pledgeInstallmentAndWriteOffWorkflow` — Dispatches upcoming pledge installment reminders, flags `PAST_DUE` commitments, and routes write-off requests to Home `WorkItem`s.
3. `annualTaxStatementAndGiftAidWorkflow` — Compiles consolidated year-end donor tax statements and UK HMRC Gift Aid 25% reclaim schedules.
4. `donorRetentionCohortSweepWorkflow` — Nightly recalculation of `NEW_FIRST_TIME`, `REPEAT_ACTIVE`, `LYBUNT`, `SYBUNT`, and `LAPSED` statuses plus generosity scores.

### 8.4 Grounded Rapider AI Rules
- AI Stewardship & Grant Briefs (`NFP-013`) and Fundraising Copilot queries (`NFP-024`) MUST ground every figure in `IndDonorProfile`, `IndGiftTransaction`, `IndGrantProposal`, and `IndRestrictedFund` records with clickable citations.
- AI MUST strictly enforce `isAnonymous` masking for unauthorized callers, MUST NEVER fabricate tax deductibility advice, and MUST require explicit human confirmation before dispatching external donor emails, voiding receipts, or releasing restricted funds.

---

## 9. Security, Privacy, Compliance & Non-Functional Requirements

- **IRS Pub 1771, CRA Charities Directorate, UK HMRC Gift Aid & FASB ASC 958:** Enforces statutory contemporaneous written acknowledgment disclosures (`goodsOrServicesDisclosure`), sequential tamper-evident receipt numbering, 7-year financial/tax receipt retention, and strict separation of donor-restricted vs. unrestricted net assets.
- **PCI-DSS, GDPR & Donor Bill of Rights Privacy:** Zero raw card/ACH numbers touch `Ind*` tables (handled exclusively via `payments` `FinPaymentIntent` tokens); donor anonymity preferences (`isAnonymousDefault`, `isAnonymous`) are enforced server-side across APIs and exports.
- **Monetary Precision:** All gift amounts (e.g., `\$10,000.00`), quid-pro-quo fair market values (`\$120.00`), Gift Aid 25% reclaims, and grant burn balances use `Decimal128` — zero floating-point errors.
- **Accessibility & Responsive UX:** Full WCAG 2.2 AA compliance (`#ffffff !important` contrast on primary/danger buttons across light and dark modes, ARIA labels on icon-only Delete buttons) across `390px` gala mobile devices, `768px` major-gift tablets, and `1440px` gift-processing desktops.

---

## 10. Deterministic Acceptance Criteria

1. **Sidebar 3-Item Section Rule:** `app.manifest.json` defines 3 visible sidebar sections (`Overview`, `Giving & Campaigns`, `Funds & Tax Compliance`) with 3 visible items each (`displayOnMenu: true`) and 4 hidden detail/drawer routes (`displayOnMenu: false`).
2. **SWR & Soft-Delete Cleanliness:** Every page load uses `findSWR` / `countSWR` without manual `isDeleted` API query filters and defensively filters `item.isDeleted !== true` in memory.
3. **Active Filter Tags & Clear All:** Filtering `#/donors`, `#/gifts`, or `#/major-gifts-grants` renders `#activeFilterTagsBar` with HTML-escaped dismissible chips and `[Clear all]`, synchronously updating both table and `<rapider-kanban>` views.
4. **Table Action Standard:** Zero standalone "View" buttons exist in `Actions`; Constituent Names, Gift Numbers, Pledge Numbers, Proposal Titles, and Receipt Numbers navigate to detail routes, Edit buttons render icon + text, and Delete buttons render icon-only with `title="Delete"` and `aria-label="Delete"`.
5. **Custom Elements Adoption:** Donor stewardship phone fields use `<rapider-phone-input>`, and `#/major-gifts-grants` uses `<rapider-kanban>`.
6. **Optimistic Lifecycle & Native Dialog Ban:** Saving `gift-drawer` or `pledge-drawer` resets button state in `finally`, calls `closePageDrawer()`, clears SWR cache, and updates parent views optimistically; deletions use `#rapiderConfirmOkBtn` with zero `window.alert`/`confirm`/`prompt`.
7. **DAF & Quid-Pro-Quo Receipt Invariants:** Recording a `DAF_GRANT` sets `taxDeductibleAmount = 0.00` for individual advisor receipting and blocks IRS/CRA tax-deductible receipt issuance to the advisor; recording a gala gift with `grossAmount = \$500.00` and `fairMarketBenefitAmount = \$120.00` sets `taxDeductibleAmount = \$380.00` (`Decimal128`).
8. **Immutable Void-and-Reissue Receipts:** Direct mutation of an `ISSUED` `IndTaxReceipt` fails deterministically; `ind.nonprofit.voidAndReissueTaxReceipt` marks the prior receipt `VOIDED_REPLACED` and creates a new sequential receipt.
9. **Restricted Fund Over-Release & Reallocation Gate:** Releasing more than `availableRestrictedBalance` on an `IndRestrictedFund` is rejected, and reallocating a posted restricted gift requires Home `WorkItem` approval.
10. **Anonymous Donor Masking:** Querying `IndGiftTransaction` or `IndPeerFundraiser` as an Event/Volunteer role masks `displayName` whenever `isAnonymous = true`.
11. **Click-Through Navigation & State Restoration:** Clicking a constituent on `#/donors` transitions to `#/donor-detail?id=...` without `<base href>` 404 diversion, renders hard/soft credits and receipts, and `Back to list` restores prior filter tags.
12. **Canonical Suite Reuse & Zero `projectId`:** Zero `Ind*` models define `projectId`, and constituent masters, payment rails, subscriptions, campaigns, and GL journals reuse `CrmContact`/`CrmAccount`, `FinPaymentIntent`, `FinSubscription`, `MktCampaign`, and `FinJournalEntry`.
