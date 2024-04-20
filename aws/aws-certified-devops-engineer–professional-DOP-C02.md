# AWS: Certified DevOps Engineer – Professional (DOP-C02)

## Table of Contents

1. [Introduction](#introduction)
   1. [Exam Overview](#exam-overview)
   2. [Content Outline](#content-outline)
2. [SDLC Automation](#sdlc-automation)
   1. [CI-CD Concepts](#ci-cd-concepts)

## Introduction

### Exam Overview

**Level:** Professional
**Length:** 180 minutes to complete the exam
**Cost:** 300 USD
**Format:** 75 questions, either multiple choice or multiple response
**Delivery method:** Testing center or online proctored exam

### Content Outline

- **Domain 1:** SDLC Automation _(22% of scored content)_
- **Domain 2:** Configuration Management and IaC _(17% of scored content)_
- **Domain 3:** Resilient Cloud Solutions _(15% of scored content)_
- **Domain 4:** Monitoring and Logging _(15% of scored content)_
- **Domain 5:** Incident and Event Response _(14% of scored content)_
- **Domain 6:** Security and Compliance _(17% of scored content)_

## SDLC Automation

### CI-CD Concepts

**What problems are we trying to solve?:**
These types of projects are slow, not iterative and have long release cycles.

**How do we merge the goals of Dev and Ops?:**
The traditional goals of software development and IT operations do not really align.

- **Dev:** _How many changes, features and defects can we push into production and how quickly can we do it?_
- **Ops:** _We want stable and available systems!_

**How can we solve these problems?:**
DevOps. _Shorten dev lifecycle._ Deliver features, fixes and updates frequently.

**How does DevOps look in action?:**

```
MONITOR --------> PLAN --------> CODE 
                                      
  ^                                |  
  |                                |  
  |                                v  
                                      
OPERATE                          BUILD
                                      
  ^                                |  
  |                                |  
  |                                v  
                                      
DEPLOY <------- RELEASE <------- TEST 
```

**What is CI/CD?:**

- Continuous Integration (CI)
- Continuous Delivery (CD)

**Continuous Delivery or Continuous Deployment? Are they the same thing?:**

```
+----------+      +----------+      +----------+      +----------+      +----------+
|          |      |          |      |          |      |          |      |          |
|          |      |          |      |          |      |          |      |          |
|  SOURCE  | ---> |   TEST   | ---> |  BUILD   | ---> |    QA    | ---> | RELEASE  |
|   CODE   |      |          |      |          |      |          |      |          |
|          |      |          |      |          |      |          |      |          |
|          |      |          |      |          |      |          |      |          |
+----------+      +----------+      +----------+      +----------+      +----------+
                                                                                    
           CONTINUOUS INTEGRATION                                                   
----------------------------------------------->                                    
                                                                                    
                                      CONTINUOUS DELIVERY    +----+      DEPLOY     
                                    -----------------------> |STOP| --------------->
                                                             +----+                 
                                                                                    
                                                                                    
                                                  CONTINUOUS DEPLOYMENT             
                                    ----------------------------------------------->
```

**Continuous Deployment:** An update is automated the whole way out to production _without the safeguards of continuous devivery_.
**Continuous Delivery:** Focuses on safely getting changes out to production. _Key point: there is a stop for approval before going to production_.

### CodeCommit Overview

#### Key Points

**What is CodeCommit?:**

It is a _managed service_ that hosts private Git repositories.

**Why not just use Git?:**

Well, you can. But the key term is _managed service_.

#### Benefits

* Highly available, scalable and fault tolerant
* No size limit
* Integrates with other AWS services (CodeBuild, CodePipeline, CodeDeploy, Lambda, SNS)
* Works with existing Git-based tools

#### Exam Tips

* CodeCommit has many benefits but _is not the only repository_ you can use in an AWS deployment pipeline.
* When in CodeCommit (or CodeBuild and CodeDeploy) in the AWS Management Console, _study the dropdowns_.
* Other repositories that can be used in AWS deployments include _S3_, _GitHub_, _Bitbucket_ and _GitHub Enterprise_.
