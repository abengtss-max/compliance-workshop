# Lab Exercise 1A: Azure Policy & Initiative Setup

## 📋 Overview

This hands-on lab teaches the fundamentals of implementing CIS (Center for Internet Security) benchmark compliance using Azure Policy and initiatives. You'll learn to create custom policies, build CIS-aligned initiatives, and understand policy enforcement through practical exercises.

**Duration:** 60 minutes  
**Target Personas:** 🏛️ Compliance Officers + 🔒 Security Officers + ⚙️ Cloud Engineers  
**Focus:** CIS Azure Foundations Benchmark v2.0.0  
**Workshop Time:** 10:00 - 11:00 AM

## 🎯 Learning Objectives

By completing this lab, you will:

- Navigate Azure Policy and understand CIS benchmark alignment
- Create custom Azure Policy definitions for compliance controls
- Build and assign Policy initiatives incorporating CIS policies
- Test policy enforcement and observe compliance effects
- Review compliance status using Azure Policy dashboards

## 📋 Prerequisites

- [ ] Azure subscription with **Contributor** or **Policy Contributor** access
- [ ] Basic understanding of Azure Portal navigation
- [ ] Familiarity with CIS benchmark concepts (overview provided in presentation)

---

## Step 1: Access Azure Policy

1. **Sign in to the Azure Portal**
   - Navigate to [portal.azure.com](https://portal.azure.com)
   - Sign in with your Azure account

2. **Open Azure Policy Service**
   - In the search bar at the top, type **"Policy"**
   - Select **Policy** from the results
   - You'll see the Policy overview dashboard with compliance summary

## Step 2: Create a Custom Policy Definition

We'll create a CIS-aligned policy that requires specific tags on all resources for compliance tracking.

1. **Navigate to Definitions**
   - In the left menu, click **Definitions**
   - Click **+ Policy definition**

2. **Configure the Policy Definition**
   - **Definition location:** Select your subscription
   - **Name:** `CIS-Enforce-Tag-on-Resources`
   - **Description:** `CIS: Enforce mandatory tags on all resources for compliance tracking and audit purposes`
   - **Category:** Create new category: **"Compliance"**

3. **Create the Policy Rule**
   
   Copy and paste this JSON into the **Policy rule** field:

   ```json
   {
     "if": {
       "allOf": [
         {
           "field": "type",
           "notEquals": "Microsoft.Resources/subscriptions/resourceGroups"
         },
         {
           "field": "tags['Environment']",
           "exists": "false"
         }
       ]
     },
     "then": {
       "effect": "[parameters('effect')]"
     }
   }
   ```

4. **Add Parameters Section**
   
   Copy and paste this JSON into the **Parameters** field:

   ```json
   {
     "effect": {
       "type": "String",
       "metadata": {
         "displayName": "Effect",
         "description": "The effect determines what happens when the policy rule is evaluated to match"
       },
       "allowedValues": [
         "audit",
         "deny",
         "disabled"
       ],
       "defaultValue": "audit"
     }
   }
   ```

5. **Save the Policy**
   - Click **Save**
   - Your custom CIS-aligned policy is now created

## Step 3: Create a Policy Initiative (Set)

1. **Navigate to Initiative Definitions**
   - In the left menu, click **Definitions**
   - Click **+ Initiative definition**

2. **Configure the Initiative**
   - **Definition location:** Select your subscription
   - **Name:** `CIS-Baseline-Initiative`
   - **Description:** `CIS Azure Foundations Benchmark baseline controls for compliance assessment`
   - **Category:** Select **"Compliance"**

3. **Add Policies to Initiative**
   - Click **Add policy definition(s)**
   - **Search for your custom policy:** Type "CIS-Enforce-Tag" and add your policy
   - **Add built-in CIS policies:** Search for "CIS" and select these policies:
     - **"Audit VMs that do not use managed disks"**
     - **"Storage accounts should restrict network access"**
     - **"Secure transfer to storage accounts should be enabled"**
     - **"Audit usage of custom RBAC rules"**
   - Click **Add** for each selected policy
   - Click **Save**

4. **Save the Initiative**
   - Review the policies in your initiative
   - Click **Save**

## Step 4: Assign the Initiative

1. **Navigate to Assignments**
   - In the left menu, click **Assignments**
   - Click **+ Assign initiative**

2. **Configure the Assignment**
   - **Scope:** Select your subscription (or specific resource group for testing)
   - **Exclusions:** Leave empty
   - **Initiative definition:** Search for "CIS-Baseline-Initiative" and select it
   - **Assignment name:** `CIS Baseline Compliance Assessment`
   - **Description:** `CIS Azure Foundations Benchmark compliance assessment and enforcement`
   - **Policy enforcement:** **Enabled**

3. **Configure Parameters**
   - For your custom tag policy, set **Effect:** to **"audit"** (for initial assessment)
   - Leave other policies with default settings

4. **Complete the Assignment**
   - Click **Review + create**
   - Click **Create**

## Step 5: Test Policy Enforcement

1. **Create a Test Resource Without Required Tags**
   - Go to **Storage accounts** in the Azure Portal
   - Click **+ Create**
   - Configure basic settings:
     - **Subscription:** Your subscription
     - **Resource group:** Create new or select existing
     - **Storage account name:** Choose a unique name
   - **Important:** Skip the **Tags** section (don't add Environment tag)
   - Click **Review + create** then **Create**

2. **Observe Policy Effect**
   - Since we set the effect to "audit", the resource will be **created**
   - The policy will mark it as **non-compliant** for monitoring
   - Check deployment notifications for any policy-related messages

3. **Create a Compliant Resource**
   - Create another storage account
   - This time, in the **Tags** tab, add:
     - **Key:** `Environment`
     - **Value:** `Production`
   - Complete the deployment - this will be compliant

## Step 6: Review Compliance Dashboard

1. **Check Initiative Compliance**
   - Navigate to **Policy** > **Compliance**
   - Look for your "CIS Baseline Compliance Assessment" assignment
   - Note the overall compliance percentage

2. **Drill Down into Results**
   - Click on your initiative assignment
   - Review compliance by individual policies
   - Click on specific policies to see:
     - **Compliant resources** (green)
     - **Non-compliant resources** (red)
     - **Not applicable resources** (gray)

3. **Analyze Compliance Data**
   - Take note of which resources are non-compliant
   - Document the specific policy violations
   - This data will be used in Lab Exercise 1B (CIS Compliance Scenario)

---

## 🎯 Lab Completion Checklist

- [ ] Successfully accessed Azure Policy service
- [ ] Created custom CIS-aligned policy definition
- [ ] Built initiative with custom and built-in CIS policies
- [ ] Assigned initiative to subscription/resource group
- [ ] Tested policy enforcement with compliant/non-compliant resources
- [ ] Reviewed initial compliance dashboard and documented findings

## 🏆 Key Takeaways

### **For Compliance Officers:**
- **CIS benchmarks** provide industry-standard security baselines for Azure
- **Policy initiatives** group related controls for comprehensive assessment
- **Compliance dashboards** offer real-time visibility into organizational posture

### **For Security Officers:**
- **Preventive controls** (deny effects) stop violations before they occur
- **Detective controls** (audit effects) identify existing violations for remediation
- **Risk-based prioritization** focuses effort on highest-impact security gaps

### **For Cloud Engineers:**
- **Policy definitions** are JSON-based and version-controlled
- **Initiative assignments** can be scoped to specific environments or applications
- **Parameter flexibility** allows policies to be reused across different contexts

## 🔗 Next Steps

**Proceed immediately to [Lab Exercise 1B: CIS Compliance Scenario](./lab-01b-cis-compliance-scenario.md)** where you'll use the policies and compliance data from this exercise to simulate a real-world compliance assessment and remediation scenario.

## 🆘 Troubleshooting Tips

**Policy not evaluating:**
- Allow 10-15 minutes for initial policy evaluation
- Check policy assignment scope matches target resources
- Verify policy syntax and parameters are correct

**Can't find CIS policies:**
- Search for "audit" or "secure" if "CIS" search doesn't return results
- Look in the "Security Center" category for security-related policies
- Try searching for specific resource types like "storage" or "virtual machine"

**Compliance data not showing:**
- Refresh browser and clear cache
- Verify you have Reader access to Policy compliance data
- Check that resources exist within the policy assignment scope

---

**🎉 Ready for Part 2!** You've successfully set up CIS-aligned policies and initiatives. The compliance data you've generated will be essential for the next exercise where you'll remediate violations and prepare audit evidence.