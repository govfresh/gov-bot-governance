# Bot Governance Policy Implementation Checklist
## [Agency Name] - Technical Deployment Guide

**Document Version:** 1.0  
**Target Completion Date:** [Date]  
**Project Lead:** [Name]  
**Last Updated:** [Date]

---

## Overview

This checklist guides the technical implementation of the Bot Governance Policy. Each section includes prerequisites, tasks, responsible parties, and verification steps.

**Implementation Phases:**
1. **Discovery & Planning** (Week 1-2)
2. **Infrastructure Setup** (Week 3-4)
3. **Configuration & Testing** (Week 5-6)
4. **Deployment & Monitoring** (Week 7-8)
5. **Documentation & Training** (Week 9-10)

---

## Phase 1: Discovery & Planning

### 1.1 Infrastructure Assessment

**Responsible:** Infrastructure Team  
**Timeline:** Week 1

- [ ] **Document current web server platform**
  - [ ] Identify web server type: □ Apache □ Nginx □ IIS □ Other: ___________
  - [ ] Document version number: ___________
  - [ ] Note configuration file locations: ___________
  - [ ] Identify who has admin access and deployment authority

- [ ] **Document CDN/proxy setup**
  - [ ] Current CDN: □ Cloudflare □ Akamai □ AWS CloudFront □ Azure CDN □ None □ Other: ___________
  - [ ] How real IPs are preserved: □ X-Forwarded-For □ CF-Connecting-IP □ True-Client-IP □ Other: ___________
  - [ ] SSL/TLS termination point: □ CDN □ Load Balancer □ Web Server
  - [ ] DDoS protection currently in place: ___________

- [ ] **Identify load balancer configuration**
  - [ ] Load balancer type: □ AWS ELB □ Nginx □ HAProxy □ Hardware □ None □ Other: ___________
  - [ ] Session persistence settings: ___________
  - [ ] Health check configuration: ___________

- [ ] **Map hosting environment**
  - [ ] Hosting: □ AWS □ Azure □ GCP □ On-premise □ Hybrid □ Other: ___________
  - [ ] Number of web servers: ___________
  - [ ] Auto-scaling enabled: □ Yes □ No
  - [ ] Regions/availability zones: ___________

### 1.2 Traffic Baseline Analysis

**Responsible:** Web Operations Team  
**Timeline:** Week 1-2

- [ ] **Collect historical traffic data (last 90 days minimum)**
  - [ ] Total requests per day (average): ___________
  - [ ] Peak requests per minute: ___________
  - [ ] Unique visitors per day (average): ___________
  - [ ] Bot traffic percentage (if known): ___________%

- [ ] **Analyze current bot traffic**
  - [ ] Export top 50 user-agents from access logs
  - [ ] Categorize each user-agent: □ Search Engine □ AI Crawler □ Social Media □ Unknown □ Malicious
  - [ ] Calculate requests per bot type
  - [ ] Identify top 10 most active bots by volume
  - [ ] Document any current bot-related issues (slowdowns, abuse, etc.)

- [ ] **Identify traffic patterns**
  - [ ] Peak traffic hours: ___________
  - [ ] Geographic distribution (top 5 countries): ___________
  - [ ] Most-accessed pages/endpoints: ___________
  - [ ] Current average page load time: ___________ seconds

- [ ] **Review current access logs**
  - [ ] Log format includes: □ IP □ User-Agent □ Referrer □ Response Time □ Status Code
  - [ ] Log retention period: ___________ days
  - [ ] Log storage location: ___________
  - [ ] Log analysis tools available: ___________

### 1.3 Security Assessment

**Responsible:** Security Team  
**Timeline:** Week 1-2

- [ ] **Review existing security controls**
  - [ ] Current WAF: □ Yes (Type: ___________) □ No
  - [ ] IP blocking capability: □ Yes □ No
  - [ ] Rate limiting capability: □ Yes □ No
  - [ ] CAPTCHA solution: □ Yes (Type: ___________) □ No
  - [ ] Intrusion detection/prevention: □ Yes □ No

- [ ] **Identify security gaps**
  - [ ] Can we detect/block malicious user-agents? □ Yes □ No
  - [ ] Can we verify bot identities (reverse DNS)? □ Yes □ No
  - [ ] Can we rate limit by IP? □ Yes □ No
  - [ ] Can we rate limit by endpoint? □ Yes □ No
  - [ ] Can we challenge suspicious traffic? □ Yes □ No

- [ ] **Document recent security incidents**
  - [ ] Bot-related attacks in last 12 months: ___________
  - [ ] DDoS incidents: ___________
  - [ ] Scraping/data harvesting incidents: ___________
  - [ ] Form spam volume: ___________

### 1.4 Budget and Resource Planning

**Responsible:** Project Lead + IT Management  
**Timeline:** Week 2

- [ ] **Estimate costs for required services**
  - [ ] WAF service (if needed): $__________ /month
  - [ ] IP reputation service: $__________ /month
  - [ ] CAPTCHA service: $__________ /month
  - [ ] Additional CDN bandwidth: $__________ /month
  - [ ] Monitoring/alerting tools: $__________ /month
  - [ ] **Total estimated monthly cost:** $__________

- [ ] **Identify required personnel**
  - [ ] Implementation engineer(s): ___________ (hours)
  - [ ] Security analyst: ___________ (hours)
  - [ ] Network administrator: ___________ (hours)
  - [ ] Testing/QA resources: ___________ (hours)

- [ ] **Obtain budget approval**
  - [ ] Submit cost estimate to: ___________
  - [ ] Approval received: □ Yes □ No
  - [ ] Purchase orders created: □ Yes □ No

### 1.5 Risk Assessment and Mitigation

**Responsible:** Security Team + Project Lead  
**Timeline:** Week 2

- [ ] **Identify implementation risks**
  - [ ] Risk: Blocking legitimate users
    - Mitigation: ___________
  - [ ] Risk: Performance degradation
    - Mitigation: ___________
  - [ ] Risk: False positives in bot detection
    - Mitigation: ___________
  - [ ] Risk: Configuration errors causing outages
    - Mitigation: ___________
  - [ ] Risk: Interference with accessibility
    - Mitigation: ___________

- [ ] **Create rollback plan**
  - [ ] Document current configuration (backup)
  - [ ] Define rollback trigger conditions
  - [ ] Identify rollback authority and process
  - [ ] Test rollback procedure in staging

- [ ] **Establish success metrics**
  - [ ] Target bot traffic percentage: ___________%
  - [ ] Maximum acceptable false positive rate: ___________%
  - [ ] User page load time target: ___________ seconds
  - [ ] Uptime target: ___________%

---

## Phase 2: Infrastructure Setup

### 2.1 WAF Selection and Deployment

**Responsible:** Infrastructure Team + Security Team  
**Timeline:** Week 3

- [ ] **Select WAF solution** (if not already in place)
  - [ ] Evaluate options based on:
    - [ ] Budget: $__________
    - [ ] Feature requirements (bot management, rate limiting, etc.)
    - [ ] Integration with existing infrastructure
    - [ ] Support and documentation quality
  - [ ] **Selected WAF:** ___________
  - [ ] Obtain approval for purchase/deployment

- [ ] **Deploy/configure WAF**
  - [ ] Create WAF account and set up billing
  - [ ] Add website domain(s) to WAF
  - [ ] Configure DNS to route through WAF (if applicable)
  - [ ] Verify traffic is flowing through WAF
  - [ ] Enable SSL/TLS
  - [ ] Set initial mode: □ Monitor Only □ Challenge □ Block
  - [ ] Configure logging and integrate with SIEM (if applicable)

- [ ] **Configure basic WAF rules**
  - [ ] Enable OWASP Core Rule Set (if available)
  - [ ] Enable DDoS protection
  - [ ] Set up basic rate limiting (conservative initially)
  - [ ] Enable bot detection features
  - [ ] Configure IP reputation integration (if available)

### 2.2 IP Reputation Service Setup

**Responsible:** Security Team  
**Timeline:** Week 3

- [ ] **Select IP reputation service(s)**
  - Option 1: **Spamhaus**
    - [ ] Sign up for appropriate tier: □ Free □ Paid
    - [ ] Download/configure blocklist feeds
    - [ ] Set up automated updates
  - Option 2: **AbuseIPDB**
    - [ ] Create account and get API key
    - [ ] Set confidence score threshold: ___________%
    - [ ] Configure rate limits for API calls
  - Option 3: **Built into WAF**
    - [ ] Enable threat intelligence features
    - [ ] Configure reputation score thresholds
  - Option 4: **Other:** ___________

- [ ] **Integrate reputation data**
  - [ ] Web server integration: □ Complete □ N/A
  - [ ] WAF integration: □ Complete □ N/A
  - [ ] Load balancer integration: □ Complete □ N/A

- [ ] **Configure update frequency**
  - [ ] Spamhaus lists: □ Hourly □ Daily
  - [ ] AbuseIPDB queries: □ Real-time □ Cached (frequency: _________)
  - [ ] Set up automated list refresh scripts/cron jobs

- [ ] **Define blocking/challenge thresholds**
  - [ ] High-risk IPs (confidence >90%): □ Block □ Challenge
  - [ ] Medium-risk IPs (confidence 70-90%): □ Challenge □ Monitor
  - [ ] Low-risk IPs (confidence <70%): □ Monitor □ Allow
  - [ ] Document threshold rationale: ___________

### 2.3 CAPTCHA Service Setup

**Responsible:** Development Team  
**Timeline:** Week 3-4

- [ ] **Select CAPTCHA service**
  - [ ] Evaluate options:
    - [ ] Google reCAPTCHA v2 (checkbox)
    - [ ] Google reCAPTCHA v3 (invisible scoring)
    - [ ] hCaptcha (privacy-focused)
    - [ ] Custom solution
  - [ ] **Selected service:** ___________
  - [ ] Consider accessibility (audio alternatives, keyboard navigation)

- [ ] **Set up CAPTCHA account**
  - [ ] Create account and register domain(s)
  - [ ] Obtain site key: ___________
  - [ ] Obtain secret key: ___________ (store securely)
  - [ ] Configure CAPTCHA difficulty/threshold
  - [ ] Test CAPTCHA display and validation

- [ ] **Integrate CAPTCHA on forms**
  - [ ] Contact form: □ Complete
  - [ ] Search form (if protected): □ Complete □ N/A
  - [ ] Public comment submission: □ Complete □ N/A
  - [ ] FOIA request form: □ Complete □ N/A
  - [ ] Newsletter signup: □ Complete □ N/A
  - [ ] Other forms: ___________

- [ ] **Configure CAPTCHA triggers**
  - [ ] Trigger on: □ All form submissions □ Suspicious behavior only
  - [ ] Define "suspicious behavior": ___________
  - [ ] Set up server-side validation
  - [ ] Implement error handling for failed CAPTCHAs

### 2.4 Monitoring and Alerting Setup

**Responsible:** Operations Team  
**Timeline:** Week 4

- [ ] **Configure monitoring tools**
  - [ ] Tool selection: ___________
  - [ ] Install agents/configure data collection
  - [ ] Set up dashboards for:
    - [ ] Total request volume
    - [ ] Bot traffic percentage
    - [ ] Blocked requests by category
    - [ ] Response times
    - [ ] Error rates (4xx, 5xx)
    - [ ] WAF rule triggers

- [ ] **Set up alerting thresholds**
  - [ ] Alert when blocked requests > __________ per hour
  - [ ] Alert when bot traffic > __________% of total
  - [ ] Alert when response time > __________ seconds (95th percentile)
  - [ ] Alert when error rate > __________%
  - [ ] Alert when false positive reports received

- [ ] **Configure alert destinations**
  - [ ] Email: ___________
  - [ ] SMS/phone: ___________
  - [ ] Slack/Teams channel: ___________
  - [ ] PagerDuty/incident management: ___________

- [ ] **Create monitoring runbook**
  - [ ] Document normal traffic patterns
  - [ ] Define alert response procedures
  - [ ] Assign on-call responsibilities
  - [ ] Create escalation paths

---

## Phase 3: Configuration & Testing

### 3.1 Create and Deploy robots.txt

**Responsible:** Development Team  
**Timeline:** Week 5

- [ ] **Create robots.txt file**
  - [ ] Copy template from Appendix A of policy document
  - [ ] Customize for agency-specific paths
  - [ ] Add all endpoints to protect:
    - [ ] /admin/
    - [ ] /login/
    - [ ] /search/
    - [ ] /forms/
    - [ ] /api/
    - [ ] Other: ___________

- [ ] **Define crawl-delay values**
  - [ ] Search engines (Googlebot, Bingbot): ___________
  - [ ] AI crawlers (GPTBot, CCBot, etc.): ___________
  - [ ] Archival bots: ___________
  - [ ] Social media bots: ___________

- [ ] **Test robots.txt**
  - [ ] Use Google Search Console robots.txt tester
  - [ ] Validate syntax: https://www.google.com/webmasters/tools/robots-testing-tool
  - [ ] Verify disallow rules work correctly
  - [ ] Check for unintended blocks

- [ ] **Deploy robots.txt**
  - [ ] Upload to web root: yourdomain.gov/robots.txt
  - [ ] Verify accessible via browser
  - [ ] Submit to Google Search Console
  - [ ] Submit to Bing Webmaster Tools

- [ ] **Create XML sitemap** (if not exists)
  - [ ] Generate sitemap with all public pages
  - [ ] Reference in robots.txt
  - [ ] Submit to search engines

### 3.2 Configure User-Agent Filtering

**Responsible:** Infrastructure Team  
**Timeline:** Week 5

- [ ] **Create user-agent blocklist**
  - [ ] Start with common malicious agents:
    - [ ] sqlmap, nikto, nmap, masscan
    - [ ] AhrefsBot, SemrushBot (if blocking)
    - [ ] wget, curl (when generic)
    - [ ] HTTrack, WebCopier
    - [ ] Empty or missing user-agents
  - [ ] Add agency-specific bad actors from log analysis
  - [ ] Document reason for each block

- [ ] **Implement server-level blocking**
  
  **For Apache (.htaccess or httpd.conf):**
  ```apache
  # Block bad user-agents
  SetEnvIfNoCase User-Agent "badbot" bad_bot
  SetEnvIfNoCase User-Agent "scrapy" bad_bot
  SetEnvIfNoCase User-Agent "sqlmap" bad_bot
  SetEnvIfNoCase User-Agent "nikto" bad_bot
  SetEnvIfNoCase User-Agent "^$" bad_bot
  
  <Limit GET POST HEAD>
    Order Allow,Deny
    Allow from all
    Deny from env=bad_bot
  </Limit>
  ```
  - [ ] Create configuration file
  - [ ] Test in staging
  - [ ] Deploy to production
  - [ ] Verify blocks in access logs
  
  **For Nginx (nginx.conf or site config):**
  ```nginx
  # Block bad user-agents
  if ($http_user_agent ~* (badbot|scrapy|sqlmap|nikto)) {
    return 403;
  }
  
  # Block empty user-agents
  if ($http_user_agent = "") {
    return 403;
  }
  ```
  - [ ] Create configuration snippet
  - [ ] Test syntax: `nginx -t`
  - [ ] Test in staging
  - [ ] Deploy to production
  - [ ] Reload: `nginx -s reload`
  - [ ] Verify blocks in access logs

- [ ] **Implement bot verification for whitelisted bots**
  
  **Create verification script (Python example):**
  ```python
  import socket
  
  def verify_bot(ip, claimed_bot):
      """Verify bot identity via reverse DNS"""
      valid_domains = {
          'googlebot': ['.googlebot.com', '.google.com'],
          'bingbot': ['.search.msn.com'],
          'duckduckbot': ['.duckduckgo.com']
      }
      
      try:
          hostname = socket.gethostbyaddr(ip)[0]
          valid = any(hostname.endswith(domain) 
                     for domain in valid_domains.get(claimed_bot, []))
          
          if valid:
              forward_ip = socket.gethostbyname(hostname)
              return forward_ip == ip
      except:
          return False
      
      return False
  ```
  - [ ] Implement verification script
  - [ ] Integrate with web server or application
  - [ ] Cache verification results (TTL: _______ minutes)
  - [ ] Log verification failures
  - [ ] Test with known good bots

### 3.3 Configure Rate Limiting

**Responsible:** Infrastructure Team  
**Timeline:** Week 5

- [ ] **Define rate limit tiers**
  
  **Global limits (per IP):**
  - [ ] Public pages: __________ requests/minute
  - [ ] Search endpoints: __________ requests/minute
  - [ ] API endpoints: __________ requests/minute (or per-token)
  - [ ] Download endpoints: __________ requests/minute
  - [ ] Form submissions: __________ submissions/hour
  
  **Bot-specific limits:**
  - [ ] Whitelisted search engines: __________ requests/second
  - [ ] AI training crawlers: 1 request/__________ seconds
  - [ ] Unidentified bots: __________ requests/minute
  - [ ] After rate limit exceeded: □ HTTP 429 □ CAPTCHA challenge □ Block

- [ ] **Implement rate limiting**
  
  **WAF-based (preferred):**
  - [ ] Configure rate limiting rules in WAF dashboard
  - [ ] Set up per-IP limits
  - [ ] Set up per-endpoint limits
  - [ ] Configure response actions (429, challenge, block)
  - [ ] Test limits with load testing tool
  
  **Nginx-based (if not using WAF):**
  ```nginx
  # Define rate limit zones
  limit_req_zone $binary_remote_addr zone=general:10m rate=60r/m;
  limit_req_zone $binary_remote_addr zone=search:10m rate=10r/m;
  limit_req_zone $binary_remote_addr zone=api:10m rate=30r/m;
  
  # Apply to locations
  location / {
    limit_req zone=general burst=20 nodelay;
  }
  
  location /search {
    limit_req zone=search burst=5;
  }
  
  location /api {
    limit_req zone=api burst=10;
  }
  ```
  - [ ] Configure rate limit zones
  - [ ] Set burst allowances
  - [ ] Test configuration
  - [ ] Deploy to production
  
  **Apache-based (mod_ratelimit or mod_evasive):**
  - [ ] Install mod_evasive (if not installed)
  - [ ] Configure limits in httpd.conf
  - [ ] Set whitelist for monitoring IPs
  - [ ] Test and deploy

- [ ] **Configure exemptions**
  - [ ] Whitelist internal monitoring IPs: ___________
  - [ ] Whitelist partner IPs: ___________
  - [ ] Whitelist authenticated API tokens
  - [ ] Document all exemptions and rationale

### 3.4 Configure WAF Bot Management Rules

**Responsible:** Security Team  
**Timeline:** Week 5-6

- [ ] **Enable bot detection features**
  - [ ] Bot score/confidence scoring: □ Enabled
  - [ ] JavaScript challenge: □ Enabled
  - [ ] CAPTCHA challenge: □ Enabled
  - [ ] Machine learning bot detection: □ Enabled (if available)

- [ ] **Configure bot score thresholds** (if using scored system like Cloudflare)
  - [ ] Score 0-20: □ Block □ Challenge
  - [ ] Score 21-40: □ Challenge □ Monitor
  - [ ] Score 41-60: □ Monitor □ Allow
  - [ ] Score 61-100: □ Allow
  - [ ] Adjust based on testing and false positive rate

- [ ] **Create custom WAF rules**
  
  **Example rules to create:**
  1. **Block known malicious user-agents:**
     - Condition: User-Agent contains "sqlmap" OR "nikto" OR "nmap"
     - Action: Block (403)
  
  2. **Challenge high-frequency visitors:**
     - Condition: More than X requests in Y seconds
     - Action: JavaScript challenge
  
  3. **Protect sensitive endpoints:**
     - Condition: Path starts with "/admin" OR "/login" OR "/api"
     - AND: Bot score < 50
     - Action: Block or CAPTCHA
  
  4. **Rate limit AI crawlers:**
     - Condition: User-Agent contains "GPTBot" OR "CCBot" OR "Claude-Web"
     - Action: Rate limit to 1 req/10 seconds
  
  5. **Block empty user-agents:**
     - Condition: User-Agent is empty
     - Action: Block (403)
  
  - [ ] Rule 1: ___________  □ Created □ Tested □ Deployed
  - [ ] Rule 2: ___________  □ Created □ Tested □ Deployed
  - [ ] Rule 3: ___________  □ Created □ Tested □ Deployed
  - [ ] Rule 4: ___________  □ Created □ Tested □ Deployed
  - [ ] Rule 5: ___________  □ Created □ Tested □ Deployed

- [ ] **Configure rule actions**
  - [ ] Define escalation: Monitor → Challenge → Block
  - [ ] Set challenge duration/cookie lifetime
  - [ ] Configure custom block pages with helpful messages
  - [ ] Set up logging for all rule triggers

### 3.5 Testing in Staging Environment

**Responsible:** QA Team + Security Team  
**Timeline:** Week 6

- [ ] **Set up staging environment** (if not exists)
  - [ ] Mirror production configuration
  - [ ] Deploy all bot management rules
  - [ ] Configure same WAF rules
  - [ ] Enable detailed logging

- [ ] **Test legitimate bot access**
  - [ ] Simulate Googlebot requests (using verified IPs or tools)
  - [ ] Verify search engine bots are allowed
  - [ ] Test social media preview bots
  - [ ] Verify Archive.org bot access
  - [ ] Confirm rate limits work as expected for good bots

- [ ] **Test malicious bot blocking**
  - [ ] Test with common scraper user-agents
  - [ ] Test with empty user-agent
  - [ ] Test rapid-fire requests (exceed rate limits)
  - [ ] Test SQL injection patterns
  - [ ] Test form submission spam
  - [ ] Verify all blocks return appropriate error codes

- [ ] **Test CAPTCHA challenges**
  - [ ] Trigger CAPTCHA by suspicious behavior
  - [ ] Verify CAPTCHA displays correctly
  - [ ] Complete CAPTCHA successfully
  - [ ] Verify access granted after successful completion
  - [ ] Test CAPTCHA accessibility (audio alternative, keyboard nav)

- [ ] **Test false positive scenarios**
  - [ ] Simulate legitimate user on slow connection
  - [ ] Test from corporate NAT/shared IP
  - [ ] Test from mobile network
  - [ ] Test from VPN
  - [ ] Test rapid but normal navigation (clicking through site)
  - [ ] Document any false positives and adjust rules

- [ ] **Load testing**
  - [ ] Use tool: □ Apache JMeter □ LoadRunner □ k6 □ Other: ___________
  - [ ] Simulate normal traffic patterns
  - [ ] Simulate bot traffic at expected levels
  - [ ] Simulate attack scenarios (high volume)
  - [ ] Measure performance impact:
    - Response time with bot controls: __________ ms
    - Response time without: __________ ms
    - Server CPU/memory impact: __________
  - [ ] Verify rate limits enforce properly under load
  - [ ] Verify WAF handles peak traffic

- [ ] **Create test report**
  - [ ] Document all test scenarios and results
  - [ ] List any issues found and resolutions
  - [ ] Note performance impacts
  - [ ] Get sign-off from: ___________

---

## Phase 4: Deployment & Monitoring

### 4.1 Production Deployment

**Responsible:** Infrastructure Team + Project Lead  
**Timeline:** Week 7

- [ ] **Pre-deployment checklist**
  - [ ] All staging tests passed: □ Yes
  - [ ] Rollback plan documented: □ Yes
  - [ ] Stakeholders notified of deployment: □ Yes
  - [ ] Deployment window scheduled: ___________
  - [ ] On-call personnel assigned: ___________
  - [ ] Monitoring dashboards ready: □ Yes

- [ ] **Deploy robots.txt**
  - [ ] Upload to production web root
  - [ ] Verify accessible: https://yourdomain.gov/robots.txt
  - [ ] Time deployed: ___________
  - [ ] No errors: □ Confirmed

- [ ] **Deploy user-agent filtering rules**
  - [ ] Deploy web server configuration changes
  - [ ] Method: □ Graceful reload □ Rolling deployment □ Blue-green
  - [ ] Verify syntax before reload
  - [ ] Reload web servers
  - [ ] Time deployed: ___________
  - [ ] Monitor error logs for 15 minutes
  - [ ] No errors: □ Confirmed

- [ ] **Deploy rate limiting rules**
  - [ ] Start with monitoring mode (no enforcement): □ Yes
  - [ ] Deploy rate limiting configuration
  - [ ] Time deployed: ___________
  - [ ] Monitor for 24 hours in monitoring mode
  - [ ] Review rate limit triggers and adjust if needed
  - [ ] Enable enforcement mode
  - [ ] Time enforcement enabled: ___________

- [ ] **Activate WAF bot management rules**
  - [ ] Enable rules one at a time or in groups
  - [ ] Start with challenge mode before blocking
  - [ ] Rule group 1 deployed: ___________
  - [ ] Monitor for 2 hours, review impact
  - [ ] Rule group 2 deployed: ___________
  - [ ] Monitor for 2 hours, review impact
  - [ ] All rules deployed: ___________
  - [ ] Escalate to blocking mode: □ Yes, Date: ___________

- [ ] **Enable IP reputation blocking**
  - [ ] Start with high-confidence blocks only (>90%)
  - [ ] Time deployed: ___________
  - [ ] Monitor for 24 hours
  - [ ] Expand to medium-confidence (>70%) if no issues
  - [ ] Time expanded: ___________

- [ ] **Deploy CAPTCHA on forms**
  - [ ] Deploy form code changes
  - [ ] Test each form in production
  - [ ] Monitor form submission success rates
  - [ ] Forms protected: ___________

### 4.2 Initial Monitoring Period

**Responsible:** Operations Team  
**Timeline:** Week 7-8

- [ ] **Monitor key metrics continuously (first 48 hours)**
  - [ ] Total request volume: ___________ (baseline: ___________)
  - [ ] Bot traffic percentage: __________% (baseline: ___________)
  - [ ] Blocked requests: ___________
  - [ ] Challenged requests: ___________
  - [ ] Response time p95: ___________ (baseline: ___________)
  - [ ] Error rate: __________% (baseline: ___________)
  - [ ] False positive reports: ___________

- [ ] **Review bot traffic changes**
  - [ ] Good bots still crawling: □ Yes
  - [ ] Malicious bot traffic reduced: □ Yes, by ___________%
  - [ ] AI crawler traffic: □ Within limits □ Blocked □ Issue: ___________
  - [ ] Search engine indexing: □ Normal □ Issue: ___________

- [ ] **Address false positives immediately**
  - [ ] Process for false positive reports:
    1. User reports via: ___________
    2. Review access logs for user IP/pattern
    3. Identify triggering rule
    4. Add exemption if legitimate
    5. Reply to user within: ___________ hours
  - [ ] False positives found: ___________
  - [ ] Resolutions applied: ___________

- [ ] **Daily review meetings (first week)**
  - [ ] Day 1 review: □ Complete, Date: ___________
  - [ ] Day 2 review: □ Complete, Date: ___________
  - [ ] Day 3 review: □ Complete, Date: ___________
  - [ ] Day 4 review: □ Complete, Date: ___________
  - [ ] Day 5 review: □ Complete, Date: ___________
  - [ ] Issues identified: ___________
  - [ ] Adjustments made: ___________

- [ ] **Tune rules based on real traffic**
  - [ ] Adjust rate limits if needed: ___________
  - [ ] Refine user-agent blocks: ___________
  - [ ] Update bot score thresholds: ___________
  - [ ] Add new exemptions: ___________
  - [ ] Document all changes in changelog

### 4.3 Success Validation

**Responsible:** Project Lead  
**Timeline:** End of Week 8

- [ ] **Measure against success criteria**
  - [ ] Bot traffic percentage: __________% (Target: ___________)
  - [ ] False positive rate: __________% (Target: <0.1%)
  - [ ] Page load time: __________ sec (Target: ___________)
  - [ ] Uptime: __________% (Target: ___________)
  - [ ] Search engine indexing: □ Normal □ Improved □ Issue
  - [ ] Security incidents: □ Reduced □ Same □ Increased

- [ ] **Collect feedback**
  - [ ] User complaints received: ___________
  - [ ] Ops team feedback: ___________
  - [ ] Security team feedback: ___________
  - [ ] Issues to address: ___________

- [ ] **Prepare success report**
  - [ ] Document baseline vs. current metrics
  - [ ] Highlight improvements (bot traffic reduction, security, etc.)
  - [ ] Note any ongoing issues and remediation plans
  - [ ] Present to stakeholders: Date: ___________

---

## Phase 5: Documentation & Training

### 5.1 Documentation

**Responsible:** Project Lead + Technical Writers  
**Timeline:** Week 9

- [ ] **Create technical documentation**
  - [ ] Document all WAF rules and rationale
  - [ ] Document rate limiting configuration
  - [ ] Document user-agent filtering rules
  - [ ] Document IP reputation integration
  - [ ] Document CAPTCHA implementation
  - [ ] Document verification scripts
  - [ ] Create network/architecture diagram showing bot controls

- [ ] **Create operational runbooks**
  - [ ] "Responding to Bot Attacks" playbook
  - [ ] "Handling False Positive Reports" playbook
  - [ ] "Granting Bot Access Exceptions" playbook
  - [ ] "Emergency Rollback" procedure
  - [ ] "Routine Maintenance" procedures

- [ ] **Update public-facing documentation**
  - [ ] Publish bot policy at: yourdomain.gov/bot-policy
  - [ ] Create "Bot Access Request" page
  - [ ] Update contact information pages
  - [ ] Create FAQ for bot operators

- [ ] **Create changelog**
  - [ ] Document initial deployment date and configuration
  - [ ] Template for future rule changes
  - [ ] Publish at: yourdomain.gov/bot-policy/changelog
  - [ ] Subscribe stakeholders to updates

### 5.2 Training

**Responsible:** Project Lead + Training Coordinator  
**Timeline:** Week 9-10

- [ ] **Train operations team**
  - [ ] Session 1: Overview of bot governance policy
    - Date: ___________
    - Attendees: ___________
  - [ ] Session 2: Monitoring dashboards and alerts
    - Date: ___________
    - Attendees: ___________
  - [ ] Session 3: Responding to incidents
    - Date: ___________
    - Attendees: ___________
  - [ ] Session 4: Handling false positives
    - Date: ___________
    - Attendees: ___________
  - [ ] Hands-on exercises with monitoring tools
  - [ ] Practice incident response scenarios

- [ ] **Train help desk/support staff**
  - [ ] Overview of bot controls and why they exist
  - [ ] How to identify bot-related user complaints
  - [ ] Escalation procedures for false positives
  - [ ] Template responses for common issues
  - [ ] Training session date: ___________

- [ ] **Train security team**
  - [ ] Deep dive on WAF rules and capabilities
  - [ ] IP reputation service usage
  - [ ] Bot verification procedures
  - [ ] Threat intelligence integration
  - [ ] Training session date: ___________

- [ ] **Create training materials**
  - [ ] PowerPoint/slides
  - [ ] Recorded demo videos
  - [ ] Quick reference cards
  - [ ] Decision trees for common scenarios

### 5.3 Knowledge Transfer

**Responsible:** Project Lead  
**Timeline:** Week 10

- [ ] **Document tribal knowledge**
  - [ ] List of known good/bad actors
  - [ ] Common false positive scenarios
  - [ ] Tips for tuning rules
  - [ ] Lessons learned during implementation

- [ ] **Create handoff documentation**
  - [ ] Contact list for escalations
  - [ ] Access credentials and locations (in secure vault)
  - [ ] Vendor support contacts
  - [ ] Third-party service account details

- [ ] **Assign ongoing ownership**
  - [ ] Primary owner: ___________
  - [ ] Backup owner: ___________
  - [ ] On-call rotation: ___________

---

## Phase 6: Ongoing Operations

### 6.1 Regular Maintenance Tasks

**Responsible:** Operations Team  
**Frequency:** Ongoing

- [ ] **Daily tasks**
  - [ ] Review monitoring dashboards
  - [ ] Check for alerts
  - [ ] Review false positive reports
  - [ ] Verify search engine crawling is normal

- [ ] **Weekly tasks**
  - [ ] Review bot traffic trends
  - [ ] Analyze blocked requests by category
  - [ ] Check for new unknown bots in logs
  - [ ] Update IP reputation blocklists (if manual)
  - [ ] Review and respond to access requests

- [ ] **Monthly tasks**
  - [ ] Review and analyze metrics vs. baselines
  - [ ] Generate monthly report
  - [ ] Review and tune rate limits
  - [ ] Check for new bot user-agents to block/allow
  - [ ] Review WAF rule effectiveness
  - [ ] Update documentation as needed

- [ ] **Quarterly tasks**
  - [ ] Full policy review
  - [ ] Evaluate new threats and adjust rules
  - [ ] Review exception requests and renewals
  - [ ] Conduct tabletop exercise for incident response
  - [ ] Review and update training materials

- [ ] **Semi-annual tasks**
  - [ ] Comprehensive policy review and updates
  - [ ] Stakeholder review meeting
  - [ ] Evaluate new tools/services
  - [ ] Audit access controls and exemptions
  - [ ] Refresh training for teams

### 6.2 Exception Request Processing

**Responsible:** Designated Approver (from policy)  
**Timeline:** Ongoing, 5-day SLA

- [ ] **Create exception request form**
  - [ ] Online form at: yourdomain.gov/bot-policy/request-access
  - [ ] Required fields:
    - [ ] Requester name and affiliation
    - [ ] Contact information
    - [ ] Purpose of access
    - [ ] Data/pages needed
    - [ ] Expected volume and duration
    - [ ] User-agent string
    - [ ] Source IP addresses (if static)
    - [ ] How results will be used
  - [ ] Form submission triggers email to: ___________

- [ ] **Document review process**
  1. Acknowledge receipt within 1 business day
  2. Security team reviews for risks
  3. Legal team reviews for compliance (if needed)
  4. Approver makes decision within 5 business days
  5. If approved:
     - [ ] Add IP to whitelist or issue API token
     - [ ] Set expiration date (max 90 days)
     - [ ] Document in exception log
     - [ ] Notify requester with access details
  6. If denied:
     - [ ] Provide explanation
     - [ ] Suggest alternatives if applicable

- [ ] **Create exception tracking system**
  - [ ] Spreadsheet or database with:
    - [ ] Requester info
    - [ ] Approval date
    - [ ] Expiration date
    - [ ] Access type (IP whitelist, token, etc.)
    - [ ] Status (active, expired, revoked)
  - [ ] Set up automated expiration notifications

### 6.3 Incident Response Procedures

**Responsible:** Operations + Security Teams  
**Timeline:** As needed

- [ ] **Create incident severity levels**
  - [ ] **P1 - Critical:** Site down or major service disruption
    - Response time: 15 minutes
    - Escalation: Immediate
  - [ ] **P2 - High:** Significant bot attack, performance degradation
    - Response time: 1 hour
    - Escalation: 2 hours if unresolved
  - [ ] **P3 - Medium:** Elevated bot traffic, minor issues
    - Response time: 4 hours
    - Escalation: Next business day
  - [ ] **P4 - Low:** False positive reports, routine issues
    - Response time: 1 business day
    - Escalation: 3 business days

- [ ] **Document incident response steps**
  
  **Bot Attack Response:**
  1. Identify attack pattern (user-agents, IPs, endpoints targeted)
  2. Implement immediate mitigation:
     - [ ] Block attacking IPs
     - [ ] Enable aggressive WAF rules
     - [ ] Reduce rate limits temporarily
     - [ ] Enable CAPTCHA challenges site-wide (if needed)
  3. Monitor effectiveness
  4. Document incident details
  5. Post-mortem and rule updates
  
  **False Positive Response:**
  1. Receive report from user
  2. Gather details (IP, time, page, error message)
  3. Review access logs
  4. Identify triggering rule
  5. Validate user is legitimate
  6. Add exemption or tune rule
  7. Test fix
  8. Notify user of resolution
  9. Document for future prevention

- [ ] **Create escalation matrix**
  - [ ] Level 1: Operations team member
  - [ ] Level 2: Operations team lead
  - [ ] Level 3: Security team
  - [ ] Level 4: IT management
  - [ ] Contact info documented in runbook

### 6.4 Metrics and Reporting

**Responsible:** Operations Team  
**Frequency:** Monthly

- [ ] **Define KPIs to track**
  - [ ] Total requests per month
  - [ ] Bot traffic as % of total
  - [ ] Blocked requests by category:
    - [ ] Malicious bots
    - [ ] Excessive rate limits
    - [ ] Unknown/unverified bots
    - [ ] Geographic blocks (if applicable)
  - [ ] False positive reports received
  - [ ] False positive rate (% of legitimate traffic)
  - [ ] Average response time
  - [ ] Uptime percentage
  - [ ] Number of exception requests
  - [ ] Number of security incidents

- [ ] **Create monthly report template**
  - [ ] Executive summary
  - [ ] Key metrics with trends
  - [ ] Notable incidents and resolutions
  - [ ] Rule changes made
  - [ ] Exception requests processed
  - [ ] Recommendations for next month

- [ ] **Distribute reports to:**
  - [ ] IT Management
  - [ ] Security team
  - [ ] Web operations team
  - [ ] Other stakeholders: ___________

---

## Post-Implementation Review

### Completed Phases

**Phase 1: Discovery & Planning**
- Completion date: ___________
- Sign-off: ___________
- Issues encountered: ___________

**Phase 2: Infrastructure Setup**
- Completion date: ___________
- Sign-off: ___________
- Issues encountered: ___________

**Phase 3: Configuration & Testing**
- Completion date: ___________
- Sign-off: ___________
- Issues encountered: ___________

**Phase 4: Deployment & Monitoring**
- Completion date: ___________
- Sign-off: ___________
- Issues encountered: ___________

**Phase 5: Documentation & Training**
- Completion date: ___________
- Sign-off: ___________
- Issues encountered: ___________

### Overall Project Assessment

- [ ] **Project completed on time:** □ Yes □ No (Reason: ___________)
- [ ] **All objectives met:** □ Yes □ No (Outstanding: ___________)
- [ ] **Budget:** □ Under □ On target □ Over (By: ___________)
- [ ] **Success criteria achieved:** □ Yes □ Partial □ No

### Lessons Learned

**What went well:**
1. ___________
2. ___________
3. ___________

**What could be improved:**
1. ___________
2. ___________
3. ___________

**Recommendations for future projects:**
1. ___________
2. ___________
3. ___________

### Outstanding Items

- [ ] Item 1: ___________
  - Owner: ___________
  - Due date: ___________
  
- [ ] Item 2: ___________
  - Owner: ___________
  - Due date: ___________

---

## Appendix: Configuration Examples

### A. Sample Apache Configuration

```apache
# Bot Management Configuration
# File: /etc/httpd/conf.d/bot-management.conf

# Block malicious user-agents
SetEnvIfNoCase User-Agent "sqlmap" bad_bot
SetEnvIfNoCase User-Agent "nikto" bad_bot
SetEnvIfNoCase User-Agent "nmap" bad_bot
SetEnvIfNoCase User-Agent "masscan" bad_bot
SetEnvIfNoCase User-Agent "HTTrack" bad_bot
SetEnvIfNoCase User-Agent "scrapy" bad_bot
SetEnvIfNoCase User-Agent "^$" bad_bot

# Block empty referers on sensitive paths
SetEnvIf Referer "^$" empty_referer
SetEnvIf Request_URI "^/admin" admin_area
SetEnvIf Request_URI "^/login" admin_area

# Deny bad bots
<Limit GET POST HEAD>
  Order Allow,Deny
  Allow from all
  Deny from env=bad_bot
</Limit>

# Protect admin areas from empty referers
<If "%{ENV:admin_area} == '1' && %{ENV:empty_referer} == '1'">
  Require all denied
</If>

# Rate limiting with mod_ratelimit (for downloads)
<Location /downloads>
  SetOutputFilter RATE_LIMIT
  SetEnv rate-limit 400
</Location>
```

### B. Sample Nginx Configuration

```nginx
# Bot Management Configuration
# File: /etc/nginx/conf.d/bot-management.conf

# Define rate limit zones
limit_req_zone $binary_remote_addr zone=general:10m rate=60r/m;
limit_req_zone $binary_remote_addr zone=search:10m rate=10r/m;
limit_req_zone $binary_remote_addr zone=api:10m rate=30r/m;
limit_req_zone $binary_remote_addr zone=forms:10m rate=5r/h;

# Map for bot detection
map $http_user_agent $bad_bot {
    default 0;
    ~*sqlmap 1;
    ~*nikto 1;
    ~*nmap 1;
    ~*masscan 1;
    ~*HTTrack 1;
    ~*scrapy 1;
    "" 1;  # Empty user agent
}

# Server block
server {
    listen 80;
    server_name yourdomain.gov;
    
    # Block bad bots
    if ($bad_bot) {
        return 403;
    }
    
    # Apply rate limiting to general pages
    location / {
        limit_req zone=general burst=20 nodelay;
        limit_req_status 429;
        try_files $uri $uri/ =404;
    }
    
    # Protect search with strict rate limits
    location /search {
        limit_req zone=search burst=5;
        limit_req_status 429;
        proxy_pass http://backend;
    }
    
    # Protect API endpoints
    location /api {
        limit_req zone=api burst=10;
        limit_req_status 429;
        
        # Require authentication
        auth_request /auth-check;
        proxy_pass http://api-backend;
    }
    
    # Protect forms with very strict limits
    location /forms/submit {
        limit_req zone=forms;
        limit_req_status 429;
        proxy_pass http://backend;
    }
    
    # Block all bots from admin
    location /admin {
        if ($bad_bot) {
            return 403;
        }
        # Additional auth here
        proxy_pass http://backend;
    }
}
```

### C. Sample WAF Rules (Cloudflare Example)

```
Rule 1: Block Known Malicious User-Agents
Expression: (http.user_agent contains "sqlmap") or 
            (http.user_agent contains "nikto") or 
            (http.user_agent contains "nmap")
Action: Block

Rule 2: Challenge Empty User-Agents
Expression: (http.user_agent eq "")
Action: JS Challenge

Rule 3: Rate Limit AI Crawlers
Expression: (http.user_agent contains "GPTBot") or 
            (http.user_agent contains "CCBot") or 
            (http.user_agent contains "Claude-Web")
Action: Rate Limit (6 requests per minute)

Rule 4: Protect Admin Paths
Expression: (http.request.uri.path contains "/admin") and 
            (cf.bot_management.score lt 30)
Action: Block

Rule 5: Challenge Suspicious Form Submissions
Expression: (http.request.uri.path eq "/forms/submit") and 
            (cf.bot_management.score lt 50)
Action: Managed Challenge

Rule 6: Block High-Risk Countries (Optional)
Expression: (ip.geoip.country in {"XX" "YY"}) and 
            (cf.bot_management.score lt 40)
Action: Block
Note: Replace XX YY with actual country codes if needed
```

### D. Sample Bot Verification Script (Python)

```python
#!/usr/bin/env python3
"""
Bot Verification Script
Verifies claimed bot identities via reverse DNS lookup
"""

import socket
import logging
from typing import Optional

# Configure logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

# Valid bot domains by bot type
VALID_BOT_DOMAINS = {
    'googlebot': ['.googlebot.com', '.google.com'],
    'bingbot': ['.search.msn.com'],
    'duckduckbot': ['.duckduckgo.com'],
    'slackbot': ['.slack.com'],
    'facebookexternalhit': ['.facebook.com', '.fbsv.net']
}

def verify_bot(ip_address: str, claimed_bot: str) -> bool:
    """
    Verify if IP actually belongs to claimed bot
    
    Args:
        ip_address: IP address of the request
        claimed_bot: Bot name from user-agent (lowercase)
    
    Returns:
        True if verification passes, False otherwise
    """
    # Get valid domains for this bot type
    valid_domains = VALID_BOT_DOMAINS.get(claimed_bot.lower())
    if not valid_domains:
        logger.warning(f"No verification rules for bot: {claimed_bot}")
        return False
    
    try:
        # Step 1: Reverse DNS lookup
        hostname = socket.gethostbyaddr(ip_address)[0]
        logger.info(f"Reverse DNS for {ip_address}: {hostname}")
        
        # Step 2: Check if hostname matches valid domains
        hostname_valid = any(
            hostname.endswith(domain) 
            for domain in valid_domains
        )
        
        if not hostname_valid:
            logger.warning(
                f"Hostname {hostname} doesn't match valid domains "
                f"for {claimed_bot}"
            )
            return False
        
        # Step 3: Forward DNS lookup to verify
        forward_ip = socket.gethostbyname(hostname)
        logger.info(f"Forward DNS for {hostname}: {forward_ip}")
        
        # Step 4: Check if IPs match
        if forward_ip != ip_address:
            logger.warning(
                f"IP mismatch! Claimed: {ip_address}, "
                f"Forward lookup: {forward_ip}"
            )
            return False
        
        logger.info(f"✓ Verified {claimed_bot} from {ip_address}")
        return True
        
    except socket.herror as e:
        logger.error(f"DNS lookup failed for {ip_address}: {e}")
        return False
    except socket.gaierror as e:
        logger.error(f"DNS resolution failed: {e}")
        return False
    except Exception as e:
        logger.error(f"Unexpected error during verification: {e}")
        return False

def extract_bot_name(user_agent: str) -> Optional[str]:
    """
    Extract bot name from user-agent string
    
    Args:
        user_agent: Full user-agent string
    
    Returns:
        Bot name if recognized, None otherwise
    """
    user_agent_lower = user_agent.lower()
    
    for bot_name in VALID_BOT_DOMAINS.keys():
        if bot_name in user_agent_lower:
            return bot_name
    
    return None

# Example usage
if __name__ == "__main__":
    # Test cases
    test_cases = [
        ("66.249.66.1", "Googlebot"),  # Real Googlebot IP
        ("192.168.1.1", "Googlebot"),  # Fake Googlebot
    ]
    
    for ip, claimed_bot in test_cases:
        result = verify_bot(ip, claimed_bot)
        print(f"{ip} claiming to be {claimed_bot}: "
              f"{'✓ VERIFIED' if result else '✗ REJECTED'}")
```

### E. Sample robots.txt With Comments

```
# Agency Name Bot Policy
# Full policy: https://yourdomain.gov/bot-policy
# Last updated: 2024-01-15
# Contact: webmaster@yourdomain.gov

# Default for all bots
User-agent: *
# Protect authentication and admin
Disallow: /admin/
Disallow: /login/
Disallow: /auth/
# Protect internal tools
Disallow: /internal/
Disallow: /staff/
# Prevent search hammering
Disallow: /search/
# Protect form submission endpoints
Disallow: /forms/submit
Disallow: /api/submit
# Prevent email harvesting
Disallow: /*.pdf$email=
Disallow: /*?email=
# Allow everything else
Allow: /

# Google - Full access with polite crawl rate
User-agent: Googlebot
Allow: /
Crawl-delay: 1

User-agent: Googlebot-Image
Allow: /
Crawl-delay: 1

# Bing - Full access with polite crawl rate
User-agent: Bingbot
Allow: /
Crawl-delay: 1

# DuckDuckGo - Full access
User-agent: DuckDuckBot
Allow: /
Crawl-delay: 1

# AI Training Crawlers - Rate limited
# OpenAI GPT
User-agent: GPTBot
Allow: /
Crawl-delay: 10

# Common Crawl (used by many AI)
User-agent: CCBot
Allow: /
Crawl-delay: 10

# Google AI training
User-agent: Google-Extended
Allow: /
Crawl-delay: 10

# Anthropic Claude
User-agent: Claude-Web
Allow: /
Crawl-delay: 10

# ByteDance/TikTok
User-agent: Bytespider
Allow: /
Crawl-delay: 10

# Omgili news aggregator
User-agent: Omgilibot
Allow: /
Crawl-delay: 10

# Internet Archive - Allow for preservation
User-agent: ia_archiver
Allow: /
Crawl-delay: 2

# Social Media Preview Bots - Allow
User-agent: facebookexternalhit
Allow: /
Crawl-delay: 1

User-agent: Twitterbot
Allow: /
Crawl-delay: 1

User-agent: LinkedInBot
Allow: /
Crawl-delay: 1

# Aggressive crawlers - Block
User-agent: AhrefsBot
Disallow: /

User-agent: SemrushBot
Disallow: /

User-agent: MJ12bot
Disallow: /

User-agent: DotBot
Disallow: /

# Sitemaps
Sitemap: https://yourdomain.gov/sitemap.xml
Sitemap: https://yourdomain.gov/sitemap-news.xml
```

---

## Quick Reference Checklist

**Critical Pre-Launch Items:**
- [ ] robots.txt deployed and accessible
- [ ] WAF configured and tested
- [ ] Rate limiting enabled
- [ ] User-agent filtering active
- [ ] Bot verification working
- [ ] Monitoring dashboards ready
- [ ] Alert thresholds configured
- [ ] Rollback plan documented
- [ ] On-call personnel assigned
- [ ] Stakeholders notified

**Day 1 After Launch:**
- [ ] Monitor dashboards continuously
- [ ] Check for false positive reports
- [ ] Verify search engines still crawling
- [ ] Review blocked traffic patterns
- [ ] Check response times
- [ ] Team debrief at end of day

**Week 1 After Launch:**
- [ ] Daily metrics review
- [ ] Tune rules based on real traffic
- [ ] Address all false positives
- [ ] Document lessons learned
- [ ] Adjust thresholds as needed

**Month 1 After Launch:**
- [ ] Generate comprehensive report
- [ ] Review all exception requests
- [ ] Conduct policy review
- [ ] Update documentation
- [ ] Celebrate success! 🎉

---

## Contact Information

**Project Lead:** ___________  
**Email:** ___________  
**Phone:** ___________

**Infrastructure Team Lead:** ___________  
**Email:** ___________  
**Phone:** ___________

**Security Team Lead:** ___________  
**Email:** ___________  
**Phone:** ___________

**Escalation Contact:** ___________  
**Email:** ___________  
**Phone:** ___________

---

**Document Status:** □ Draft □ In Progress □ Complete  
**Last Updated:** ___________  
**Completed By:** ___________  
**Approved By:** ___________
