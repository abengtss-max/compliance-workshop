# Lab Exercise 3: Resource Graph & Compliance Dashboards

## 📋 Lab 3 Overview

This hands-on lab teaches you to query Azure resources using KQL (Kusto Query Language) through Azure Resource Graph and build interactive compliance dashboards. You'll master persona-specific queries and create comprehensive visualizations for compliance monitoring.

**Duration:** 60 minutes  
**Target Personas:** 🏛️ Compliance Officers + 🔒 Security Officers + ⚙️ Cloud Engineers  
**Focus:** Data discovery, KQL mastery, and interactive dashboard creation

## 🎯 Learning Objectives

By completing this lab, you will:

- Master Azure Resource Graph KQL queries for compliance analysis
- Execute persona-specific queries to extract actionable compliance insights
- Build interactive compliance dashboards with comprehensive visualizations
- Create drill-down capabilities for detailed resource investigation
- Deploy persona-specific dashboard views for different organizational roles

## 📋 Prerequisites

- [ ] **Completed Lab Exercise 1** (Azure Policy & Initiative Setup)
- [ ] **Completed Lab Exercise 2** (CIS Compliance Scenario)
- [ ] Azure subscription with resources and active policy assignments
- [ ] Basic understanding of query languages (helpful but not required)

## 🏢 Real-World Scenario: Contoso Ltd Quarterly Compliance Review

**Background:** Following your successful policy implementation and compliance remediation, the executive team wants comprehensive visibility into the organization's compliance posture. You need to create data-driven dashboards that provide real-time insights for different stakeholders across the organization.

**Challenge:** Build role-specific compliance dashboards that enable:
- **Compliance Officers** to track regulatory adherence and generate reports
- **Security Officers** to monitor security posture and identify threats  
- **Cloud Engineers** to understand technical implementation and optimization opportunities

---

## Step 1: Master Azure Resource Graph

### 1A: Access Azure Resource Graph Explorer

1. Navigate to Azure Portal > **Resource Graph Explorer**
2. **Alternative access:** Portal search > "Resource Graph Explorer"
3. Familiarize yourself with the interface:
   - **Query editor** (top panel)
   - **Results pane** (bottom panel)
   - **Table/Chart toggle** (results toolbar)
   - **Export options** (CSV, Excel, PowerBI)

### 1B: Understanding KQL Basics

**Quick KQL Primer:**
```kql
// Basic resource listing
Resources
| limit 10

// Filter by resource type
Resources
| where type == "microsoft.storage/storageaccounts"

// Project specific columns
Resources  
| project name, type, location, resourceGroup

// Count resources by type
Resources
| summarize count() by type
| order by count_ desc
```

**Test Query:** Run this basic query to verify access:
```kql
Resources
| summarize ResourceCount = count() by type
| order by ResourceCount desc
| limit 10
```

---

## Step 2: Persona-Specific KQL Queries

### 2A: 🏛️ Compliance Officer Query Library

#### **Query 1: Overall Compliance Posture**
```kql
PolicyResources
| where type == "microsoft.policyinsights/policystates"
| extend complianceState = tostring(properties.complianceState)
| summarize 
    TotalResources = count(),
    CompliantCount = countif(complianceState == "Compliant"),
    NonCompliantCount = countif(complianceState == "NonCompliant")
| extend CompliancePercentage = round((CompliantCount * 100.0) / TotalResources, 2)
| project CompliancePercentage, CompliantCount, NonCompliantCount, TotalResources
```

#### **Query 2: Policy Compliance by Initiative**
```kql
PolicyResources
| where type == "microsoft.policyinsights/policystates"
| extend 
    policyDefinitionId = tostring(properties.policyDefinitionId),
    complianceState = tostring(properties.complianceState),
    policySetDefinitionId = tostring(properties.policySetDefinitionId)
| where isnotempty(policySetDefinitionId)
| summarize 
    CompliantResources = countif(complianceState == "Compliant"),
    NonCompliantResources = countif(complianceState == "NonCompliant"),
    TotalResources = count()
    by InitiativeName = tostring(split(policySetDefinitionId, "/")[-1])
| extend ComplianceRate = round((CompliantResources * 100.0) / TotalResources, 1)
| order by ComplianceRate asc
```

#### **Query 3: Resource Tagging Compliance**
```kql
Resources
| extend hasEnvironmentTag = isnotempty(tags["Environment"])
| extend hasCostCenterTag = isnotempty(tags["CostCenter"])  
| extend hasOwnerTag = isnotempty(tags["Owner"])
| summarize 
    TotalResources = count(),
    WithEnvironmentTag = countif(hasEnvironmentTag),
    WithCostCenterTag = countif(hasCostCenterTag),
    WithOwnerTag = countif(hasOwnerTag)
    by resourceGroup
| extend 
    EnvironmentTagCompliance = round((WithEnvironmentTag * 100.0) / TotalResources, 1),
    CostCenterTagCompliance = round((WithCostCenterTag * 100.0) / TotalResources, 1),
    OwnerTagCompliance = round((WithOwnerTag * 100.0) / TotalResources, 1)
| order by EnvironmentTagCompliance desc
```

#### **Query 4: Cost Allocation by Environment**
```kql
Resources
| extend Environment = tostring(tags["Environment"])
| extend CostCenter = tostring(tags["CostCenter"])
| where isnotempty(Environment)
| summarize ResourceCount = count() by Environment, type
| order by Environment, ResourceCount desc
```

#### **Query 5: Policy Exemptions and Exclusions**
```kql
PolicyResources
| where type == "microsoft.authorization/policyexemptions"
| extend 
    exemptionName = name,
    exemptionCategory = tostring(properties.exemptionCategory),
    expiresOn = todatetime(properties.expiresOn),
    policyAssignmentId = tostring(properties.policyAssignmentId)
| project exemptionName, exemptionCategory, expiresOn, policyAssignmentId, resourceGroup
| order by expiresOn asc
```

### 2B: 🔒 Security Officer Query Library

#### **Query 1: Security Center Recommendations Overview**
```kql
SecurityResources
| where type == "microsoft.security/assessments"
| extend 
    recommendationDisplayName = tostring(properties.displayName),
    severity = tostring(properties.metadata.severity),
    status = tostring(properties.status.code)
| summarize count() by severity, status
| order by severity desc
```

#### **Query 2: Network Security Group Analysis**
```kql
Resources
| where type == "microsoft.network/networksecuritygroups"
| extend nsgRules = properties.securityRules
| mvexpand nsgRules
| extend 
    ruleName = tostring(nsgRules.name),
    access = tostring(nsgRules.properties.access),
    direction = tostring(nsgRules.properties.direction),
    sourceAddressPrefix = tostring(nsgRules.properties.sourceAddressPrefix),
    destinationPortRange = tostring(nsgRules.properties.destinationPortRange)
| where access == "Allow" and direction == "Inbound" 
| where sourceAddressPrefix == "*" or sourceAddressPrefix == "Internet"
| project name, resourceGroup, ruleName, destinationPortRange, sourceAddressPrefix
| order by name
```

#### **Query 3: Public IP and Endpoint Exposure**
```kql
Resources
| where type == "microsoft.network/publicipaddresses"
| extend 
    ipAddress = tostring(properties.ipAddress),
    allocationMethod = tostring(properties.publicIPAllocationMethod),
    associatedResource = tostring(properties.ipConfiguration.id)
| project name, resourceGroup, ipAddress, allocationMethod, associatedResource, location
| order by resourceGroup
```

#### **Query 4: Identity and Access Management Gaps**
```kql
AuthorizationResources
| where type == "microsoft.authorization/roleassignments"
| extend 
    principalType = tostring(properties.principalType),
    roleDefinitionId = tostring(properties.roleDefinitionId),
    scope = tostring(properties.scope)
| where principalType == "User"
| summarize AssignmentCount = count() by 
    RoleId = tostring(split(roleDefinitionId, "/")[-1]),
    Scope = case(
        scope contains "/subscriptions/" and scope contains "/resourceGroups/", "Resource Group",
        scope contains "/subscriptions/" and not(scope contains "/resourceGroups/"), "Subscription", 
        "Other"
    )
| order by AssignmentCount desc
```

#### **Query 5: Storage Encryption and Security Status**
```kql
Resources
| where type == "microsoft.storage/storageaccounts"
| extend 
    httpsTrafficOnly = tostring(properties.supportsHttpsTrafficOnly),
    minimumTlsVersion = tostring(properties.minimumTlsVersion),
    allowBlobPublicAccess = tostring(properties.allowBlobPublicAccess),
    encryption = tostring(properties.encryption.services.blob.enabled)
| project 
    name, 
    resourceGroup, 
    httpsTrafficOnly, 
    minimumTlsVersion, 
    allowBlobPublicAccess, 
    encryption,
    location
| order by name
```

### 2C: ⚙️ Cloud Engineer Query Library

#### **Query 1: Resource Health and Availability**
```kql
HealthResources
| where type == "microsoft.resourcehealth/availabilitystatuses"
| extend 
    resourceId = tostring(properties.targetResourceId),
    availabilityState = tostring(properties.availabilityState),
    reasonType = tostring(properties.reasonType)
| summarize count() by availabilityState, reasonType
| order by availabilityState
```

#### **Query 2: Virtual Machine Configuration Compliance**
```kql
Resources
| where type == "microsoft.compute/virtualmachines"
| extend 
    vmSize = tostring(properties.hardwareProfile.vmSize),
    osType = tostring(properties.storageProfile.osDisk.osType),
    managedDisk = isnotempty(properties.storageProfile.osDisk.managedDisk),
    diagnosticsEnabled = isnotempty(properties.diagnosticsProfile)
| project name, resourceGroup, vmSize, osType, managedDisk, diagnosticsEnabled, location
| order by resourceGroup, name
```

#### **Query 3: Storage Account Configuration Analysis**
```kql
Resources
| where type == "microsoft.storage/storageaccounts"
| extend 
    sku = tostring(properties.sku.name),
    kind = tostring(properties.kind),
    accessTier = tostring(properties.accessTier),
    replication = case(
        properties.sku.name contains "LRS", "Locally Redundant",
        properties.sku.name contains "GRS", "Geo Redundant", 
        properties.sku.name contains "ZRS", "Zone Redundant",
        "Other"
    )
| summarize count() by sku, replication, accessTier
| order by count_ desc
```

#### **Query 4: Resource Utilization Overview**
```kql
Resources
| summarize 
    ResourceCount = count(),
    UniqueTypes = dcount(type),
    UniqueLocations = dcount(location)
    by resourceGroup, subscriptionId
| extend SubscriptionName = tostring(split(subscriptionId, "/")[-1])
| order by ResourceCount desc
```

#### **Query 5: Network Topology Analysis**
```kql
Resources
| where type == "microsoft.network/virtualnetworks"
| extend addressSpace = properties.addressSpace.addressPrefixes
| mvexpand addressSpace
| extend 
    vnetName = name,
    cidr = tostring(addressSpace),
    subnets = array_length(properties.subnets)
| project vnetName, resourceGroup, cidr, subnets, location
| order by resourceGroup, vnetName
```

---

## Step 3: Execute and Test Queries

### 3A: Query Execution Workshop

**For each persona section (choose your role):**

1. **Copy and paste** each query into Resource Graph Explorer
2. **Execute the query** and examine results
3. **Export results** using the CSV option for documentation
4. **Modify queries** to match your subscription's resources
5. **Note interesting findings** for dashboard integration

### 3B: Query Customization Exercise

**Customize these base queries for your environment:**

1. **Replace generic tag names** with your organization's tags
2. **Adjust time ranges** if using time-based filters  
3. **Add resource group filters** to focus on specific areas
4. **Modify result columns** to match reporting requirements

---

## Step 4: Build Interactive Compliance Dashboards

### 4A: Create Azure Workbook

1. Navigate to Azure Portal > **Azure Workbooks**
2. Click **+ New** to create a blank workbook
3. **Save as:** "Compliance Dashboard - Multi-Persona"
4. **Resource Group:** Choose existing or create "rg-compliance-workshop"

### 4B: Import Pre-Built Dashboard Template

1. **Download the dashboard template:**
   - Navigate to: `workbooks/workbook-compliance-personas.json`
   - **Alternative:** Import from repository link

2. **Import process:**
   - In Azure Workbooks, click **Advanced Editor** (</> icon)
   - **Clear existing content**
   - **Paste the JSON template** 
   - Click **Apply**

### 4C: Configure Dashboard Parameters

The dashboard includes several parameters you can customize:

1. **Subscription Filter** - Select target subscriptions
2. **Resource Group Filter** - Focus on specific resource groups  
3. **Time Range** - Set evaluation period for compliance data
4. **Environment Tag** - Specify your environment tag values

### 4D: Persona-Specific Dashboard Sections

The imported dashboard contains three main sections:

#### **🏛️ Compliance Officer Dashboard**
- **Overall Compliance KPI tiles**
- **Policy compliance trends** (line chart)
- **Compliance by resource group** (bar chart)
- **Non-compliant resources list** with drill-down links
- **Tagging compliance heatmap**

#### **🔒 Security Officer Dashboard**
- **Security recommendations summary** (pie chart)
- **Critical findings list** with severity indicators
- **Network exposure analysis** (network topology visual)
- **Identity risk indicators** (gauge charts)
- **Quick access links** to Security Center

#### **⚙️ Cloud Engineer Dashboard**
- **Resource health overview** (status indicators)
- **Configuration drift detection** (comparison charts)
- **Performance optimization opportunities** (recommendation lists)
- **Cost optimization insights** (resource utilization metrics)
- **Direct links** to resource configuration pages

---

## Step 5: Dashboard Testing and Validation

### 5A: Interactive Elements Testing

Test each dashboard section:

1. **Parameter filters** - Verify subscription and resource group filtering
2. **Drill-down links** - Click on non-compliant resources to navigate to details
3. **Chart interactions** - Click pie chart segments to filter related data
4. **Export functionality** - Test PDF and Excel export options

### 5B: Data Accuracy Validation

Compare dashboard results with:

1. **Azure Policy compliance pages** - Verify compliance percentages match
2. **Security Center recommendations** - Cross-check security findings
3. **Resource listings** - Validate resource counts and configurations

### 5C: Performance Testing

1. **Load time assessment** - Note query execution speeds
2. **Large dataset handling** - Test with subscriptions containing many resources
3. **Refresh behavior** - Verify auto-refresh and manual refresh functionality

---

## 🎯 Lab Completion Checklist

- [ ] Successfully executed all persona-specific KQL queries in Resource Graph Explorer
- [ ] Exported query results to CSV for documentation
- [ ] Imported and configured the multi-persona compliance dashboard
- [ ] Tested all interactive elements and drill-down capabilities  
- [ ] Validated dashboard data accuracy against Azure Portal sources
- [ ] Customized dashboard parameters for your subscription environment
- [ ] Identified actionable compliance and security insights from the data

## 🏆 Key Takeaways

### **For Compliance Officers:**
- **Resource Graph queries** provide real-time compliance visibility across large Azure environments
- **Automated dashboards** enable continuous monitoring without manual report generation
- **Tag-based governance** is essential for effective compliance tracking and cost allocation
- **Policy exemptions** require careful tracking and regular review for audit purposes

### **For Security Officers:**
- **KQL queries** can identify security misconfigurations and policy violations at scale
- **Network security analysis** reveals potential attack vectors and overly permissive rules
- **Identity and access queries** help identify privilege escalation risks and access anomalies
- **Integration with Security Center** provides comprehensive security posture visibility

### **For Cloud Engineers:**
- **Resource Graph** is essential for infrastructure inventory and configuration management
- **Performance queries** identify optimization opportunities for cost and efficiency
- **Configuration drift detection** helps maintain compliance and security standards
- **Automated monitoring** reduces manual effort while improving accuracy and coverage

## 🔗 Next Steps

1. **Schedule regular dashboard reviews** - Set up weekly/monthly compliance review meetings
2. **Create automated alerts** - Configure Azure Monitor alerts based on query results
3. **Expand query library** - Develop custom queries for organization-specific requirements
4. **Integrate with CI/CD** - Include compliance checks in deployment pipelines

## 🆘 Troubleshooting Tips

**Query execution errors:**
- Verify you have Reader access to target subscriptions and resources
- Check that Resource Graph permissions are properly configured
- Ensure queries are syntactically correct (semicolons, brackets, etc.)

**Dashboard display issues:**
- Refresh the workbook if data appears stale or empty
- Verify subscription and resource group parameters are set correctly
- Check that the target resources exist in the selected scope

**Performance issues:**
- Add resource group or subscription filters to limit query scope
- Consider time range restrictions for large environments
- Use summarization and aggregation to reduce result set sizes

---

**🎉 Congratulations!** You've mastered Azure Resource Graph queries and built comprehensive compliance dashboards. You now have the tools to provide data-driven compliance visibility and insights across your entire Azure environment. The queries and dashboards you've created can be adapted and extended for your organization's specific compliance and governance requirements.