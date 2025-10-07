# Lab Exercise 3: AI-Driven Compliance Assistant with Azure AI Foundry

## 📋 Overview

This hands-on lab demonstrates how AI can transform compliance management by deploying an intelligent Azure AI Foundry agent with GPT-4o. You'll create a RAG (Retrieval Augmented Generation) system using real compliance data and interact with persona-specific prompts to understand AI's value for compliance work.

**Duration:** 60 minutes  
**Target Personas:** 🏛️ Compliance Officer + 🔒 Security Officer + ⚙️ Cloud Engineer  
**Focus:** AI-powered compliance automation and decision support

## 🏢 Real-World Scenario: Contoso Ltd Quarterly Compliance Review

**Background:** You've just joined Contoso Ltd as part of their compliance team during a critical quarterly compliance review. The company has been struggling with manual compliance analysis, spending weeks reviewing reports, and struggling to provide actionable insights to different stakeholders across the organization.

**The Challenge:** 
- The **Compliance Officer** needs to present a comprehensive risk assessment to the board next week
- The **Security Officer** requires immediate identification of critical security gaps for incident response
- The **Cloud Engineer** needs a prioritized remediation plan with technical implementation steps
- All three personas need insights extracted from a 47-page compliance assessment report - **manually analyzing this would take days**

**Your Mission:** 
Deploy an AI-powered compliance assistant that can instantly analyze the Contoso compliance report and provide persona-specific insights. Through targeted prompts, you'll discover how AI can transform weeks of manual analysis into minutes of intelligent automation.

**Success Criteria:** 
By the end of this lab, you'll use your AI assistant to reach specific conclusions about:
- **Risk Priority Matrix** - Which compliance gaps pose the highest business risk?
- **Immediate Action Items** - What critical security issues need attention this week?
- **Technical Roadmap** - What's the most efficient remediation sequence for cloud engineers?
- **Executive Summary** - How do you communicate compliance status to non-technical leadership?

## 🎯 Learning Objectives

By completing this lab, you will:

- Deploy an Azure AI Foundry instance with GPT-4o model capabilities
- Create and configure an AI agent for compliance-specific tasks
- Upload and index compliance documentation for RAG functionality
- Use persona-based prompts to extract actionable insights from compliance data
- Understand how AI can accelerate compliance analysis and reporting
- Experience the practical value of AI assistants for different organizational roles

## 📋 Prerequisites

- [ ] Azure subscription with **AI services access** and sufficient quota for GPT-4o
- [ ] **Owner or Contributor** permissions in the target subscription
- [ ] Access to the **Contoso Azure Compliance and Security Report.pdf** file in repository assets
- [ ] Basic understanding of AI/ML concepts (helpful but not required)
- [ ] Completed Labs 1 and 2 for context (recommended)

## 🗂️ Required Files

Ensure you have access to this file in your repository:
- `assets/Contoso Azure Compliance and Security Report.pdf`

---

## Step 1: Create Azure AI Foundry Instance

### 1A: Access Azure AI Foundry

1. **Navigate to Azure Portal**
   - Go to [portal.azure.com](https://portal.azure.com)
   - Sign in with your Azure credentials

2. **Search for AI Foundry**
   - In the search bar, type **"AI Foundry"**
   - Select **Azure AI Foundry** from the results
   - Click **Create a resource** to start the deployment process

### 1B: Configure AI Foundry Instance

1. **Basic Configuration**
   - **Subscription:** Select your subscription
   - **Resource group:** Create new: `rg-compliance-ai-foundry`
   - **Name:** `aif-compliance-workshop-[yourname]` (replace [yourname] with your initials)
   - **Region:** **Sweden Central**

2. **Your first project**
   - **Default project name:** `ComplianceWorkshopProject`
   
3. **Content Review Policy**  
   - Review the Azure OpenAI content policy information
   - Accept the terms for Azure OpenAI Service access
   - Click checkboxes for content filtering and abuse monitoring if required

4. **Deploy the Instance**
   - Click **Next** to review settings
   - Click **Create** 
   - **Wait time:** 5-10 minutes for deployment completion

---

## Step 2: Configure GPT-4o Model

### 2A: Access AI Foundry Studio

1. **Open AI Foundry Studio**
   - Once deployment is complete, click **Go to resource**
   - Click **Launch AI Foundry Studio** button
   - This opens the AI Foundry web interface

2. **Navigate to Models**
   - In the left sidebar, click **Models**
   - Click **+ Deploy model**
   - Search for **GPT-4o**

### 2B: Deploy GPT-4o Model

1. **Select GPT-4o Model**
   - Find **GPT-4o** in the model catalog
   - Click **Deploy**
   - **Deployment name:** `gpt-4o-compliance-agent`
   - **Version:** Latest available
   - **Deployment type:** Standard

2. **Configure Model Settings**
   - **Tokens per minute rate limit:** 30,000 (or maximum available)
   - **Content filter:** Standard (default)
   - **Enable system message:** Yes
   - Click **Deploy**

3. **Verify Deployment**
   - Wait for deployment status to show **Succeeded**
   - Note the **deployment endpoint** for later use
   - Test the model with a simple query: "Hello, can you help with compliance?"

---

## Step 3: Create Compliance AI Agent

### 3A: Create New Agent

1. **Navigate to Agents**
   - In AI Foundry Studio, click **Agents** in the left sidebar
   - Click **+ New agent**
   - **Agent name:** `ComplianceAdvisor-[yourname]`
   - **Description:** `AI assistant for Azure compliance analysis and recommendations`

2. **Configure Agent Settings**
   - **Model:** Select your deployed `gpt-4o-compliance-agent`
   - **System message:** Copy and paste the following:

```
You are a specialized Azure Compliance Advisor AI assistant. You help Compliance Officers, Security Officers, and Cloud Engineers analyze compliance data, provide remediation guidance, and generate actionable insights.

Your expertise includes:
- CIS Azure Foundations Benchmark
- PCI DSS requirements
- Microsoft Cloud Security Benchmark (MCSB)
- Azure Policy implementation
- Risk assessment and prioritization
- Compliance reporting and evidence collection

When responding:
1. Always provide specific, actionable recommendations
2. Include relevant control IDs and standard references
3. Format responses with clear headings and bullet points
4. Prioritize findings by business impact and security risk
5. Suggest concrete implementation steps where applicable
6. Reference Azure-native tools and services for solutions

You have access to compliance assessment data through uploaded documents. Use this data to provide contextual, data-driven responses tailored to the user's specific environment and role.
```

3. **Save Agent Configuration**
   - Click **Save** to create the agent
   - Verify the agent appears in your agents list

### 3B: Test Basic Agent Functionality

1. **Open Agent Chat**
   - Click on your newly created agent
   - This opens the **Agent Playground**
   - Test with: "Hello, I'm a Compliance Officer. Can you help me understand your capabilities?"

2. **Verify Response Quality**
   - The agent should respond with compliance-focused capabilities
   - Note the professional tone and structured formatting
   - If responses are generic, check the system message configuration

---

## Step 4: Upload and Index Compliance Document

### 4A: Access Data Sources

1. **Navigate to Data Sources**
   - In AI Foundry Studio, click **Data** in the left sidebar
   - Click **+ Add data source**
   - Select **Upload files**

2. **Upload Contoso Report**
   - Click **Browse files**
   - Navigate to your repository's `assets` folder
   - Select **Contoso Azure Compliance and Security Report.pdf**
   - Click **Upload**
   - **Data source name:** `Contoso-Compliance-Assessment`

### 4B: Configure Document Indexing

1. **Index Settings**
   - **Chunk size:** 1000 tokens (default)
   - **Overlap:** 200 tokens (default)
   - **Search type:** Hybrid (vector + keyword)
   - **Enable semantic ranking:** Yes

2. **Start Indexing Process**
   - Click **Create and index**
   - **Processing time:** 3-5 minutes depending on document size
   - Monitor progress in the **Data sources** section

3. **Verify Indexing Completion**
   - Status should show **Indexing completed**
   - **Chunks created:** Should show 50+ chunks (varies by document size)
   - **Index name:** Note this for agent configuration

### 4C: Connect Data Source to Agent

1. **Update Agent Configuration**
   - Return to your **ComplianceAdvisor** agent
   - Click **Settings** or **Edit**
   - In **Data sources**, click **+ Add data source**

2. **Link Indexed Document**
   - Select your **Contoso-Compliance-Assessment** data source
   - **Search relevance:** 0.7 (default)
   - **Max search results:** 10
   - Click **Save**

3. **Test RAG Functionality**
   - In the agent playground, ask: "What are the top compliance findings in the Contoso assessment?"
   - The response should reference specific data from the uploaded document
   - Verify the agent cites document sections in its responses

---

## Step 5: Persona-Based Compliance Analysis

Now you'll use specialized prompts designed for different organizational roles to demonstrate AI's value for compliance work.

### 5A: Compliance Officer Scenarios

**Choose your role:** 🏛️ **Compliance Officer**

1. **Regulatory Overview Prompt**
   
   Copy and paste this prompt:
   ```
   Provide a consolidated compliance overview across CIS Azure, PCI DSS, and MCSB from the Contoso assessment. Return a table of the top 10 failing controls with columns: standard, control_id, title, severity, affected_resources, non_compliant_percentage, and remediation_priority. End with a numbered list of the 5 fastest wins to improve overall compliance posture.
   ```

2. **Audit Evidence Preparation**
   
   Use this prompt:
   ```
   Generate an evidence checklist for the top CIS and PCI gaps found in the Contoso assessment. List required documentation, screenshots to capture (e.g., policy assignment pages, diagnostic settings), Azure portal paths to access them, and who should collect each piece of evidence based on resource ownership.
   ```

3. **Executive Summary Generation**
   
   Try this prompt:
   ```
   Summarize the Contoso compliance assessment for executive leadership. Provide current posture, top 5 business risks, and strategic recommendations in bullet format suitable for a board presentation. Keep it to 10 bullets with plain language and quantified business impact where possible.
   ```

### 5B: Security Officer Scenarios

**Choose your role:** 🔒 **Security Officer**

1. **High-Severity Security Findings**
   
   Copy and paste:
   ```
   From the Contoso assessment, create a security hotlist of all Critical and High severity findings. Provide a table with: finding_title, affected_systems, security_risk, potential_impact, and immediate_action_required. Focus on findings that could lead to data breach, privilege escalation, or network compromise.
   ```

2. **Identity and Access Weaknesses**
   
   Use this prompt:
   ```
   Analyze identity and access management findings in the Contoso report. List all findings related to MFA, privileged access, legacy authentication, and standing permissions. For each finding, provide: current_risk_level, attack_scenarios, and step-by-step remediation with minimal business disruption.
   ```

3. **Incident Response Readiness**
   
   Try this prompt:
   ```
   Based on the Contoso logging and monitoring findings, evaluate incident response readiness. Identify gaps in security logging, SIEM integration, and alerting capabilities. Provide a prioritized action plan to improve detection and response capabilities within 90 days.
   ```

### 5C: Cloud Engineer Scenarios

**Choose your role:** ⚙️ **Cloud Engineer**

1. **Implementation Backlog**
   
   Copy and paste:
   ```
   Convert the top 15 technical findings from the Contoso assessment into an engineering backlog. For each finding, provide: control_id, required_azure_policy, CLI_or_PowerShell_command_example, validation_steps, and estimated_effort_hours. Prioritize by technical complexity and business impact.
   ```

2. **Azure Policy Automation**
   
   Use this prompt:
   ```
   For the policy-related findings in the Contoso report, generate Azure Policy initiative assignment guidance. Include: initiative_name, policy_effect (Deny/Audit/DeployIfNotExists), recommended_scope, parameter_values, and a phased rollout plan from test environments to production.
   ```

3. **Infrastructure as Code Remediation**
   
   Try this prompt:
   ```
   Based on the Contoso security configuration gaps, provide Infrastructure as Code examples (ARM template or Bicep snippets) to implement: network security groups baseline, storage account security settings, and Key Vault access policies. Include validation commands and rollback procedures.
   ```

---

## Step 6: Advanced AI Compliance Scenarios

### 6A: Exception Management Simulation

Use this scenario-based prompt to simulate real-world exception requests:

```
Scenario: A development team requests an exception to deploy App Services with HTTP (not HTTPS only), which violates CIS Azure control 10.1 found in the Contoso assessment. 

Based on the assessment data:
1. Explain the specific security risks of this exception
2. Identify what compensating controls are required
3. Draft an exception approval memo with required business justification
4. Suggest monitoring and review requirements for this exception
5. Provide a timeline for when this exception should be re-evaluated
```

### 6B: Compliance Gap Analysis

Use this advanced analytical prompt:

```
Perform a cross-standard gap analysis using the Contoso assessment. Identify controls that appear across multiple standards (CIS, PCI DSS, MCSB) but are failing. For each overlapping control:
1. List all standard references (e.g., CIS 5.1, PCI 3.4, MCSB DP.4)
2. Assess cumulative business risk of non-compliance
3. Calculate remediation ROI (reduced audit findings vs implementation cost)
4. Recommend unified remediation approach that satisfies all standards
```

### 6C: Future State Architecture

Try this strategic planning prompt:

```
Based on the Contoso compliance findings and industry best practices, design a target state compliance architecture for 12 months from now. Include:
1. Recommended Azure services and configurations
2. Automated compliance monitoring and reporting approach
3. Policy-as-code implementation strategy
4. Integration with existing security tools and processes
5. Success metrics and KPIs for measuring compliance improvement
```

---

## Step 7: Document Insights and Recommendations

### 7A: Capture Key Insights

As you work through the persona-based prompts, document:

1. **Most Valuable AI Responses**
   - Which prompts provided the most actionable insights?
   - What information would have taken hours to compile manually?
   - Which responses changed your understanding of the compliance data?

2. **Role-Specific Value**
   - How did AI responses differ for each persona?
   - Which role benefited most from AI assistance?
   - What types of questions worked best for your role?

### 7B: Identify AI Limitations

Note any areas where the AI assistant:
- Provided generic responses despite having specific data
- Missed important context or nuances
- Required follow-up prompts for clarification
- Made recommendations that wouldn't work in your environment

### 7C: Plan Production Implementation

Consider how you might use AI compliance assistants in your organization:
- **Data Sources:** What compliance reports and policies would you upload?
- **User Access:** Who should have access to different types of AI insights?
- **Integration:** How would this connect with existing compliance tools?
- **Governance:** What controls are needed for AI-generated compliance advice?

---

## 🎯 Lab Completion Checklist

- [ ] Successfully deployed Azure AI Foundry instance in Sweden Central
- [ ] Configured and tested GPT-4o model deployment
- [ ] Created ComplianceAdvisor AI agent with appropriate system message
- [ ] Uploaded and indexed Contoso compliance report for RAG functionality
- [ ] Tested persona-based prompts for Compliance Officer role
- [ ] Tested persona-based prompts for Security Officer role  
- [ ] Tested persona-based prompts for Cloud Engineer role
- [ ] Completed advanced scenario analysis (exception management, gap analysis)
- [ ] Documented insights and limitations of AI assistance
- [ ] Identified potential use cases for production implementation

## � Lab Conclusions: Contoso Compliance Analysis Results

### **Mission Accomplished - What You Discovered:**

Using the AI assistant and persona-specific prompts, you should now be able to present concrete findings to Contoso's leadership:

#### **📊 Risk Priority Matrix (Compliance Officer Conclusion):**
- **Critical Findings:** [Document the 3-5 highest risk items the AI identified]
- **Risk Score Justification:** [Note how AI explained the risk prioritization methodology]
- **Board Presentation Status:** [Summarize key points suitable for executive communication]

#### **🚨 Immediate Action Items (Security Officer Conclusion):**
- **This Week's Priorities:** [List urgent security gaps requiring immediate attention]
- **Incident Response Readiness:** [Document current security posture assessment]
- **Resource Allocation:** [Note AI recommendations for security team focus areas]

#### **⚙️ Technical Roadmap (Cloud Engineer Conclusion):**
- **Implementation Sequence:** [Outline the optimal remediation order suggested by AI]
- **Effort Estimates:** [Document complexity assessments for each remediation task]
- **Automation Opportunities:** [Identify which fixes can be automated vs. manual]

#### **💼 Executive Summary (All Personas):**
- **Overall Compliance Status:** [Provide percentage or grade-level assessment]
- **Timeline for Full Compliance:** [Realistic timeline based on AI analysis]
- **Investment Requirements:** [Resource needs identified through AI insights]

### **🔍 Reflection Questions - Did Your AI Assistant Help You:**

1. **Reduce Analysis Time:** How long would manual analysis have taken vs. AI-assisted?
2. **Improve Accuracy:** Did AI catch patterns or relationships you might have missed?
3. **Enable Better Decisions:** How did persona-specific insights change your approach?
4. **Create Actionable Outputs:** Are your conclusions ready for immediate organizational use?

## �🏆 Key Takeaways

### **For Compliance Officers:**
- **AI accelerates analysis** of large compliance datasets and cross-standard mapping
- **Automated report generation** can produce executive summaries and audit evidence lists
- **Exception management** becomes more consistent with AI-generated risk assessments
- **Trend analysis** across multiple assessments becomes feasible with AI assistance

### **For Security Officers:**
- **Risk prioritization** improves with AI's ability to correlate findings across controls
- **Incident response planning** benefits from AI's comprehensive view of security gaps  
- **Remediation planning** becomes more systematic with AI-generated technical guidance
- **Threat landscape awareness** increases through AI's pattern recognition capabilities

### **For Cloud Engineers:**
- **Implementation guidance** provides concrete steps and code examples for remediation
- **Policy automation** becomes more accessible with AI-generated policy definitions
- **Technical documentation** improves with AI assistance in explaining complex configurations
- **Validation procedures** become more comprehensive with AI-suggested testing approaches

## 🔗 Next Steps

### **Immediate Actions:**
1. **Save your agent configuration** for future use in compliance assessments
2. **Export valuable AI responses** as templates for recurring analysis tasks
3. **Document lessons learned** about effective AI prompting for compliance work
4. **Share insights** with your organization's compliance and security teams

### **Future Implementation:**
1. **Expand data sources** to include your organization's actual compliance reports
2. **Integrate with existing tools** through Azure AI Foundry APIs
3. **Develop custom agents** for specific compliance frameworks or industries
4. **Create automated workflows** that combine AI insights with approval processes

## 🆘 Troubleshooting Tips

**AI Foundry deployment issues:**
- Ensure you have sufficient quota for GPT-4o in Sweden Central region
- Check that all required Azure services are available in your subscription
- Verify you have Owner or Contributor permissions on the subscription

**Document indexing problems:**
- Ensure PDF file is not password-protected or corrupted
- Check file size limits (typically 100MB maximum)
- Try re-uploading if indexing appears stuck

**Agent not referencing uploaded data:**
- Verify data source is properly connected to agent configuration
- Test with specific questions about document content
- Check that indexing completed successfully with chunks created

**Generic or unhelpful AI responses:**
- Refine system message to be more specific about your needs
- Use more detailed prompts with specific context
- Reference specific sections or findings from the uploaded document
- Experiment with different prompt structures and formats

---

**🎉 Congratulations!** You've successfully deployed an AI-powered compliance assistant and experienced firsthand how AI can transform compliance analysis, reporting, and decision-making. The insights and efficiencies you've discovered represent the future of intelligent compliance management in cloud environments.