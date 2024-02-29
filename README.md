# Enhancing CI/CD Workflows: Integrating AWS Access Analyzer for IAM Security

This project revolves around the idea - **_Security + Automation_**  

We aim to elevate both efficiency and security within deployment processes by integrating a specialized tool, `cfn-policy-validator` , into a cohesive CI/CD Pipeline. This integration _**automates IAM Policy Validation Tests**_, ensuring **_IAM security is inherently a part of every deployment cycle_**, while automatically halting the build, in the event of its failure.  

--> Robust Security & Compliance throughout the Infrastructure


## What are the Core Components here?

- _<ins>CodeCommit</ins>_:- </br>
 This actually enables us to store our source code in **secure, private Git-based Repos.** </br> It's **a starting point of my pipeline**, each time a commit or a modification is made to the Source Code, it <ins>acts as a trigger, for subsequent steps in the pipeline.</ins>
  
- _<ins>CodeBuild</ins>_:-</br>**Automates build and test.** It compiles the source code, links the modules, <ins>bundles necessary libraries into a single standalone package</ins>, or yeah, you may also call it an 'artifact.'

- _<ins>CodePipeline</ins>_:- 'Our orchestrator' </br>
It **integrates all of the AWS Services together cohesively**, enabling managed CI and CD Service. </br>
   <ins>Automates software releases</ins>, making deployments quicker, more frequent, and reliable.

- _<ins>CloudFormation</ins>_:- </br>Manages and provisions resources in the Cloud Infrastructure, </br> We can then define and <ins>**deploy resources in a much more reliable and repeatable manner**</ins> 

- _<ins>Access Analyzer Integration</ins>_:- 'Our IAM Fortifier'  </br> **Uses ML Algorithms to analyse if the policies attached to resources are overtly privileged** / or if they need to be pruned down. Also, helps check if the resources are exposed to the internet

</br>


## Key Tangibles at a Glance

- **Streamlined Policy Management**: Scaling simplicity -> embedding IAM security  within every deployment cycle.

- **Security Standards**: Each deployment  conforms to predefined security benchmarks -> the essence of Shift-Left Security.

- **Optimized Deployment**: = Fast + Efficient + Secure

- **Increased Compliance**: Policy validation checks -> compliance & reducing risks in IAM configurations.

</br>

## Insights into Access Analyser - And how it aligns with the overarching Project Goals?

![image](https://github.com/TanishkaMarrott/Integrating-AWS-IAM-Access-Analyzer-in-a-CI-CD-Pipeline/assets/78227704/13167157-1519-4296-a575-4dbbae7e1368)


 - _Unwanted Public Exposure_:- Identifies resources **_accessible to an external entity_**. </br>

 - _Cross-Account Resource Access_:- Helps identify ***resources that have been shared with accounts outside our organisation***, and remediates broad access. </br>

 - _Unused Permissions / PrivEsc Risks_:-  **_'Redundant permissions are a big no'_**. </br> Enables us to appropriately lock down policies. </br>

- _Smart Policy Recommendations_:- Thanks to AWS CloudTrail, </br> Access Analyzer helps get **_smart policy recommendations_** based on access activity. </br>

- _Security Best Practices_:- Custom Policy Checks help **_validate against AWS's stringent standards._** </br> ---> _If it's not compliant, it's not going through._ </br>

- _Automated Policy Generation_:- **_Generates fine-grained IAM policies_** based on access activity in your AWS CloudTrail logs. </br>


> _Is there a way I can merge the two? </br> Enter CFN Policy Validator_

## Integrating CFN Policy Validator into our CI/CD Pipeline 


The IAM Policy Validator for AWS CloudFormation (`cfn-policy-validator`) is a command-line tool, that **_parses resource-based and identity-based policies in CF Templates_**.

 It runs the policies through two types of Access Analyser APIs:

- The `ValidatePolicy` API to validate IAM Policies and SCPs against IAM Policy grammar and IAM Best Practices
- The `AccessPreview` APIs to determine if a resource-based policy allows Public or Cross-Account Access.

### How does it actually work?

The `cfn-policy-validator` tool has two actions that it can perform - `parse` and `validate`

`parse` - it walks through each CloudFormation resource in the template, **_extracts identity-based & resource-based IAM policies_**. While parsing a template, the tool **_resolves CloudFormation intrinsic functions  and pseudo parameters_**. 

The `validate` action parses your template, **_passes the identity-based and resource-based IAM policies to Access Analyzer_**, & **_reports these findings_**

```bash
cfn-policy-validator parse --template-path cfn-policy-validator/parse-template.json --region us-east-1
```

























