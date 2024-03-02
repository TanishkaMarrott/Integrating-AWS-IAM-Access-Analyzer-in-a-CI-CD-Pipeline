# Enhancing CI/CD Workflows: Integrating AWS Access Analyzer for IAM Security

This project revolves around the idea - **_Security + Automation_**  

We aim to elevate both efficiency and security within deployment processes by integrating a specialized tool, `cfn-policy-validator`  into a cohesive CI/CD Pipeline. This integration _**automates IAM Policy Validation Tests**_, such that **_IAM security is inherently a part of every deployment cycle_**, while automatically halting the build, in the event of its failure.  

--> Robust Security & Compliance throughout the Infrastructure

----

## Core Services we've used:-

- CodeCommit </br>
  - Store our source code in **secure, private Git-based Repos.** </br> It's **a starting point of my pipeline**, each time a commit is made to the Source Code, it <ins>acts as a trigger, for subsequent steps in the pipeline.</ins>
  
- CodeBuild </br>
  - **<ins>--> Automates build and test.</ins>** Compiles the source code, bundles up all necessary libraries + exec code into a shippable package</ins>, or yeah, you may also call it an 'artifact.'

- CodePipeline  </br>
  - 'Our orchestrator'. Integrates all of the services cohesively. </br>
   <ins>Automates software releases</ins>, deployments = quicker + more frequent + reliable.

- CloudFormation </br>
  - IaC. We can define and <ins>**deploy resources in a much, much reliable & repeatable manner**</ins> 

- Access Analyzer  </br>
  - **Uses ML Algorithms to analyse overly privileged resources.** And if they're exposed to the public internet.

</br>

## Key Tangibles at a Glance

- **Streamlining Policy Management:**: Scaling _simplicity_ --> Embedding IAM security within every deployment cycle.

- **Complying to Security Standards:**: Each deployment conforms to predefined security benchmarks --> the essence of Shift-Left Security.

- **Optimizing Deployment:** = Fast + Efficient + Secure

- **Increasing Compliance:** Policy validation checks -> compliance & reducing risks in IAM configurations.

</br>

## Insights into Access Analyser - And how it aligns with the overarching Project Goals?

![image](https://github.com/TanishkaMarrott/Integrating-AWS-IAM-Access-Analyzer-in-a-CI-CD-Pipeline/assets/78227704/13167157-1519-4296-a575-4dbbae7e1368)


Access Analyzer plays a critical role in identifying **Unwanted Public Exposure** by identifying resources that are accessible to external entities. 

It also addresses **Cross-Account Resource Access**, identifying resources shared with external accounts and tightening access controls accordingly.

The tool  manages **Unused Permissions and Privilege Escalation Risks** by removing unnecessary permissions, --> the principle of least privilege. Through **Smart Policy Recommendations** from AWS CloudTrail data, it refines IAM policies for better security and efficiency.

**Security Best Practices** are maintained through policy validations against AWS standards. 


</br>

>  _Why not directly use Access Analyzer APIs to scan CF templates?_
</br>
--

## The Pain-Point

### _Practical Challenges in Policy Validation_
I was leading the Cloud Security Team at one of my previous companies.    
  
Reducing the use of the wildcard (`*`) by Developer Teams, in the resource Section of IAM Policies, was really challenging.   

> This was primarily because we relied on the **ARNs** of resources, which were only available to us _**post-deployment**_. This meant that we lacked a mechanism to **preprocess the CF templates** for security analysis by **Access Analyzer**.

### _Where does Access Analyser fail?_

A heads-up here...    
**It's absolutely crucial that we have a mechanism in place capable of resolving Pseudo parameters & Intrinsic Functions.**

**Pseudo Parameters** refers to some static, predefined, maybe AWS-specific values, like AWS Account, AWS Region and so on.
While **Intrinsic Functions** are actually some dynamic values available during runtime, for example, `Fn::Sub`, `Fn::GetAtt`, conditionals etc

A notable limitation of **Access Analyzer** is its inability to **parse templates and resolve CloudFormation's dynamic parameters**. This shortfall made it **difficult to ensure our policies were as tight** and secure as possible before deployment. It's purely dependent on concrete ARNs and it assesses Policies Post deployment.

> _This does not serve our purpose..._

</br>

## Integrating CFN Policy Validator into our CI/CD Pipeline 

### _What's the solution?_

I came across this solution at _**AWS: ReInforce 2022**._ It's a conference aimed at building super-robust, secure solutions in the Cloud.

--

**IAM Policy Validator for AWS CloudFormation**:-

* Parses resource-based and identity-based policies in CF Templates.
  
* Runs the policies through two types of Access Analyser APIs:
  - `ValidatePolicy` API --> to  validate IAM Policies & SCPs against IAM Policy grammar and Best Practices
  -  `AccessPreview` APIs --> to determine if a resource-based policy allows Public or Cross-Account Access.

### _How does the validator deal with intrinsic functions within policies?_

The tool deals with this by autogenerating appropriate ARNs for the referenced resource. The autogenerated ARN will have a valid ARN structure for that resource and a randomly generated name. The tool can do this and still provide valid IAM finding results because the **_structure of the ARN is what is important, not the value of the resource name._**

**_Quick Note:-_**

**Policy Validation is NOT dependent on the exact / actual resource ARNs. It works by analysing the relationship between Resources and Actions**

--> ARNs are super-important at the time of Policy ENFORCEMENT, it's critical that we are assigning the permissions in the policy to the correct resource.

However, in case of Policy Validation and Analysis, wherein we are analysing the Effect, Action, Condition Clauses of a Policy, so long as the ARN are structured appropriately --> **a well-formatted ARN which reflects the type of resource + permissions attached to it (via the policy statement), we are good to go.**

This preprocessing allows for a form of static analysis on the CloudFormation template's IAM policies, making it **_possible to catch potential security issues**_ before deployment.

</br> --

### The Functionality - Quick Overview

The `cfn-policy-validator` tool has two actions that it can perform - `parse` and `validate`

`parse` - it walks through each CloudFormation resource in the template, **_extracts identity-based & resource-based IAM policies_**. While parsing a template, the tool **_resolves CloudFormation intrinsic functions  and pseudo parameters_**. 

`validate` - parses your template, **_passes the identity-based and resource-based IAM policies to Access Analyzer_**, & **_reports these findings_**

#### Usage

```bash
sudo pip3 install cfn-policy-validator
cfn-policy-validator parse --template-path cfn-policy-validator/parse-template.json --region us-east-1
```

























