# Lab Exercise 2: CIS Compliance Scenario

## 📋 Lab 2 Overview

This practical exercise simulates a real-world compliance scenario where you inherit an Azure subscription with existing resources and must assess, remediate, and report on CIS benchmark violations using only native Azure tools.

**Duration:** 60 minutes  
**Target Personas:** 🏛️ Compliance Officers + 🔒 Security Officers + ⚙️ Cloud Engineers  
**Focus:** Real-world CIS compliance assessment and remediation

## 🎯 Learning Objectives

By completing this lab, you will:

- Assess existing environments against CIS benchmarks using Azure Policy
- Prioritize remediation efforts based on risk and business impact
- Execute both automated and manual remediation tasks
- Collect comprehensive audit evidence for compliance reporting
- Present findings and lessons learned to stakeholders

## 📋 Prerequisites

- [ ] **Completed Lab Exercise 1** (Azure Policy & Initiative Setup)
- [ ] Azure subscription with resources and active policy assignments
- [ ] Group work assignment completed (see roles below)

## 👥 Group Roles

**Assign these roles within your team:**

### **👤 Policy Admin**
- Manages policy assignments and compliance monitoring
- Reviews compliance dashboards and policy effectiveness
- Coordinates policy changes and remediation task creation

### **🔧 Remediator** 
- Executes remediation tasks and configuration changes
- Implements manual fixes for non-compliant resources
- Validates remediation success and resource functionality

### **📋 Auditor**
- Documents findings, collects evidence, and prepares reports
- Takes screenshots and exports compliance data
- Maintains remediation logs and audit trails

---

## Scenario Background

Your organization has just acquired a subsidiary with an existing Azure subscription containing various resources deployed over the past year. As the compliance team, you must:

1. **Assess** the current environment against CIS Azure Foundations Benchmark
2. **Prioritize** remediation efforts based on risk and business impact  
3. **Remediate** non-compliant resources using available tools
4. **Document** all findings and actions for an upcoming audit
5. **Present** your compliance posture to executive leadership

---

## Step 1: Assess Current Compliance

### 2A: Initial Compliance Assessment

1. **Policy Admin:** Navigate to Azure Portal > **Policy** > **Compliance**
2. Filter by your CIS initiative assignment from Lab 1
3. Document the overall compliance percentage
4. **Auditor:** Take a screenshot of the main compliance dashboard

### 2B: Identify Non-Compliant Resources

1. Click on your "CIS Baseline Compliance Assessment" initiative
2. For each failing policy, document:
   - **Policy name** and CIS control reference
   - **Number of non-compliant resources**
   - **Resource types affected** (storage accounts, VMs, etc.)
   - **Specific violation details**

3. **Auditor:** Export compliance data:
   - Click **Download** > **CSV** 
   - Save file as `baseline-compliance-assessment.csv`

### 1C: Analyze Common Violations

Review the most typical violations you'll encounter:

- **Missing Environment tags** on resources
- **Storage accounts without secure transfer** enabled
- **Virtual machines not using managed disks**
- **Custom RBAC roles** in use without proper justification
- **Network security groups** with overly permissive rules

**Team Discussion (5 minutes):** Which violations pose the highest security risk to the organization?

---

## Step 2: Prioritize Remediation

### 2A: Risk-Based Priority Assessment

**All Team Members:** Collaborate to rank violations using this framework:

#### **🔴 High Priority**
- Security configurations exposing data (storage encryption, network access)
- Identity and access management weaknesses
- Public-facing resources with security gaps

#### **🟡 Medium Priority**
- Operational compliance gaps (tagging, monitoring)
- Infrastructure security improvements (managed disks, backup)
- Governance violations (unauthorized RBAC)

#### **🟢 Low Priority**
- Documentation and metadata improvements
- Non-security related policy violations
- Cosmetic compliance issues

### 2B: Create Remediation Plan

**Auditor:** Document your team's prioritization decisions:

1. **Critical items** requiring immediate attention
2. **High priority items** for this session
3. **Medium priority items** for future remediation
4. **Items requiring approval** or maintenance windows

---

## Step 3: Execute Remediation

### 3A: Automated Remediation (Where Available)

1. **Policy Admin:** Check for available remediation tasks
   - Go to **Policy** > **Remediation**
   - Look for policies that support automatic remediation
   - Click **Create remediation task** for applicable policies

2. **Example: Storage Account Security**
   - If "Secure transfer to storage accounts should be enabled" shows remediation options
   - Create remediation task to automatically enable secure transfer
   - Monitor task progress in the remediation dashboard

3. **Auditor:** Document automated remediation:
   - Which policies support automation
   - Remediation task IDs and status
   - Expected completion timeframes

### 3B: Manual Remediation

#### **Fix Missing Environment Tags**

**Remediator:** For each resource missing the Environment tag:

1. Navigate to the non-compliant resource in Azure Portal
2. Click on the **Tags** section
3. Add required tag:
   - **Key:** `Environment`
   - **Value:** Choose appropriate value (`Production`, `Development`, `Testing`)
4. Click **Apply**
5. **Auditor:** Log the resource name, type, and tag value applied

#### **Enable Storage Account Security**

**Remediator:** For non-compliant storage accounts:

1. Navigate to **Storage accounts**
2. Select the non-compliant storage account
3. Go to **Security + networking** > **Configuration**
4. Set **Secure transfer required** to **Enabled**
5. Click **Save**
6. **Auditor:** Document storage account name and timestamp of change

#### **Address VM Disk Compliance**

**Remediator:** For VMs not using managed disks:

1. Navigate to **Virtual machines**
2. Select the non-compliant VM
3. Go to **Disks** section
4. **Note:** Converting to managed disks may require VM downtime
5. **For this exercise:** Document the current configuration and create a remediation plan
6. **Auditor:** Record VM details and planned remediation approach

---

## Step 4: Verify Remediation Success

### 4A: Refresh Compliance Data

1. **Policy Admin:** Wait 10-15 minutes for policy evaluation to update
2. Navigate back to **Policy** > **Compliance**
3. Click **Refresh** on your initiative assignment
4. **Note:** Some evaluations may take up to 24 hours for full refresh

### 4B: Validate Improvements

1. Compare new compliance percentage to baseline from Step 1
2. **Auditor:** Take "after" screenshot of compliance dashboard
3. Document specific improvements:
   - Policies that moved from non-compliant to compliant
   - Number of resources remediated by policy type
   - Overall compliance percentage improvement

### 4C: Handle Remaining Violations

For violations that cannot be immediately resolved:

1. **Document business justification** for delayed remediation
2. **Create remediation timeline** with responsible parties
3. **Consider policy exclusions** if business-justified (with approval)
4. **Escalate complex issues** to appropriate technical teams

---

## Step 5: Collect Audit Evidence

### 5A: Compliance Evidence Package

**Auditor:** Compile a comprehensive evidence folder:

#### **Screenshots Required:**
- Before/after compliance dashboard views
- Individual policy compliance details  
- Remediation task status and results
- Resource configuration before/after changes

#### **Data Exports:**
- Baseline compliance CSV export
- Post-remediation compliance CSV export
- List of remediated resources with timestamps
- Documentation of remaining violations and justifications

### 5B: Remediation Documentation

**Remediator:** Create detailed remediation log:

```
Resource Name: [storage-account-name]
Resource Type: Microsoft.Storage/storageAccounts
Policy Violation: Secure transfer not enabled
Remediation Action: Enabled secure transfer requirement
Date/Time: [timestamp]
Performed By: [your name]
Validation: Verified via Azure Portal configuration page
```

### 5C: Policy Management Evidence

**Policy Admin:** Document policy configuration:

- Screenshot of initiative definition with included policies
- Assignment scope and parameters configured
- Policy enforcement settings (audit vs deny modes)
- Any exclusions or exemptions applied

---

## Step 6: Present Findings

### Team Presentation Preparation (10 minutes)

Each team prepares a 5-minute presentation covering:

#### **Slide 1: Executive Summary**
- Overall compliance improvement (before/after percentages)
- Number of resources remediated
- Critical security issues resolved

#### **Slide 2: Key Findings**
- Most common violation types discovered
- Resources posing highest security risk
- Violations that were easily automated vs requiring manual effort

#### **Slide 3: Remediation Results**
- Successful remediations completed during session
- Issues requiring additional time/resources
- Recommendations for preventing future violations

#### **Slide 4: Lessons Learned & Next Steps**
- What worked well in your remediation approach
- Challenges encountered and how you overcame them
- Recommendations for ongoing compliance monitoring

### Team Presentations (15 minutes total)

**Each team presents for 5 minutes maximum**

---

## 🎯 Lab Completion Checklist

- [ ] Assessed baseline compliance against CIS initiative
- [ ] Identified and categorized non-compliant resources by risk level
- [ ] Executed both automated and manual remediation tasks
- [ ] Verified compliance improvements through dashboard refresh
- [ ] Collected comprehensive audit evidence package
- [ ] Documented all remediation actions with timestamps
- [ ] Presented findings and recommendations to group

## 🏆 Key Takeaways

### **For Compliance Officers:**
- **CIS assessments** provide standardized security baseline measurements
- **Risk-based prioritization** ensures critical issues are addressed first
- **Audit evidence collection** must be systematic and comprehensive
- **Executive reporting** should focus on business impact and risk reduction

### **For Security Officers:**
- **Automated remediation** scales security improvements across large environments
- **Manual remediation** may be required for complex configuration changes
- **Preventive controls** (deny policies) stop future violations before they occur
- **Detective controls** (audit policies) identify existing security gaps

### **For Cloud Engineers:**
- **Policy compliance** provides measurable security and governance metrics
- **Remediation tasks** can automate common configuration fixes
- **Resource tagging** is fundamental for governance and cost management
- **Security configurations** should be validated after any changes

## 🔗 Next Steps

1. **Implement in Production:** Apply lessons learned to your organization's Azure environment
2. **Establish Monitoring:** Set up regular compliance reporting and alerting
3. **Expand Coverage:** Implement additional CIS controls and compliance frameworks
4. **Automate Prevention:** Convert audit policies to deny mode where appropriate

## 🆘 Troubleshooting Tips

**Compliance not updating:**
- Policy evaluation can take 10-15 minutes for recent changes
- Force refresh by clicking "Refresh" on compliance dashboard
- Check that remediated resources are within policy assignment scope

**Remediation tasks failing:**
- Verify managed identity has required permissions on target resources
- Check if resource supports the specific remediation action
- Review activity logs for detailed error messages

**Can't find specific resources:**
- Use resource filters in compliance view to narrow results
- Check resource group and subscription scope of policy assignment
- Verify resource hasn't been deleted or moved to different subscription

---

**🎉 Congratulations!** You've successfully completed a realistic CIS compliance assessment and remediation exercise. You now have hands-on experience with the complete compliance lifecycle: assess, prioritize, remediate, document, and report. These skills are directly applicable to real-world Azure governance scenarios.