# 🛡️ Azure Compliance Workshop

## Welcome to the Azure Compliance Workshop

This comprehensive workshop is designed to empower compliance professionals, security officers, and cloud engineers with hands-on experience in Azure compliance management. Through practical exercises, you'll learn to implement robust compliance frameworks, automate governance processes, and leverage AI-driven insights for enterprise-scale compliance operations.

## 🎯 Workshop Objectives

By completing this workshop, participants will:

- **Master Azure Policy** - Create, assign, and manage custom policies for organizational compliance
- **Leverage Resource Graph** - Query compliance data and build executive dashboards
- **Automate Exception Management** - Implement streamlined approval workflows for policy exemptions  
- **Deploy AI Compliance Assistants** - Use Azure AI Foundry to build intelligent compliance tools
- **Understand Persona-Based Views** - Navigate compliance from different organizational perspectives

## 👥 Target Personas

This workshop is tailored for three key organizational roles:

### 🏛️ **Compliance Officer**
*Focus: Regulatory adherence, risk management, audit preparation*
- Overall compliance posture monitoring
- Regulatory framework alignment
- Exception tracking and approval
- Evidence collection and reporting

### 🔒 **Security Officer** 
*Focus: Security controls, threat detection, incident response*
- Security policy enforcement
- Vulnerability management
- Identity and access governance
- Threat landscape monitoring

### ⚙️ **Cloud Engineer**
*Focus: Implementation, automation, technical remediation*
- Policy development and deployment
- Automation and CI/CD integration
- Technical remediation workflows
- Infrastructure as code compliance

## 🧪 Lab Exercises

### 📋 [Lab Exercise 1: Azure Policy & Initiative Setup](./labs/lab-01-azure-policy-setup.md)
**Workshop Time:** Morning Session (10:00-11:00)  
**Target Persona:** 🏛️ Compliance Officer + 🔒 Security Officer + ⚙️ Cloud Engineer  
**Duration:** 60 minutes  
**Prerequisites:** Azure subscription with Contributor or Policy Contributor access  
**Focus:** CIS Azure Foundations Benchmark v2.0.0

Learn to create custom Azure Policy definitions aligned with CIS benchmarks, build comprehensive policy initiatives, and assign them for organizational compliance monitoring.

**Key Learning Outcomes:**
- Navigate Azure Policy service and understand CIS benchmark alignment
- Create custom Azure Policy definitions for compliance controls using JSON
- Build and assign Policy initiatives incorporating CIS policies
- Test policy enforcement and observe compliance effects
- Review compliance dashboards and document baseline findings

---

### 🎯 [Lab Exercise 2: CIS Compliance Scenario](./labs/lab-02-cis-compliance-scenario.md)
**Workshop Time:** Afternoon Session (14:00-15:00)  
**Target Persona:** 🏛️ Compliance Officer + 🔒 Security Officer + ⚙️ Cloud Engineer  
**Duration:** 60 minutes  
**Prerequisites:** Completed Lab Exercise 1, Group role assignments  
**Focus:** Real-world CIS compliance assessment and remediation

Simulate inheriting an Azure subscription with compliance violations and execute a complete assessment, remediation, and reporting cycle using team-based roles.

**Key Learning Outcomes:**
- Assess existing environments against CIS benchmarks using policy data
- Prioritize remediation efforts based on risk and business impact
- Execute both automated and manual remediation tasks
- Collect comprehensive audit evidence for compliance reporting
- Present findings and recommendations to stakeholders

---

### 🤖 [Lab Exercise 3: AI-Driven Compliance Assistant](./labs/lab-03-ai-compliance-assistant.md)
**Workshop Time:** Day 2 Afternoon Session (14:00-15:00)  
**Target Persona:** 🏛️ Compliance Officer + 🔒 Security Officer + ⚙️ Cloud Engineer  
**Duration:** 60 minutes  
**Prerequisites:** Azure subscription with AI services access

Deploy an intelligent compliance assistant using Azure AI Foundry with GPT-4o, complete with RAG functionality using real compliance data for persona-based analysis and decision support.

**Key Learning Outcomes:**
- Deploy Azure AI Foundry instance in Sweden Central with GPT-4o model
- Create and configure AI agent with compliance-specific system prompts
- Upload and index Contoso compliance report for RAG functionality  
- Use persona-based prompts to extract actionable insights from compliance data
- Experience practical value of AI assistants for compliance analysis and reporting
- Understand AI limitations and production implementation considerations

---

## 📁 Repository Structure

```
compliance-workshop/
├── README.md                              # This landing page
├── labs/                                 # Lab exercise instructions
│   ├── lab-01-azure-policy-setup.md     # Lab 1: Policy & Initiative Setup
│   ├── lab-02-cis-compliance-scenario.md # Lab 2: CIS Compliance Scenario
│   └── lab-03-ai-compliance-assistant.md # Lab 3: AI Foundry with GPT-4o and RAG
├── workbooks/                           # Azure Workbook templates (future)
│   └── workbook-compliance-personas.json
└── assets/                             # Supporting files and compliance data
    └── Contoso Azure Compliance and Security Report.pdf
```

## 🚀 Getting Started

1. **Clone this repository** to your local machine or access it directly on GitHub
2. **Review the prerequisites** for each lab exercise you plan to complete
3. **Choose your persona path** or complete all exercises for comprehensive understanding
4. **Follow the lab exercises** in order, as each builds upon previous concepts
5. **Join the discussion** - Share findings and ask questions during group sessions

## 📋 Prerequisites Checklist

Before starting the workshop, ensure you have:

- [ ] **Azure Subscription** with Contributor or Owner access
- [ ] **Azure CLI** or **Azure PowerShell** installed (for some exercises)
- [ ] **Basic familiarity** with Azure Portal navigation
- [ ] **Text editor** for viewing and editing JSON/code files

## 💡 Workshop Tips

- **Take your time** - Each exercise includes verification steps to ensure success
- **Document your findings** - Note any organization-specific adaptations needed  
- **Experiment safely** - All exercises use non-production resources
- **Ask questions** - This is a learning environment designed for exploration
- **Think beyond the lab** - Consider how concepts apply to your real-world scenarios

## 🤝 Support & Resources

- **Workshop Issues:** Create an issue in this repository for technical problems
- **Azure Documentation:** [docs.microsoft.com/azure](https://docs.microsoft.com/azure)
- **Azure Policy Samples:** [Azure Policy GitHub Repository](https://github.com/Azure/azure-policy)
- **Community Support:** [Microsoft Tech Community](https://techcommunity.microsoft.com/azure)

## 📄 License

This workshop content is provided under the MIT License. Feel free to adapt and use these materials for your organization's training needs.

---

**Ready to begin?** Choose your first lab exercise based on your role and dive into hands-on Azure compliance management!