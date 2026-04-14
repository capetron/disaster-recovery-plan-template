# Disaster Recovery Plan Template

A comprehensive, ready-to-use disaster recovery plan (DRP) template for IT teams, compliance officers, and managed service providers. This template covers every critical section of a production disaster recovery plan -- from business impact analysis through recovery procedures and testing schedules.

Use this template as-is or customize it for your organization's specific infrastructure, compliance requirements (CMMC, HIPAA, SOC 2, PCI DSS), and risk profile.

## Table of Contents

- [How to Use This Template](#how-to-use-this-template)
- [Section 1: Plan Overview and Scope](#section-1-plan-overview-and-scope)
- [Section 2: Roles and Responsibilities](#section-2-roles-and-responsibilities)
- [Section 3: Business Impact Analysis (BIA)](#section-3-business-impact-analysis-bia)
- [Section 4: RTO and RPO Definitions](#section-4-rto-and-rpo-definitions)
- [Section 5: Recovery Strategies](#section-5-recovery-strategies)
- [Section 6: Communication Plan](#section-6-communication-plan)
- [Section 7: Detailed Recovery Procedures](#section-7-detailed-recovery-procedures)
- [Section 8: Testing Schedule and Procedures](#section-8-testing-schedule-and-procedures)
- [Section 9: Plan Maintenance](#section-9-plan-maintenance)
- [Appendix A: Contact Directory](#appendix-a-contact-directory)
- [Appendix B: Vendor and Third-Party Contacts](#appendix-b-vendor-and-third-party-contacts)
- [Appendix C: Asset Inventory](#appendix-c-asset-inventory)

---

## How to Use This Template

1. **Fork or download** this repository
2. Replace all `[PLACEHOLDER]` values with your organization's information
3. Complete the Business Impact Analysis tables with your actual systems
4. Define your RTO/RPO targets based on business requirements
5. Fill in contact directories and vendor information
6. Conduct a tabletop exercise using Section 8 as your guide
7. Review and update quarterly (see Section 9)

---

## Section 1: Plan Overview and Scope

### 1.1 Purpose

This Disaster Recovery Plan establishes procedures to recover `[ORGANIZATION NAME]`'s IT infrastructure and critical business systems following a disruptive event. The plan aims to minimize downtime, data loss, and financial impact while ensuring compliance with applicable regulations.

### 1.2 Scope

This plan covers:

- All production servers and infrastructure (on-premises and cloud)
- Network equipment (firewalls, switches, routers, wireless controllers)
- Critical business applications: `[LIST YOUR APPLICATIONS]`
- Data storage and backup systems
- Communication systems (email, VoIP, collaboration tools)
- End-user computing devices (where critical to operations)

### 1.3 Activation Criteria

This plan is activated when any of the following occur:

| Trigger | Example | Activation Authority |
|---------|---------|---------------------|
| Complete site loss | Fire, flood, structural damage | CEO / CIO |
| Extended power outage | >4 hours, generator failure | IT Director |
| Ransomware / cyber attack | Encryption of production systems | CISO / Incident Commander |
| Critical system failure | Primary server cluster failure | IT Director |
| Network outage | ISP failure >2 hours | Network Manager |
| Cloud provider outage | AWS/Azure region failure >1 hour | IT Director |

### 1.4 Assumptions

- Offsite backups are current and tested (see Section 8)
- At least one member of each recovery team is available
- Alternate processing site is available within `[X]` hours
- Insurance coverage is current (see Appendix D)

---

## Section 2: Roles and Responsibilities

### 2.1 Disaster Recovery Team Structure

| Role | Primary | Alternate | Phone | Email |
|------|---------|-----------|-------|-------|
| DR Plan Owner | `[Name]` | `[Name]` | `[Phone]` | `[Email]` |
| Incident Commander | `[Name]` | `[Name]` | `[Phone]` | `[Email]` |
| IT Recovery Lead | `[Name]` | `[Name]` | `[Phone]` | `[Email]` |
| Network Recovery Lead | `[Name]` | `[Name]` | `[Phone]` | `[Email]` |
| Application Recovery Lead | `[Name]` | `[Name]` | `[Phone]` | `[Email]` |
| Communications Lead | `[Name]` | `[Name]` | `[Phone]` | `[Email]` |
| Facilities Coordinator | `[Name]` | `[Name]` | `[Phone]` | `[Email]` |

### 2.2 Responsibilities by Role

**Incident Commander:**
- Declares disaster and activates the DR plan
- Coordinates all recovery efforts
- Makes go/no-go decisions for failover and failback
- Provides status updates to executive leadership
- Authorizes emergency spending

**IT Recovery Lead:**
- Executes server and infrastructure recovery procedures
- Coordinates with hosting/cloud providers
- Validates system restoration and data integrity
- Documents recovery actions and timelines

**Communications Lead:**
- Notifies all stakeholders per the communication plan
- Manages external communications (customers, vendors, media)
- Maintains communication logs
- Coordinates with HR for employee communications

---

## Section 3: Business Impact Analysis (BIA)

### 3.1 Critical Business Functions

Complete this table for each business function. Rank by priority (1 = highest).

| Priority | Business Function | Department | Supporting Systems | Max Tolerable Downtime | Financial Impact (per hour) | Regulatory Impact |
|----------|-------------------|------------|-------------------|----------------------|---------------------------|-------------------|
| 1 | `[e.g., Payment Processing]` | `[Finance]` | `[System names]` | `[e.g., 1 hour]` | `[$X,XXX]` | `[PCI DSS]` |
| 2 | `[e.g., Email/Communication]` | `[All]` | `[Exchange/M365]` | `[e.g., 4 hours]` | `[$X,XXX]` | `[None]` |
| 3 | `[e.g., Customer Portal]` | `[Operations]` | `[Web servers, DB]` | `[e.g., 8 hours]` | `[$X,XXX]` | `[SLA]` |
| 4 | `[Function]` | `[Dept]` | `[Systems]` | `[Time]` | `[$]` | `[Regulation]` |
| 5 | `[Function]` | `[Dept]` | `[Systems]` | `[Time]` | `[$]` | `[Regulation]` |

### 3.2 Dependencies Matrix

Map each critical system to its dependencies:

| System | Depends On | Network Requirements | Storage Requirements | External Dependencies |
|--------|-----------|---------------------|---------------------|----------------------|
| `[ERP System]` | `[Database server, AD, DNS]` | `[VLAN 10, 100Mbps]` | `[500GB, SAN]` | `[Vendor API]` |
| `[Email]` | `[Exchange/M365, DNS, MX]` | `[Internet, SMTP]` | `[1TB]` | `[Microsoft 365]` |
| `[CRM]` | `[Web server, DB, SSO]` | `[HTTPS, port 443]` | `[200GB]` | `[Salesforce API]` |

---

## Section 4: RTO and RPO Definitions

### 4.1 Definitions

- **Recovery Time Objective (RTO):** Maximum acceptable time to restore a system after a disaster
- **Recovery Point Objective (RPO):** Maximum acceptable data loss measured in time (how old can restored data be?)

### 4.2 RTO/RPO Targets by System Tier

| Tier | Description | RTO Target | RPO Target | Example Systems |
|------|-------------|-----------|-----------|----------------|
| **Tier 1 - Mission Critical** | Systems that directly generate revenue or are legally required | 1 hour | 15 minutes | Payment processing, production databases, ERP |
| **Tier 2 - Business Critical** | Systems required for daily operations | 4 hours | 1 hour | Email, CRM, file shares, VoIP |
| **Tier 3 - Business Important** | Systems that support but do not drive operations | 24 hours | 4 hours | Development environments, reporting, HR systems |
| **Tier 4 - Non-Critical** | Systems that can tolerate extended outages | 72 hours | 24 hours | Training systems, archives, test environments |

### 4.3 Current RTO/RPO by System

| System | Current RTO | Target RTO | Current RPO | Target RPO | Gap? | Remediation Plan |
|--------|------------|-----------|------------|-----------|------|-----------------|
| `[System 1]` | `[Time]` | `[Time]` | `[Time]` | `[Time]` | `[Y/N]` | `[Actions]` |
| `[System 2]` | `[Time]` | `[Time]` | `[Time]` | `[Time]` | `[Y/N]` | `[Actions]` |

---

## Section 5: Recovery Strategies

### 5.1 Backup Strategy

| Backup Type | Frequency | Retention | Storage Location | Encryption | Tested |
|-------------|-----------|-----------|-----------------|------------|--------|
| Full backup | Weekly (Sunday 2 AM) | 4 weeks | `[Offsite/Cloud]` | AES-256 | `[Date]` |
| Incremental | Daily (2 AM) | 2 weeks | `[Offsite/Cloud]` | AES-256 | `[Date]` |
| Transaction logs | Every 15 minutes | 72 hours | `[Local + Offsite]` | AES-256 | `[Date]` |
| System images | Monthly | 3 months | `[Offsite/Cloud]` | AES-256 | `[Date]` |
| Configuration backups | Weekly | 12 weeks | `[Git repo/Offsite]` | AES-256 | `[Date]` |

### 5.2 Recovery Site Options

| Strategy | RTO Achievable | Cost | Best For |
|----------|---------------|------|----------|
| Hot site (active-active) | <1 hour | $$$$$ | Tier 1 systems |
| Warm site (standby) | 4-12 hours | $$$ | Tier 2 systems |
| Cold site (infrastructure only) | 24-72 hours | $$ | Tier 3-4 systems |
| Cloud failover (IaaS) | 1-4 hours | $$-$$$$ | All tiers depending on config |
| Reciprocal agreement | 12-48 hours | $ | Small organizations |

### 5.3 Selected Strategy

`[Document your chosen recovery strategy for each system tier, including vendor, location, and contract details]`

---

## Section 6: Communication Plan

### 6.1 Notification Sequence

**Phase 1: Immediate (0-30 minutes)**
1. DR Plan Owner notifies Incident Commander
2. Incident Commander assembles core recovery team
3. Communications Lead begins stakeholder notification

**Phase 2: Assessment (30-60 minutes)**
1. Recovery teams assess damage and confirm scope
2. Incident Commander makes activation decision
3. Communications Lead notifies executive leadership

**Phase 3: Ongoing (hourly)**
1. Status updates to all stakeholders
2. Customer communications if service is impacted
3. Regulatory notifications if required (within mandated timeframes)

### 6.2 Notification Templates

**Internal Notification (Email/SMS):**
> DISASTER RECOVERY ACTIVATED - `[DATE/TIME]`
>
> Incident: `[Brief description]`
> Impact: `[Systems/services affected]`
> Expected Recovery: `[Estimated time]`
> Action Required: `[What recipients should do]`
>
> Next Update: `[Time]`
> Contact: `[Incident Commander name and phone]`

**Customer Notification:**
> We are currently experiencing a service disruption affecting `[services]`. Our team has activated recovery procedures and we expect to restore service by `[time/date]`. We will provide updates every `[interval]`. For urgent matters, please contact `[alternate contact method]`.

### 6.3 Regulatory Notification Requirements

| Regulation | Notification Requirement | Timeframe | Contact Method |
|------------|------------------------|-----------|---------------|
| HIPAA | HHS breach notification | 60 days | HHS portal |
| PCI DSS | Card brands, acquiring bank | Immediately | Direct contact |
| State breach laws | Affected individuals | Varies by state | Written notice |
| CMMC/DFARS | DIBCNET reporting | 72 hours | dibnet.dod.mil |
| GDPR | Supervisory authority | 72 hours | DPA portal |

---

## Section 7: Detailed Recovery Procedures

### 7.1 Phase 1: Initial Response (0-2 hours)

- [ ] Confirm the disaster event and scope
- [ ] Activate the DR team call tree
- [ ] Assess physical safety of personnel
- [ ] Secure the affected site (if accessible)
- [ ] Begin damage assessment
- [ ] Activate alternate communication channels
- [ ] Notify insurance carrier

### 7.2 Phase 2: System Recovery (2-24 hours)

**Network Recovery:**
- [ ] Activate backup internet circuits
- [ ] Restore firewall configurations from backup
- [ ] Re-establish VPN tunnels to recovery site
- [ ] Verify DNS resolution and update records if needed
- [ ] Test network connectivity between all recovery systems

**Server Recovery (in priority order):**
- [ ] Restore Active Directory / identity services
- [ ] Restore DNS and DHCP services
- [ ] Restore Tier 1 application servers
- [ ] Restore Tier 1 database servers from most recent backup
- [ ] Verify data integrity with checksums
- [ ] Restore Tier 2 systems
- [ ] Restore Tier 3 systems

**Application Recovery:**
- [ ] Validate database consistency
- [ ] Restore application configurations
- [ ] Test application functionality with checklist
- [ ] Verify integrations and API connections
- [ ] Confirm user access and authentication

### 7.3 Phase 3: Validation (ongoing)

- [ ] Run data integrity checks on all restored databases
- [ ] Test critical business workflows end-to-end
- [ ] Verify backup jobs are running on recovered systems
- [ ] Confirm monitoring and alerting is operational
- [ ] Get sign-off from each department head

### 7.4 Phase 4: Failback to Primary Site

- [ ] Confirm primary site is fully operational
- [ ] Plan failback window (minimal business impact)
- [ ] Replicate data from recovery site to primary
- [ ] Execute failback in reverse order (Tier 4 first)
- [ ] Verify all systems on primary site
- [ ] Decommission temporary recovery resources
- [ ] Update DNS and routing
- [ ] Conduct post-failback validation

---

## Section 8: Testing Schedule and Procedures

### 8.1 Testing Calendar

| Test Type | Frequency | Duration | Participants | Next Scheduled |
|-----------|-----------|----------|-------------|---------------|
| Tabletop exercise | Quarterly | 2 hours | DR team + executives | `[Date]` |
| Component test (backup restore) | Monthly | 1-2 hours | IT team | `[Date]` |
| Partial failover test | Semi-annually | 4-8 hours | DR team | `[Date]` |
| Full DR test | Annually | 1-2 days | All teams | `[Date]` |

### 8.2 Tabletop Exercise Scenarios

Use these scenarios for quarterly tabletop exercises:

1. **Ransomware Attack:** All production servers encrypted at 2 AM Saturday. Backups appear intact. Walk through detection, containment, recovery, and communication.
2. **Data Center Flood:** Primary server room has 6 inches of standing water. All on-premises equipment is offline. Power is cut.
3. **Cloud Provider Outage:** Your primary cloud region is down with no ETA. Only local backups are available.
4. **Insider Threat:** A departing employee deleted critical databases and modified backup configurations before leaving.

### 8.3 Test Documentation Template

After each test, document:

- **Test Date:** `[Date]`
- **Test Type:** `[Tabletop / Component / Partial / Full]`
- **Scenario:** `[Description]`
- **Participants:** `[Names and roles]`
- **Objectives Met:** `[Y/N for each objective]`
- **Actual RTO Achieved:** `[Time]`
- **Actual RPO Achieved:** `[Time]`
- **Issues Found:** `[List all gaps]`
- **Corrective Actions:** `[Action items with owners and deadlines]`

---

## Section 9: Plan Maintenance

### 9.1 Review Schedule

| Activity | Frequency | Responsible | Last Completed |
|----------|-----------|------------|---------------|
| Full plan review | Annually | DR Plan Owner | `[Date]` |
| Contact directory update | Quarterly | Communications Lead | `[Date]` |
| BIA review | Annually | Department heads | `[Date]` |
| Backup verification | Monthly | IT Recovery Lead | `[Date]` |
| Vendor contract review | Annually | Procurement | `[Date]` |

### 9.2 Change Triggers

Review and update this plan whenever:

- New critical systems are deployed
- Infrastructure changes occur (cloud migration, new data center)
- Organizational changes affect the DR team
- A real disaster or significant incident occurs
- Test results reveal gaps
- Regulatory requirements change
- Vendor or third-party service changes

---

## Appendix A: Contact Directory

| Name | Role | Work Phone | Mobile | Personal Email | Location |
|------|------|-----------|--------|---------------|----------|
| `[Name]` | `[Role]` | `[Phone]` | `[Phone]` | `[Email]` | `[City]` |

## Appendix B: Vendor and Third-Party Contacts

| Vendor | Service | Support Phone | Account Number | SLA | Escalation Contact |
|--------|---------|--------------|----------------|-----|-------------------|
| `[ISP]` | Internet | `[Phone]` | `[Acct #]` | `[SLA]` | `[Name/Phone]` |
| `[Cloud Provider]` | IaaS | `[Phone]` | `[Acct #]` | `[SLA]` | `[Name/Phone]` |
| `[Backup Vendor]` | Backup/DR | `[Phone]` | `[Acct #]` | `[SLA]` | `[Name/Phone]` |
| `[Insurance]` | Cyber Insurance | `[Phone]` | `[Policy #]` | N/A | `[Agent]` |

## Appendix C: Asset Inventory

| Asset | Type | Location | Serial/Tag | IP Address | Recovery Priority | Backup Method |
|-------|------|----------|-----------|-----------|-------------------|---------------|
| `[Server 1]` | `[Physical/VM]` | `[Location]` | `[Tag]` | `[IP]` | `[Tier 1-4]` | `[Method]` |

---

## Professional Disaster Recovery Services

**Petronella Technology Group** helps businesses build resilient IT infrastructure:

- [Disaster Recovery Planning](https://petronellatech.com/cybersecurity/disaster-recovery/) - Custom DR strategies
- [Managed IT Services](https://petronellatech.com/managed-it-services/) - 24/7 monitoring and backup management
- [Cybersecurity Services](https://petronellatech.com/cybersecurity/) - Comprehensive security posture
- [Compliance Consulting](https://petronellatech.com/compliance/cmmc-compliance-guide/) - CMMC, HIPAA, SOC 2

**Petronella Technology Group** is headquartered in Raleigh, NC. [Contact us](https://petronellatech.com/contact-us/) or call (919) 348-4912.

---

## About

Created and maintained by [Petronella Technology Group](https://petronellatech.com) - a cybersecurity and managed IT services firm based in Raleigh, NC. With 23+ years of experience and zero client breaches, we help businesses secure their infrastructure and achieve compliance.

- **Website:** [petronellatech.com](https://petronellatech.com)
- **Phone:** 919-348-4912
- **Free Assessment:** [Book a consultation](https://book.petronella.ai/blake)

## License

MIT License - See [LICENSE](LICENSE) for details.
