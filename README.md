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


 &rarr; _Unwanted Public Exposure_:- Identifies resources **_accessible to an external entity_**. </br>

  &rarr; _Cross-Account Resource Access_:- Helps identify ***resources that have been shared with accounts outside our organisation***, and remediates broad access. </br>

  &rarr; _Unused Permissions / PrivEsc Risks_:-  **_'Redundant permissions are a big no'_**. </br> Enables us to appropriately lock down policies. </br>

 &rarr; _Smart Policy Recommendations_:- Thanks to AWS CloudTrail, </br> Access Analyzer helps get **_smart policy recommendations_** based on access activity. </br>

 &rarr; _Security Best Practices_:- Custom Policy Checks help **_validate against AWS's stringent standards._** </br> ---> _If it's not compliant, it's not going through._ </br>

 &rarr; _Automated Policy Generation_:- **_Generates fine-grained IAM policies_** based on access activity in your AWS CloudTrail logs. </br>

</br>

>  Why not directly use Access Analyzer APIs to scan CF templates?
</br>

## The Pain-Point

I was leading the Cloud Security Team at one of my previous companies.    
  
Reducing the use of the wildcard (`*`) by Developer Teams, in the resource Section of IAM Policies, was really challenging.   
    
This was primarily because we relied on the **ARNs** of resources, which were only available to us _**post-deployment**_. This meant that we lacked a mechanism to **preprocess the CF templates** for security analysis by **Access Analyzer**.

A notable limitation of **Access Analyzer** is its inability to **parse templates and resolve CloudFormation's dynamic parameters**. This shortfall made it difficult to ensure our policies were as tight and secure as possible before deployment.

</br>

## The Solution - Integrating CFN Policy Validator into our CI/CD Pipeline 

A heads-up here... 

> It's absolutely crucial that we have a mechanism in place that is capable of resolving dynamic references, Access Analyser cannot parse Pseudo parameters and Intrinsic Functions

The former is some reference to dynamic values available during runtime, for example, `Fn::Sub`, `Fn::GetAtt` Dynamic Referencing, conditionals etc
While the latter refers to some static, predefined, maybe AWS-specific values, like AWS Account, AWS Region and so on.

</br>

I came across this solution at _**AWS: ReInforce 2022**._ It's a conference aimed at making super-robust, secure solutions in the Cloud.

IAM Policy Validator for AWS CloudFormation (`cfn-policy-validator`)...    
It's a command-line tool, that **_parses resource-based and identity-based policies in CF Templates_**. It runs the policies through two types of Access Analyser APIs:

- The `ValidatePolicy` API -- to  validate IAM Policies and SCPs against IAM Policy grammar and IAM Best Practices
- The `AccessPreview` APIs -- to determine if a resource-based policy allows Public or Cross-Account Access.

### How does it actually work?

The `cfn-policy-validator` tool has two actions that it can perform - `parse` and `validate`

`parse` - it walks through each CloudFormation resource in the template, **_extracts identity-based & resource-based IAM policies_**. While parsing a template, the tool **_resolves CloudFormation intrinsic functions  and pseudo parameters_**. 

The `validate` action parses your template, **_passes the identity-based and resource-based IAM policies to Access Analyzer_**, & **_reports these findings_**

#### Usage

```bash
sudo pip3 install cfn-policy-validator
cfn-policy-validator parse --template-path cfn-policy-validator/parse-template.json --region us-east-1
```

























