# Enhancing CI/CD Workflows: Integrating AWS Access Analyzer for IAM Security

This project revolves around the idea - **_Security + Automation_**  

We aim to elevate both efficiency and security within deployment processes by integrating a specialized tool, `cfn-policy-validator` , into a cohesive CI/CD Pipeline. This integration _**automates IAM Policy Validation Tests**_, ensuring **_IAM security is inherently a part of every deployment cycle_**, while automatically halting the build, in the event of its failure.  

---> Robust Security & Compliance throughout the Infrastructure


## What are the Core Components here?

 - **_<ins>CodeCommit</ins> -_**
This actually enables us to store our source code in **_secure, private Git-based Repos._**  
----> It's **_a starting point of my pipeline_**,  each time a commit or a modification is made to the Source Code, it acts as a trigger, for subsequent steps in the pipeline. 
  
- **_<ins>CodeBuild</ins> -_**
**_Automates build and test._** ---> it compiles the source code, links the modules, **_bundles necessary libraries into a single standalone package_**, or yeah, you may also call it an **_'artifact'_**

- **_<ins>CodePipeline</ins> -_**
Our orchestrator. </br>
It **_integrates all of the AWS Services together cohesively_,** enabling managed CI and CD Service. It **_automates software releases_**, making deployments quicker, more frequent and reliable.

- **_<ins>CloudFormation</ins> -_** Enables us to manage and provision resources in the Cloud Infrastructure, 
We can then define and deploy resources in a much more reliable and repeatable manner 

- **_<ins>IAM Access Analyzer</ins> -_**



## Access Analyzer - Quick Walkthrough

- Helps identify resources exposed to the public internet
- Cross-Account Resource Access
- Unused Access Control Policies ( This might lead to unintentional Privilege Escalation )
- Automated Policy Generation through AWS CloudTrail Logs
- Policy Validation against IAM Best Practices - ( Stringent Policy Checks for a compliant architecture )





