# Bot Governance Policy
## [Agency Name] Website

**Version:** 1.0  
**Effective Date:** [Date]  
**Last Reviewed:** [Date]  
**Next Review:** [Date + 6 months]  
**Document Owner:** [IT Security / Web Operations Team]

---

## 1. Purpose and Scope

### 1.1 Purpose
This policy establishes guidelines for managing automated bot traffic on [Agency Name] public-facing websites. It aims to:

- Ensure public information remains discoverable and accessible
- Protect website infrastructure from abuse and malicious activity
- Balance transparency requirements with security needs
- Comply with federal accessibility and public information mandates
- Provide clear guidance for legitimate bot operators

### 1.2 Scope
This policy applies to:
- All public-facing domains under [agency].gov
- All automated traffic including web crawlers, scrapers, AI training bots, and search engines
- Both read-only crawling and form/API interactions

This policy does not cover:
- Authenticated API access (governed by separate API policies)
- Internal monitoring tools
- Assistive technologies used by individuals with disabilities

### 1.3 Legal and Regulatory Context
This policy operates within:
- Section 508 accessibility requirements
- Freedom of Information Act (FOIA) obligations
- Federal Records Act requirements
- Agency-specific transparency mandates

---

## 2. Policy Principles

### 2.1 Default Openness
Public government information should be discoverable and accessible. We default to allowing legitimate crawlers unless there is a specific security or operational reason to restrict access.

### 2.2 Proportional Response
Bot management measures should be proportional to the risk. We employ graduated responses from rate limiting to blocking based on behavior severity.

### 2.3 Transparency
Our bot policies are publicly documented. Legitimate bot operators can understand and comply with our requirements.

### 2.4 Continuous Improvement
Bot landscapes evolve rapidly. This policy requires regular review and updating based on operational experience.

---

## 3. Bot Classification and Treatment

We define a resonable request rate limit and expect all visitors to abide by it. This level should never be triggered by normal human browsing activity.

### 3.3 Blocking

We use modern tools that are trained on bot behavior across the network and dynamically apply blocks when bots display bad behavior. 

Examples of bad behavior that will trigger automated blocking action includes:

- Exceeding request rate limits 
- port scanning or intrusion like behavior not part of normal browsing
- Requests exceeding 1000 pages over 3 minute from single requestor

---

## 4. Technical Implementation

### 4.1 robots.txt Configuration

Primary bot guidance is published at [agency].gov/robots.txt

**Current Configuration Highlights:**
- Allows major search engines to all public content

**Note:** robots.txt is advisory only. Enforcement occurs at additional layers.

### 4.2 Web Application Firewall (WAF)

**Provider:** [Cloudflare / AWS WAF / Akamai / Other]

**Active Rules:**
2. **Rate Limiting:** Enforce per-IP and per-user-agent rate limits
3. **Known Threat Blocking:** Block IPs from threat intelligence feeds
4. **Geographic Analysis:** Flag unusual geographic patterns (optional)
5. **JavaScript Challenge:** Require JS execution for suspicious requests

**Challenge Actions:**
- Suspicious but unconfirmed bots: JavaScript challenge
- Rate limit exceeded: HTTP 429 with Retry-After header
- Known malicious: HTTP 403 block

### 4.3 User-Agent Filtering

**Server-Level Rules:**
- Block requests with empty user-agents
- Block known malicious user-agent strings

### 4.4 IP Reputation Services

**Active Services:**
- [Spamhaus / AbuseIPDB / Cloudflare Threat Intel / Other]

**Blocking Thresholds:**
- Confirmed malware/botnet sources: Immediate block
- High-confidence spam sources: Block
- Medium-confidence sources: Challenge with CAPTCHA
- TOR exit nodes: [Block / Challenge / Allow] - determined by risk assessment

**Update Frequency:** [Real-time / Hourly / Daily]

### 4.5 Rate Limiting

We don't want to limit the ability of beneficial crawlers from keeping up to date. Bots that consistently run above 1000 requests over 3 minutes may be blocked at the WAF layer. We don't rely on the robots.txt file to control bot request frequency.

### 4.6 Protected Endpoints

**Complete Bot Block (all automated access prohibited):**
- /admin/* - Administrative interfaces
- /login, /auth/* - Authentication endpoints
- /forms/submit - Form submission endpoints
- /search/* - Search functionality (prevents search hammering)
- /*.pdf/download?email=* - Prevents email harvesting
- /api/* - All API endpoints require valid tokens

---

## 5. Monitoring and Response

### 5.1 Monitoring Metrics

The web operations team monitors:
- Bot traffic percentage of total traffic
- Blocked request volume by category
- False positive reports
- Server load correlation with bot activity
- Crawl efficiency of whitelisted bots

**Review Frequency:** Weekly operational review, monthly trend analysis

### 5.2 Incident Response

**Excessive Bot Traffic (DDoS):**
1. Identify traffic source and pattern
2. Apply immediate rate limiting or blocking
3. Engage CDN/WAF provider for mitigation
4. Document incident and response
5. Update rules to prevent recurrence

**False Positive (Legitimate User Blocked):**
1. User reports issue via contact form
2. Review access logs for user's IP/pattern
3. Add temporary exemption if legitimate
4. Adjust rules to prevent similar false positives
5. Follow up with user within 1 business day

**New Malicious Pattern:**
1. Identify pattern in logs
2. Create WAF rule or user-agent block
3. Test rule in monitoring mode (1 week)
4. Deploy to production if effective
5. Document in change log

---

## 6. Public Communication

### 6.1 Documentation Location

Bot policies are published at:
- robots.txt: [agency].gov/robots.txt
- Full policy: [agency].gov/bot-policy (this document, public version)
- Contact information: [agency].gov/bot-policy/contact

### 6.2 Updates and Changes

When this policy changes:
- Update effective date and version number
- Publish changelog at [agency].gov/bot-policy/changelog
- Provide 30-day notice for significant restrictions (when feasible)
- No advance notice for security-driven emergency blocks

### 6.3 Bot Operator Guidance

We encourage bot operators to:
- Identify themselves with descriptive user-agent strings
- Include contact information or website in user-agent
- Respect robots.txt directives
- Implement reasonable rate limiting
- Respond to technical contact requests within 48 hours

Example good user-agent:
```
MyBot/1.0 (+https://mycompany.com/bot-info; bot@mycompany.com)
```

---

## 7. Exception Request Process

### 7.1 Who Can Request Exceptions

- Academic researchers studying government data
- Journalists investigating matters of public interest
- Non-profit organizations working on civic projects
- Government partner agencies
- Contractors with approved projects

### 7.2 Request Requirements

Submit requests to: [botaccess@agency.gov]

Include:
1. Requester identity and affiliation
2. Purpose of elevated access
3. Specific data or pages needed
4. Expected crawl volume and duration
5. Technical details (user-agent, IPs)
6. How results will be used and published

### 7.3 Review Process

1. **Initial Review (5 business days):** IT Security reviews for feasibility
2. **Approval Authority:** [Web Operations Manager / CTO / designated authority]
3. **Approval Criteria:**
   - Legitimate purpose aligned with agency mission
   - Reasonable technical requirements
   - Acceptable security risk
   - Compliance with applicable laws and policies
4. **Response:** Approve, deny (with explanation), or request modifications
5. **If Approved:** Provide:
   - Approved time period (max 90 days)
   - Rate limits for granted access
   - IP whitelist or authentication token
   - Contact for technical issues
   - Requirement to cite/attribute data source

### 7.4 Ongoing Access

- Granted exceptions require 30-day renewal if needed beyond initial period
- Access can be revoked immediately for policy violations
- Requesters must report completion and provide results summary

---

## 8. Compliance and Enforcement

### 8.1 Policy Violations

Violations include:
- Circumventing technical controls
- Misrepresenting bot identity
- Exceeding granted rate limits
- Accessing protected endpoints without authorization
- Causing service disruption

### 8.2 Enforcement Actions

**Progressive response:**
1. First offense (unintentional): Warning and guidance
2. Repeated violations: Temporary block (24 hours to 30 days)
3. Malicious violations: Permanent block + report to authorities if warranted

### 8.3 Appeals

Blocked parties may appeal to [botappeals@agency.gov]:
- Explain circumstances
- Demonstrate good faith
- Propose remediation
- Response within 10 business days

---

## 9. Roles and Responsibilities

### 9.1 Document Owner
**[IT Security Manager / Web Operations Lead]**
- Maintains this policy
- Coordinates reviews and updates
- Approves exception requests

### 9.2 Implementation Team
**[Web Operations / DevOps Team]**
- Implements technical controls
- Monitors bot traffic and performance
- Responds to incidents
- Updates WAF rules and configurations

### 9.3 Security Team
- Reviews security implications
- Manages threat intelligence feeds
- Investigates malicious activity
- Coordinates incident response

### 9.4 Legal/Compliance
- Ensures policy meets legal requirements
- Reviews exception requests for legal issues
- Advises on FOIA and transparency obligations

---

## 10. Review and Maintenance

### 10.1 Review Schedule

- **Monthly:** Operational metrics review
- **Quarterly:** Technical control effectiveness assessment
- **Semi-annually:** Full policy review and updates
- **As needed:** Emergency reviews for new threats or major incidents

### 10.2 Update Triggers

Policy should be reviewed when:
- Significant security incidents occur
- Changes to legal/regulatory requirements
- Major website infrastructure changes
- User feedback indicates problems

### 10.3 Changelog

All substantive changes documented at [agency].gov/bot-policy/changelog

---

## 11. Contact Information

### 11.1 Technical Issues
**Email:** [webmaster@agency.gov]  
**Response Time:** 2 business days

### 11.2 Exception Requests
**Email:** [botaccess@agency.gov]  
**Response Time:** 5 business days for initial review

### 11.3 Appeals
**Email:** [botappeals@agency.gov]  
**Response Time:** 10 business days

### 11.4 Security Concerns
**Email:** [security@agency.gov]  
**Phone:** [Security Hotline]  
**Response Time:** 24 hours for critical issues

---

## Appendix A: Example robots.txt

```
# [Agency Name] robots.txt
# Last updated: [Date]
# Full policy: https://[agency].gov/bot-policy

User-agent: *
Disallow: /admin/
Disallow: /login/
Disallow: /auth/
Disallow: /search/
Disallow: /forms/
Disallow: /api/
Disallow: /internal/
Disallow: /*.pdf$email=

# Major search engines - full access
User-agent: Googlebot
Allow: /
Crawl-delay: 1

User-agent: Bingbot
Allow: /
Crawl-delay: 1

User-agent: DuckDuckBot
Allow: /
Crawl-delay: 1

# AI training crawlers - rate limited
User-agent: GPTBot
Allow: /
Crawl-delay: 10

User-agent: Google-Extended
Allow: /
Crawl-delay: 10

User-agent: CCBot
Allow: /
Crawl-delay: 10

User-agent: Claude-Web
Allow: /
Crawl-delay: 10

User-agent: Omgilibot
Allow: /
Crawl-delay: 10

# Archival
User-agent: ia_archiver
Allow: /
Crawl-delay: 2

# Aggressive crawlers - blocked
User-agent: AhrefsBot
Disallow: /

User-agent: SemrushBot
Disallow: /

# Sitemap
Sitemap: https://[agency].gov/sitemap.xml
```

---

## Appendix C: Glossary

**Bot/Crawler/Spider:** Automated software that systematically browses websites

**User-Agent:** HTTP header identifying the software making a request

**robots.txt:** Standard file that provides crawling guidelines to bots

**WAF (Web Application Firewall):** Security system that filters malicious web traffic

**Rate Limiting:** Restricting the number of requests from a source over time

**Reverse DNS Lookup:** Finding the hostname associated with an IP address

**CAPTCHA:** Challenge-response test to distinguish humans from bots

**Whitelist:** List of explicitly allowed entities

**Blacklist:** List of explicitly blocked entities

**Crawl-delay:** Specified wait time between requests for a bot

**HTTP 403:** Forbidden status code (access denied)

**HTTP 429:** Too Many Requests status code (rate limit exceeded)

---

**Document Control:**
- **Classification:** Public
- **Distribution:** Unlimited
- **Approval:** [Name, Title, Date]
- **Next Review Date:** [Date]
