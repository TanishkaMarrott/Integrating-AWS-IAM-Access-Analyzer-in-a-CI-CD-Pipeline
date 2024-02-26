# Enhancing CI/CD Workflows: Integrating AWS Access Analyzer for IAM Security

This project revolves around the idea - **_Security + Automation_**  

We aim to elevate both efficiency and security within deployment processes by integrating a specialized tool, `cfn-policy-validator` , into a cohesive CI/CD Pipeline. This integration _**automates IAM Policy Validation Tests**_, ensuring **_IAM security is inherently a part of every deployment cycle_**, while automatically halting the build, in the event of its failure.  

---> Robust Security & Compliance throughout the Infrastructure


## What are the Core Components here?

- **_CodeCommit_** -
This actually enables us to store our source code in **_secure, private Git-based Repos._**  
It's **_a starting point of my pipeline_**,  each time a commit or a modification is made to the Source Code, it acts as a trigger, for subsequent steps in the pipeline. 
  
- **_CodeBuild_** -  It **_automates the build and test process_**   - it compiles the source code, links the modules, **_bundles necessary libraries into a single standalone package_**, or yeah, you may also call it an **_'artifact'_**

- **_CodePipeline_** - Our orchestrator. It integrates all of the AWS Services together cohesively, enabling managed CI and CD Service. It automates software releases, making deployments quicker, more frequent and reliable. 

- **_IAM Access Analyzer_**

- 


- 
- 



## Access Analyzer - Quick Walkthrough

- Helps identify resources exposed to the public internet
- Cross-Account Resource Access
- Unused Access Control Policies ( This might lead to unintentional Privilege Escalation )
- Automated Policy Generation through AWS CloudTrail Logs
- Policy Validation against IAM Best Practices - ( Stringent Policy Checks for a compliant architecture )





