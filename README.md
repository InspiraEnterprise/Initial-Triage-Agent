# Initial-Triage-Agent
Building a custom Microsoft Security Copilot agent to perform deterministic, analyst-grade initial triage for Microsoft Sentinel and Microsoft Defender XDR incidents.

# Description
The Initial Triage Agent is a contract-locked, deterministic, read-only Microsoft Security Copilot custom agent designed to perform analyst-grade initial triage for incidents in Microsoft Sentinel and Microsoft Defender XDR. The agent automatically detects the source system, retrieves available incident context, evaluates current evidence and historical incident patterns, and produces a fixed six-section triage output suitable for Logic App automation, incident task injection, and Copilot chat execution.

The agent is built to behave like an experienced L3/L4 SOC analyst by applying evidence-based reasoning, explicit contradiction handling, and conservative disposition logic. It does not rely on external enrichment and uses only permitted Microsoft Sentinel or Defender XDR incident data from the detected source system.

# Business Requirements

•  Standardized Initial Triage for SOC Operations: The agent provides a consistent and deterministic triage workflow for Microsoft Sentinel and Defender XDR incidents, reducing analyst-to-analyst variance and improving operational consistency across L1, L2, and L3 SOC teams.

•  Faster Incident Dispositioning: By automatically retrieving incident context, correlating evidence, and evaluating historical patterns, the agent helps analysts quickly determine whether an incident is likely malicious, confirmed benign, or requires escalation.

•  Automation-Ready Output for SOC Workflows: The agent returns a strict six-section output format that is compatible with Logic Apps, incident task injection, and Copilot chat, enabling seamless integration into existing SOC automation pipelines.

•  Improved Analyst Efficiency and Quality Control: The agent helps reduce triage fatigue, enforces evidence-based decisioning, and improves the quality and repeatability of initial incident assessments across Microsoft security operations workflows.

•  Read-Only and Audit-Friendly Security Model: The agent operates in strict read-only mode, making it safe for production use in investigation workflows without risk of changing incidents, comments, tasks, rules, or triggering containment actions.

# Prerequisites

•  An active Microsoft Security Copilot environment

•  Access to Microsoft Security Store / Security Copilot custom agents

•  An active Microsoft Sentinel workspace

•  Access to Microsoft Defender XDR (recommended for dual-source support)

•  Required Security Copilot skillsets enabled in the workspace:
   - Generic
   - Fusion
   - Sentinel
   - M365

•  Read permissions to Microsoft Sentinel incidents and related incident context

•  Read permissions to Microsoft Defender XDR incidents and related incident context

•  Appropriate Security Copilot workspace access for the user or service context running the agent

# Setup Guide
The following provides step-by-step instructions to deploy and configure the Initial Triage Agent:

**Step 1: Access Microsoft Security Copilot**

• Sign in to the Microsoft Security Copilot portal.

• Navigate to the Microsoft Security Store / Agent catalog.

• Search for **Initial Triage Agent**.

• Select the custom agent published by **Inspira Enterprise**.

**Step 2: Add the Agent**

• Click on **Set up**.

• Review the agent details and supported platforms.

• Begin the installation and configuration flow.

**Step 3: Grant Required Permissions**

• Approve all required permissions requested during setup.

• Ensure the workspace has access to:
  - Microsoft Sentinel
  - Microsoft Defender XDR
  - Required Security Copilot skillsets and plugins

• Confirm the user or service context has the required read permissions for incident retrieval and analysis.

**Step 4: Sign In with an Authorized User**

• Sign in using a user account that has the necessary access to:
  - Microsoft Sentinel incidents
  - Microsoft Defender XDR incidents
  - Security Copilot workspace resources

• Verify the user has sufficient permissions to execute Security Copilot custom agents in the target workspace.

**Step 5: Validate Required Skillsets**

Ensure the following skillsets are available and enabled in the workspace before running the agent:
• Generic  
• Fusion  
• Sentinel  
• M365  

**Step 6: Complete Configuration**

• Finish the setup process.

• Confirm that the Initial Triage Agent is visible and enabled in the workspace.

• Once configuration is complete, you can either run the agent manually or configure it for automated execution through supported workflows.

# Running the Agent
After the agent has been configured, you can run it using one of the following methods:

**Option 1: Run the Agent Manually**

• Open the **Initial Triage Agent**.

• Select **Run it one time without a trigger**.

• Provide the required input:
  - **IncidentId** = Microsoft Sentinel Incident ID or Defender XDR Incident ID

• Review the input values.

• Click **Submit**.

• The agent will automatically:
  - Detect whether the incident belongs to Microsoft Sentinel or Defender XDR
  - Retrieve the incident data from the correct source
  - Perform deterministic triage
  - Return the six-section structured output

**Option 2: Run the Agent Automatically on a Trigger**

• Open the **Initial Triage Agent**.

• Select **Run it automatically on the trigger**.

• Configure the automation or trigger path that will provide the required **IncidentId** input.

• Save the trigger configuration.

• Use this mode when integrating the agent into:
  - Logic App automation
  - Incident task injection workflows
  - Automated SOC triage pipelines
  - Event-driven Security Copilot processes

# Input Requirements

•  **IncidentId** (Required)

•  Accepted values:
   - Microsoft Sentinel Incident ID
   - Microsoft Defender XDR Incident ID

•  The agent validates the IncidentId before processing begins.

•  The user does not need to specify the source system manually.

# How the Agent Works

The Initial Triage Agent automatically performs source detection before triage begins:

•  First, it checks Microsoft Sentinel for the provided IncidentId.

•  If found in Sentinel, the agent uses Microsoft Sentinel as the source system.

•  If not found in Sentinel, the agent checks Microsoft Defender XDR.

•  If found in Defender XDR, the agent proceeds with Defender XDR data.

•  If the incident is found in both systems, Microsoft Sentinel is used as the primary source.

•  If the incident is not found in either system, the agent returns a standardized not-found response.

# Output Structure

Every successful execution returns exactly seven sections in a fixed and deterministic order:

1. Verdict

2. Confidence Score

3. Classification Reasoning
4. Live Entity Investigation Summary

5. Critical Evidence Observed

6. Attack Timeline

7. Recommended Actions

This output format is designed for direct use in:

•  Security Copilot chat responses

•  Microsoft Sentinel incident task injection

•  Logic App automation outputs

•  SOC analyst workflows requiring consistent and auditable triage formatting

# Verdict Types

The agent will classify incidents using one of the following deterministic verdict values:

•  True Positive - Confirmed Breach

•  True Positive - Likely Malicious

•  False Positive - Suspicious but Benign

•  False Positive - Confirmed Benign

# Security & Architecture Guardrails

The Initial Triage Agent is governed by strict architecture guardrails:

•  Read-Only Enforcement: The agent never creates, updates, or deletes incidents, comments, tasks, rules, or playbooks.

•  No Containment Actions: The agent does not isolate devices, disable users, revoke sessions, or block indicators.

•  No Fabrication: The agent never invents alerts, entities, comments, timelines, classifications, or evidence.

•  No External Enrichment: Only Microsoft Sentinel or Defender XDR data from the detected source is used.

•  No Mixed-Source Analysis: The agent does not combine Sentinel and Defender XDR data for the same execution.

•  No Placeholder Output: The agent avoids generic filler such as [TBD], N/A, or blank sections.

# Supported Use Cases

•  Initial incident triage for Microsoft Sentinel incidents

•  Initial incident triage for Microsoft Defender XDR incidents

•  SOC analyst assist for L1 / L2 / L3 workflows

•  Logic App-based automated triage

•  Incident task generation with structured triage summaries

•  Standardized triage comments for repeatable investigations

•  Deterministic incident assessment in Security Copilot chat

# Solution Insights: Agent Workflow
![image](https://github.com/user-attachments/assets/REPLACE-WITH-YOUR-IMAGE-LINK)

# Additional Notes

•  The agent is optimized for deterministic, evidence-based, and audit-friendly SOC triage.

•  Historical incidents are used only as a bounded supporting signal and never as standalone proof of maliciousness.

•  Closed or resolved incidents are still supported and can be analyzed.

•  The agent is suitable for production environments where safe, read-only investigation support is required.

•  The output format is intentionally strict to support automation compatibility and downstream SOC integrations.
