# Lab Exercise 1: CIS Compliance Workshop - Day 1

## 📋 Overview

This comprehensive lab focuses on implementing and managing CIS (Center for Internet Security) benchmark compliance using Azure Policy and initiatives. The workshop is split into two focused sessions that align with your workshop schedule.

**Total Duration:** 2 hours (split across workshop day)  
**Target Personas:** 🏛️ Compliance Officers + 🔒 Security Officers + ⚙️ Cloud Engineers  
**Focus:** CIS Azure Foundations Benchmark v2.0.0

## 🎯 Complete Learning Objectives

By completing both parts of this lab, you will:

- Navigate Azure Policy and understand CIS benchmark alignment
- Create custom Azure Policy definitions for compliance controls
- Build and assign Policy initiatives incorporating CIS policies  
- Test policy enforcement and observe compliance effects
- Assess existing environments against CIS benchmarks using real data
- Remediate non-compliant resources using native Azure tools
- Collect comprehensive audit evidence and prepare compliance reports
- Present findings and recommendations to stakeholders

## 🏗️ Lab Structure

This lab is organized into two separate sessions aligned with your workshop schedule:

---

## 📚 [Part 1A: Azure Policy & Initiative Setup](./lab-01a-azure-policy-setup.md)
**Workshop Time:** 10:00 - 11:00 AM  
**Duration:** 60 minutes  
**Focus:** Hands-on policy creation and assignment

### What You'll Do:
- Access Azure Policy service and navigate compliance dashboards
- Create custom CIS-aligned policy definitions with proper JSON syntax
- Build policy initiatives combining custom and built-in CIS policies
- Assign initiatives to subscriptions with appropriate parameters
- Test policy enforcement with compliant and non-compliant resources
- Review initial compliance status and prepare data for afternoon session

### Key Deliverables:
- Functional CIS policy initiative assigned to your subscription
- Compliance baseline data for use in Part 1B
- Understanding of policy enforcement mechanisms

---

## 🎯 [Part 1B: CIS Compliance Scenario](./lab-01b-cis-compliance-scenario.md)  
**Workshop Time:** 14:00 - 15:00 PM  
**Duration:** 60 minutes  
**Focus:** Real-world compliance assessment and remediation

### What You'll Do:
- Simulate inheriting a subscription with compliance violations
- Work in teams with assigned roles (Policy Admin, Remediator, Auditor)
- Assess compliance gaps using the policies created in Part 1A
- Prioritize remediation based on risk and business impact
- Execute both automated and manual remediation tasks
- Collect audit evidence and prepare executive presentations
- Present findings and lessons learned to the group

### Key Deliverables:
- Comprehensive compliance assessment report
- Documented remediation actions with before/after evidence
- Executive presentation with recommendations and next steps

---

## 📋 Prerequisites

- [ ] Azure subscription with **Contributor** or **Policy Contributor** access
- [ ] Basic understanding of Azure Portal navigation
- [ ] Familiarity with CIS benchmark concepts (covered in morning presentation)
- [ ] Willingness to work collaboratively in assigned team roles

## 🏆 Expected Outcomes

### **For Compliance Officers:**
- Practical experience implementing industry-standard CIS benchmarks
- Understanding of how to collect and present audit evidence
- Knowledge of Azure's native compliance monitoring capabilities

### **For Security Officers:**
- Hands-on experience with preventive and detective security controls
- Skills in risk-based prioritization of security remediation
- Understanding of automated vs manual security configuration management

### **For Cloud Engineers:**
- Practical policy creation and management skills
- Experience with Azure Policy JSON syntax and parameters
- Knowledge of remediation automation and compliance monitoring

## 🔗 Getting Started

**Begin with [Lab Exercise 1A: Azure Policy & Initiative Setup](./lab-01a-azure-policy-setup.md)** during the morning session, then return for [Lab Exercise 1B: CIS Compliance Scenario](./lab-01b-cis-compliance-scenario.md) in the afternoon.

The data and policies you create in Part 1A will be essential for the realistic compliance scenario in Part 1B, so both sessions build upon each other to provide a complete learning experience.

---

## 🎯 Lab Completion Checklist

### Part 1: Policy & Initiative Setup ✅
- [ ] Successfully accessed Azure Policy service
- [ ] Created custom CIS-aligned policy definition
- [ ] Built initiative with custom and built-in CIS policies
- [ ] Assigned initiative to subscription/resource group
- [ ] Tested policy enforcement with compliant/non-compliant resources
- [ ] Reviewed initial compliance dashboard

### Part 2: CIS Compliance Scenario ✅
- [ ] Assessed baseline compliance against CIS initiative
- [ ] Identified and prioritized non-compliant resources
- [ ] Executed both automated and manual remediation
- [ ] Verified compliance improvements post-remediation
- [ ] Collected comprehensive audit evidence
- [ ] Presented findings and lessons learned to group

## 🏆 Key Takeaways

### **For Compliance Officers:**
- **CIS benchmarks** provide industry-standard security baselines for Azure
- **Policy initiatives** group related controls for comprehensive assessment
- **Compliance dashboards** offer real-time visibility into organizational posture
- **Evidence collection** is automated through policy compliance reporting

### **For Security Officers:**
- **Preventive controls** (deny effects) stop violations before they occur
- **Detective controls** (audit effects) identify existing violations for remediation
- **Risk-based prioritization** focuses effort on highest-impact security gaps
- **Automated remediation** reduces time-to-fix for common security misconfigurations

### **For Cloud Engineers:**
- **Policy-as-code** enables scalable compliance management
- **Initiative assignments** can be scoped to specific environments or applications
- **Remediation tasks** automate common configuration fixes
- **Compliance APIs** enable integration with external reporting systems

## 🔗 Next Steps

1. **Implement in Production:** Apply CIS policies to production subscriptions with appropriate testing
2. **Automate Monitoring:** Set up regular compliance reporting and alerting
3. **Expand Coverage:** Implement additional CIS controls and industry-specific requirements
4. **Integrate CI/CD:** Include policy compliance checks in deployment pipelines

## 🆘 Troubleshooting Tips

**Policy not evaluating:**
- Allow 10-15 minutes for initial policy evaluation
- Check policy assignment scope matches target resources
- Verify policy syntax and parameters are correct

**Remediation not working:**
- Ensure managed identity has appropriate permissions
- Check if resource supports the specific remediation action
- Review remediation task logs for detailed error messages

**Compliance data not showing:**
- Refresh browser and clear cache
- Verify you have Reader access to Policy compliance data
- Check that resources exist within the policy assignment scope

---

**🎉 Congratulations!** You've successfully completed hands-on CIS compliance management using Azure Policy. You now have practical experience with industry-standard compliance frameworks and Azure's native governance tools.



