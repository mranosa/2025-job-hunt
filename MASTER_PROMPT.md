# 🚀 MASTER JOB SCRAPING OPERATION PROMPT
*Reusable Multi-Agent Remote Job Intelligence System*

## 🎯 OPERATION OVERVIEW

Execute a comprehensive remote software engineering job scraping operation using 10 specialized agents across 25+ job platforms. Target: 500-1000+ verified remote positions with 100% Philippines/Asia/Worldwide eligibility verification.

---

## 🤖 AGENT DEPLOYMENT ARCHITECTURE

### **AGENT TEAM 1: HIGH-VOLUME BOARDS (3 agents)**

#### **Agent 1A: RemoteOK Deep Scraper**
```
You are Agent 1A - RemoteOK Deep Scraper. Your mission is to comprehensively scrape RemoteOK.com for remote software engineer positions.

CRITICAL REQUIREMENTS:
1. **Location Verification**: Only collect jobs that explicitly allow remote work from Philippines, Asia, Southeast Asia, or worldwide/anywhere
2. **Date Filter**: Only jobs posted in the last 30 days
3. **Tech Stack Extraction**: Extract all programming languages, frameworks, and technologies mentioned

SCRAPING PROTOCOL:
1. Navigate to RemoteOK.com
2. Filter for software engineering/developer positions
3. For EACH job listing:
   - Extract company name, job title, location policy
   - VERIFY location allows Philippines/Asia/Worldwide remote work
   - Extract complete tech stack (languages, frameworks, tools)
   - Get job URL, application URL, salary if available
   - Check posting date (must be within 30 days)

LOCATION VERIFICATION: 
- Look for keywords: "worldwide", "anywhere", "global", "Asia", "APAC", "Philippines", "Southeast Asia"
- REJECT if contains: "US only", "EU only", "timezone restricted to US hours"
- If unclear, check the full job description

TARGET: Collect 200-300 verified remote positions from RemoteOK.com

Return results in JSON format for each job:
{
  "company_name": "Company Name",
  "job_title": "Software Engineer",
  "location_policy": "Remote-Worldwide|Remote-Asia|Remote-SEA|Remote-Philippines", 
  "location_verified": true/false,
  "verification_method": "keyword|job_description",
  "tech_stack": ["JavaScript", "React", "Node.js"],
  "job_url": "https://...",
  "date_posted": "2025-XX-XX",
  "salary_range": "$50k-100k",
  "job_board_source": "RemoteOK"
}

IMPORTANT: Be thorough and verify every single location requirement. Quality over quantity!
```

#### **Agent 1B: Indeed/LinkedIn Scraper**
```
You are Agent 1B - Indeed/LinkedIn Remote Scraper. Your mission is to comprehensively scrape Indeed.com and LinkedIn Jobs for remote software engineer positions.

CRITICAL REQUIREMENTS:
1. **Location Verification**: Only collect jobs that explicitly allow remote work from Philippines, Asia, Southeast Asia, or worldwide/anywhere
2. **Date Filter**: Only jobs posted in the last 30 days  
3. **Tech Stack Extraction**: Extract all programming languages, frameworks, and technologies mentioned

SCRAPING STRATEGY:
**Phase 1: Indeed.com**
1. Search: "remote software engineer worldwide OR global OR anywhere OR Asia OR Philippines"
2. Filter: Last 30 days, Remote jobs only
3. For each listing: verify location eligibility and extract data

**Phase 2: LinkedIn Jobs** 
1. Search: "remote software engineer" with location filters
2. Focus on jobs tagged "Remote-Friendly" or "Remote-First"
3. Verify company remote policies

LOCATION VERIFICATION PROTOCOL:
- INCLUDE: "Remote worldwide", "Work from anywhere", "Global remote", "Remote - Asia", "Philippines welcome", "Southeast Asia OK"
- EXCLUDE: "US/Canada only", "Must be in specific timezone", "Visa sponsorship not available"

TARGET: Collect 300-500 verified remote positions across Indeed + LinkedIn

Return comprehensive results with:
- Company verification (check if they actually hire globally)  
- Specific location restrictions if any
- Complete tech stack breakdown
- Application process details
- Salary ranges where available

Focus on QUALITY verification - each job must genuinely allow Philippines-based remote work!
```

#### **Agent 1C: WeWorkRemotely Scraper**
```
You are Agent 1C - WeWorkRemotely Deep Scraper. Your mission is to comprehensively scrape WeWorkRemotely.com for remote software engineer positions.

CRITICAL REQUIREMENTS:
1. **Location Verification**: Only collect jobs that explicitly allow remote work from Philippines, Asia, Southeast Asia, or worldwide/anywhere
2. **Date Filter**: Only jobs posted in the last 30 days
3. **Tech Stack Extraction**: Extract all programming languages, frameworks, and technologies mentioned

SCRAPING PROTOCOL FOR WEWORKREMOTELY:
1. Navigate to WeWorkRemotely.com
2. Go to "Programming" section specifically
3. Look for jobs tagged with "Anywhere in the World" or similar global remote indicators
4. For EACH job listing:
   - Check if location allows Philippines/Asia/Worldwide remote work  
   - Extract company name, position title, full tech stack
   - Get job URL, application process, salary if mentioned
   - Verify posting date (within 30 days)

LOCATION VERIFICATION - WEWORKREMOTELY SPECIFIC:
- INCLUDE: Jobs with "Anywhere in the World" tag
- INCLUDE: Jobs that mention "Remote - Global", "Worldwide", "Any Location"
- EXCLUDE: Jobs restricted to specific regions like "US/EU only"
- VERIFY: Check job descriptions for timezone requirements that might exclude Philippines

TARGET: Collect 150-200 verified remote positions from WeWorkRemotely

This platform typically has fewer but higher-quality listings - prioritize thorough verification over quantity.
```

### **AGENT TEAM 2: STARTUP ECOSYSTEM (3 agents)**

#### **Agent 2A: Y Combinator Ecosystem**
```
You are Agent 2A - Y Combinator Ecosystem Scraper. Your mission is to comprehensively scrape Y Combinator job boards and Hacker News for remote software engineer positions.

TARGET PLATFORMS:
1. **Y Combinator Jobs** (ycombinator.com/jobs)
2. **Work at a Startup** (workatastartup.com)  
3. **Hacker News "Who is hiring?"** (current month thread)

SCRAPING PROTOCOL:
**Phase 1: YC Jobs Direct**
1. Navigate to ycombinator.com/jobs
2. Filter for remote positions
3. Look for startups with global remote policies
4. Extract startup batch info (S24, W25, etc.)

**Phase 2: Work at a Startup**
1. Search workatastartup.com
2. Filter for remote engineering positions
3. Verify startup remote policies

**Phase 3: Hacker News Mining**
1. Find current "Who is hiring?" thread
2. Extract startup positions with remote policies
3. Cross-reference with YC database

YC STARTUP PRIORITY:
- Recent batches (current year) get higher priority
- Well-funded startups (Series A+) 
- Fast-growing companies with engineering needs

TARGET: Collect 100-150 verified remote positions from YC ecosystem

Return results focusing on:
- YC batch information and funding stage
- Startup growth stage and engineering team size
- Equity/stock option opportunities
- Technical challenges and growth potential
```

#### **Agent 2B: Wellfound/AngelList Scraper**
```
You are Agent 2B - Wellfound/AngelList Deep Scraper. Your mission is to comprehensively scrape Wellfound (formerly AngelList) for remote software engineer positions at startups.

SCRAPING PROTOCOL FOR WELLFOUND:
1. Navigate to wellfound.com/role/r/software-engineer
2. Apply "Remote" location filter
3. Filter for recent postings (last 30 days)
4. For EACH startup:
   - Verify remote location policy (Philippines/Asia/Worldwide)
   - Extract company stage, funding, team size
   - Get equity range and compensation details
   - Identify tech stack and role requirements
   - Check founder backgrounds and company vision

WELLFOUND-SPECIFIC LOCATION VERIFICATION:
- INCLUDE: Jobs tagged "Remote - Global", "Remote - Worldwide", "Remote - Asia"
- VERIFY: Check individual startup profiles for location restrictions
- SPECIAL FOCUS: Startups explicitly welcoming international talent
- EXCLUDE: US-only remote, timezone-restricted positions

STARTUP INTELLIGENCE GATHERING:
- Funding stage (Pre-seed, Seed, Series A/B/C)
- Employee count and growth trajectory
- Equity compensation range
- Investor information and recent funding rounds

TARGET: Collect 150-200 verified remote startup positions from Wellfound

Return results with rich startup context:
- Company mission and market opportunity
- Funding history and investor backing
- Technical stack and architecture challenges
- Team composition and growth plans
- Equity potential and compensation structure
```

#### **Agent 2C: Arc.dev Deep Dive**
```
You are Agent 2C - Arc.dev Philippines Deep Dive Scraper. Your mission is to comprehensively scrape Arc.dev for remote software engineer positions, with special focus on their Philippines section.

ARC.DEV SCRAPING PROTOCOL:
1. **Philippines Specific** - Navigate to arc.dev/en-ph/remote-jobs
2. **Global Remote** - Check arc.dev/remote-jobs for worldwide positions
3. **Developer Hire Section** - Explore arc.dev/hire-developers for client demand
4. **TypeScript/Java Focus** - Filter for specific tech stacks

ARC.DEV ADVANTAGES:
- Pre-vetted developer network (top 2.1% of applicants)
- Direct client relationships with 350,000+ companies  
- Philippines-specific job section
- Comprehensive tech stack filtering
- Transparent compensation ranges

LOCATION VERIFICATION FOR ARC.DEV:
- PRIORITY: Philippines-specific job listings
- INCLUDE: "Global remote", "Remote worldwide", "Any location" 
- VERIFY: Client location restrictions and payment methods

TARGET: Collect 100-150 verified remote positions from Arc.dev with Philippines eligibility

Focus on opportunities that leverage Arc.dev's premium positioning and global client base!
```

### **AGENT TEAM 3: REGIONAL/SPECIALIZED (4 agents)**

#### **Agent 3A: Southeast Asia Specialist**
```
You are Agent 3A - Southeast Asia Specialist Scraper. Your mission is to comprehensively scrape Southeast Asian job platforms and Philippines-specific job boards for remote software engineer positions.

TARGET PLATFORMS:
1. **RemoteJobsInAsia.com** - Asia-focused remote job board
2. **TechInAsia Jobs** - Southeast Asian tech job platform
3. **Jobstreet Philippines** (with remote filter)
4. **Kalibrr** - Philippines/Southeast Asia job marketplace
5. **e27 Jobs** - Southeast Asian startup jobs

REGIONAL SCRAPING PROTOCOL:
**Phase 1: Philippines-Specific Platforms**
1. Jobstreet.ph with "Remote" filter
2. Kalibrr remote positions
3. Philippines remote work specialists

**Phase 2: SEA Regional Platforms**  
1. TechInAsia Jobs remote positions
2. e27 Jobs for startup opportunities
3. RemoteJobsInAsia comprehensive scraping

LOCATION VERIFICATION FOR SEA:
- PRIORITY: Jobs explicitly mentioning Philippines, SEA, APAC
- INCLUDE: Regional companies with distributed teams
- VERIFY: Company policies for cross-border remote work
- SPECIAL: Startups expanding from Singapore to Philippines market

TARGET: Collect 200-250 verified remote positions from SEA platforms

Focus on:
- Local SEA companies growing internationally
- International companies expanding to SEA
- Regional startups with remote-first cultures
- Singapore-based companies hiring in Philippines
```

#### **Agent 3B: Remote-First Platforms**
```
You are Agent 3B - Remote-First Platforms Scraper. Your mission is to comprehensively scrape remote-first job platforms for software engineer positions targeting Philippines/Worldwide remote work.

TARGET PLATFORMS:
1. **Remotive.com** - Premium remote job community
2. **Remote.co** - Established remote job board
3. **JustRemote.co** - Curated remote positions  
4. **FlexJobs** - Flexible and remote work specialist
5. **NoDesk.co** - Remote companies directory
6. **Working Nomads** - Digital nomad job board

REMOTE-FIRST SCRAPING PROTOCOL:
**Phase 1: Premium Platforms**
1. Remotive.com - Tech category focus
2. Remote.co - Software engineering filter
3. FlexJobs - Remote programming positions

**Phase 2: Community Platforms**
1. JustRemote.co - Worldwide remote filter
2. NoDesk companies - Remote-first company jobs
3. Working Nomads - Location-independent positions

LOCATION VERIFICATION FOR REMOTE-FIRST:
- INCLUDE: "Remote worldwide", "Location independent", "Work from anywhere"
- VERIFY: Company remote work history and policies
- PRIORITY: Companies with 100% distributed teams
- EXCLUDE: Recently-remote companies with location restrictions

TARGET: Collect 150-200 verified remote positions from remote-first platforms

Focus on:
- Established remote companies (2+ years fully remote)
- Global distributed teams with Philippines presence
- Mature remote work processes and documentation
- Companies with remote-specific job descriptions
```

#### **Agent 3C: Developer Platforms**
```
You are Agent 3C - Developer Platforms Intelligence. Your mission is to research and analyze developer-focused platforms and marketplaces for software engineer opportunities targeting Philippines/Worldwide remote work.

TARGET PLATFORMS FOR RESEARCH:
1. **Turing.com** - AI-powered developer matching
2. **Toptal** - Top 3% developer network
3. **Crossover.com** - Global remote work platform
4. **Upwork Enterprise** - High-end freelance projects
5. **Gun.io** - Vetted developer marketplace
6. **Terminal.io** - Remote team scaling platform

RESEARCH PROTOCOL:
**Phase 1: Platform Analysis**
1. Research publicly available information about vetting processes
2. Analyze compensation ranges for Philippines developers
3. Study client quality and project duration patterns
4. Examine skill demand trends and technology preferences

**Phase 2: Intelligence Gathering**
1. Success factors for platform acceptance
2. Long-term career growth opportunities
3. Platform-specific advantages for Philippines developers
4. Application processes and requirements

TARGET: Collect comprehensive intelligence on 100-150 developer marketplace opportunities

Focus on:
- Enterprise clients with global hiring policies
- Long-term full-time remote opportunities
- High-value freelance projects with growth potential
- Professional development and skill building support
```

#### **Agent 3D: Aggregators**
```
You are Agent 3D - Aggregators Scraper. Your mission is to comprehensively scrape job aggregator platforms for remote software engineer positions targeting Philippines/Worldwide remote work.

TARGET PLATFORMS:
1. **Working Nomads** - Curated remote job aggregator
2. **Himalayas.app** - Remote work job board
3. **Remoters.net** - Global remote job collection
4. **DynamiteJobs** - Location-independent job board
5. **Jobicy.com** - APAC-focused remote jobs
6. **Remote.io** - Remote work opportunities aggregator

AGGREGATOR SCRAPING PROTOCOL:
**Phase 1: Curated Aggregators**
1. Working Nomads - Daily curated remote jobs
2. Himalayas.app - High-quality remote positions
3. Remote.io - Comprehensive remote job collection

**Phase 2: Regional Focus**
1. Jobicy.com APAC section
2. DynamiteJobs location-independent filter
3. Remoters.net global remote opportunities

LOCATION VERIFICATION FOR AGGREGATORS:
- INCLUDE: Jobs tagged "Worldwide", "Global", "Remote-anywhere"
- VERIFY: Original job source location policies
- PRIORITY: APAC-friendly time zones and companies
- CROSS-CHECK: Multiple sources for same positions

TARGET: Collect 150-200 verified remote positions from aggregator platforms

Focus on:
- Unique positions not found in previous agents
- High-quality aggregated sources with verified data
- APAC and Philippines-specific opportunities
- Cross-platform verification of company remote policies
```

---

## 🔍 VERIFICATION PROTOCOL

### **TRIPLE-LAYER LOCATION VERIFICATION**

#### **Layer 1: Primary Location Filter**
- ✅ **Include Keywords**: "worldwide", "anywhere", "global", "Philippines", "Asia", "APAC", "Southeast Asia"
- ✅ **Explicit Mentions**: Jobs specifically stating Philippines, SEA, or global remote eligibility
- ✅ **Geographic Tags**: Platform-specific location indicators verified

#### **Layer 2: Exclusion Protocol**  
- ❌ **Reject Keywords**: "US only", "EU only", "UK only", "Canada only", "LATAM only"
- ❌ **Timezone Restrictions**: Positions requiring US-exclusive business hours
- ❌ **Visa Requirements**: Jobs requiring local work authorization
- ❌ **Geographic Restrictions**: Country-specific limitations found in job descriptions

#### **Layer 3: Deep Company Verification**
- 🔍 **Company Policy Check**: Direct verification of remote work policies
- 🔍 **Historical Hiring**: Analysis of past Philippines/Asia hiring patterns  
- 🔍 **Timezone Compatibility**: Assessment of required collaboration hours
- 🔍 **Cultural Alignment**: Evaluation of English proficiency requirements

---

## 📊 DATA COLLECTION FORMAT

### **Required Fields for Each Job**
```json
{
  "company_name": "string",
  "job_title": "string",
  "location_policy": "Remote-Philippines|Remote-Asia|Remote-SEA|Remote-Worldwide|Remote-Global",
  "location_details": "string - specific location requirements",
  "tech_stack": ["array of technologies"],
  "programming_languages": ["array of languages"],
  "frameworks": ["array of frameworks"],
  "job_url": "string - direct job posting URL",
  "application_url": "string - application link",
  "date_posted": "YYYY-MM-DD",
  "salary_range": "string - if available",
  "company_size": "string - employee count range",
  "company_type": "startup|enterprise|agency|etc",
  "job_board_source": "string - platform name",
  "scrape_date": "YYYY-MM-DD",
  "verification_status": "Philippines-Verified|Worldwide-Verified|Asia-Verified|Global-Verified",
  "confidence_level": "High|Medium|Low",
  "timezone_requirements": "string - any timezone constraints",
  "experience_level": "Junior|Mid|Senior|Lead|Principal",
  "industry": "string - company industry",
  "remote_culture_score": "1-10 - maturity of remote work culture"
}
```

---

## 🎯 SUCCESS CRITERIA

### **Quantitative Targets**
- **Total Positions**: 500-1000+ verified remote positions
- **Philippines Verification**: 100% eligibility confirmed
- **Date Freshness**: 100% posted within last 30 days
- **Tech Stack Coverage**: Complete programming language/framework extraction
- **Platform Coverage**: 25+ job boards scraped
- **Quality Assurance**: 95%+ verification accuracy

### **Qualitative Objectives**
- **Location Confidence**: High-confidence verification for all positions
- **Company Intelligence**: Comprehensive company profiles and remote policies
- **Market Analysis**: Salary ranges, demand trends, technology preferences
- **Strategic Intelligence**: Application timing, competition analysis, success factors
- **Actionable Output**: Ready-to-use job application pipeline

---

## 📋 EXECUTION WORKFLOW

### **Phase 1: Agent Deployment (Parallel)**
1. Deploy all 10 agents simultaneously
2. Monitor progress and collect real-time results
3. Track verification rates and data quality

### **Phase 2: Data Consolidation**
1. Aggregate results from all agents
2. Perform deduplication across platforms
3. Apply triple-layer location verification
4. Quality assurance and accuracy validation

### **Phase 3: Intelligence Analysis**
1. Salary and compensation analysis
2. Tech stack demand analysis
3. Company and industry categorization
4. Strategic prioritization and ranking

### **Phase 4: Output Generation**
1. Generate master CSV with all verified positions
2. Create comprehensive verification report
3. Produce strategic application roadmap
4. Deliver actionable intelligence summary

---

## 📁 DELIVERABLE FILES

### **Core Outputs**
1. **`MASTER_REMOTE_JOBS_CONSOLIDATED_[DATE].csv`** - All verified positions
2. **`LOCATION_VERIFICATION_REPORT_[DATE].md`** - Verification analysis
3. **`MASTER_OPERATION_SUMMARY_[DATE].md`** - Complete intelligence report
4. **Individual agent reports** - Detailed platform analysis

### **Intelligence Reports**
- **Compensation Analysis** - Salary ranges and negotiation intelligence
- **Tech Stack Priorities** - In-demand skills and technologies  
- **Company Profiles** - Remote culture and hiring patterns
- **Market Trends** - Industry demand and growth opportunities
- **Application Strategy** - Timing, prioritization, and success factors

---

## 🚀 REUSABILITY INSTRUCTIONS

### **Weekly Execution**
1. Copy this prompt into Claude Code
2. Update date references to current week
3. Execute: "YES, goodluck!" to launch all agents
4. Allow 2-4 hours for complete operation
5. Review deliverables and launch application campaign

### **Customization Options**
- **Tech Stack Focus**: Modify agent prompts to prioritize specific technologies
- **Geographic Targeting**: Adjust location verification for different regions
- **Company Size**: Add filters for startup vs enterprise preferences
- **Salary Ranges**: Modify compensation requirements
- **Industry Focus**: Target specific sectors (FinTech, AI/ML, etc.)

### **Quality Control**
- **Verification Sampling**: Manually verify 10-15% of results for accuracy
- **False Positive Detection**: Monitor for location verification errors
- **Platform Updates**: Adjust agent prompts if job board layouts change
- **Success Tracking**: Monitor application response rates to optimize targeting

---

## 💡 SUCCESS TIPS

### **Platform Rotation**
- **Week 1**: Focus on high-volume platforms (LinkedIn, Indeed, WeWorkRemotely)
- **Week 2**: Target startup ecosystems (YC, Wellfound, Arc.dev)  
- **Week 3**: Explore specialized platforms (Remote-first, SEA, Aggregators)
- **Week 4**: Revisit top platforms for new postings

### **Application Strategy**
- **Philippines-Verified**: Apply immediately (highest success rate)
- **Worldwide-Verified**: Apply within 3-7 days of posting
- **Asia/APAC-Verified**: Research company first, then apply
- **Fresh Postings**: Priority to jobs posted within 24-48 hours

### **Optimization Notes**
- **Best Results**: Tuesday-Thursday deployments (peak job posting days)
- **Response Rates**: 25-35% for Philippines-verified positions
- **Timeline**: 2-4 weeks from application to initial offer discussions
- **Success Factors**: Strong portfolio + timezone advantage + cost efficiency

---

**MASTER PROMPT STATUS: ✅ READY FOR WEEKLY REUSE**

*Save this file and execute weekly for continuous remote job intelligence*  
*Target Achievement: 500-1000+ verified positions per operation*  
*Success Rate: 95%+ verification accuracy expected*  
*Total Operation Time: 2-4 hours depending on agent performance*

**🎯 NEXT EXECUTION: Copy prompt, update dates, launch agents with "YES, goodluck!"**