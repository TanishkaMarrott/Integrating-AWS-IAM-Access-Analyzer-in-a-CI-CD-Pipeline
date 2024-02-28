# Enhancing CI/CD Workflows: Integrating AWS Access Analyzer for IAM Security

This project revolves around the idea - **_Security + Automation_**  

We aim to elevate both efficiency and security within deployment processes by integrating a specialized tool, `cfn-policy-validator` , into a cohesive CI/CD Pipeline. This integration _**automates IAM Policy Validation Tests**_, ensuring **_IAM security is inherently a part of every deployment cycle_**, while automatically halting the build, in the event of its failure.  

---> Robust Security & Compliance throughout the Infrastructure


## What are the Core Components here?
 
 - _<ins>CodeCommit</ins> -_ This actually enables us to store our source code in **_secure, private Git-based Repos._**  </br>  It's **_a starting point of my pipeline_**,  each time a commit or a modification is made to the Source Code, it <ins>acts as a trigger, for subsequent steps in the pipeline. </ins>
  
- _<ins>CodeBuild</ins> -_ **_Automates build and test._**  it compiles the source code, links the modules, <ins>bundles necessary libraries into a single standalone package</ins>, or yeah, you may also call it an **_'artifact'_**

- **_<ins>CodePipeline</ins> -_**_'Our orchestrator'_ </br>
It **_integrates all of the AWS Services together cohesively_,** enabling managed CI and CD Service. </br>
   <ins>Automates software releases</ins>, making deployments quicker, more frequent and reliable.

- **_<ins>CloudFormation</ins> -_** **_Manages and provisions resources_** in the Cloud Infrastructure, </br> We can then define and <ins>deploy resources in a much more reliable and repeatable manner_</ins> 

- **_<ins> Access Analyzer</ins> -_** '_Our IAM Fortifier_'  </br> Uses ML Algorithms to analyse if the policies attached to **_resources are overtly privileged_** / or if they need to be pruned down. Also, helps check if the resources are **_exposed to the internet_**



## How does Access Analyser bolster IAM Security?

A quick preview for our non-security folks!

1 - **_Public Exposure_**:- AA identifies resources which are accessible to an external entity. </br>

2 - **_Cross-Account Resource Access_**:- Helps identify resources that have been shared with accounts outside our organisation. </br>

3 - **_Policy Optimization_**:- Redundant permissions are a big no. Enables us to appropriately lock down Policies. </br>

4 - **_Automated Insights_**:- Thanks to AWS CloudTrail, Access Analyzer helps get **_smart policy recommendations_** based on access activity. </br>

5 - **_Best Practices_**:- Custom Policy Checks help validate against AWS's stringent standards. If it's not compliant, it's not going through. </br>

6 - **_Policy Generation_**:- Generates IAM policies based on access activity in your AWS CloudTrail logs. </br>








