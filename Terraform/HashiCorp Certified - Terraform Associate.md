# Introduction Information
## Exam Format
Length: 1 Hour
Amount of Questions: 50 to 60 questions
Online: Proctored
Expiration Date: 2 Years

## Exam Objectives:
1. **Understand IaC Concepts**
	1. Explain what IaC is
	2. Describe advantages of IaC
2. **Understand Terraform's Purpose**
	1. Know what Terraform state is
	2. Know Terraform's multi-cloud benefits
3. **Understand Terraform Basics**
	1. Install Terraform
	2. Use Terraform providers
	3. Use Terraform provisioners
4. **Use Terraform CLI**
	1. How to debug
	2. Terraform commands:
		1. fmt
		2. state
		3. taint
		4. import
		5. workspaces
5. **Interact with Terraform Modules**
	1. Differentiate module sources
	2. Module inputs and outputs and module verisoning
	3. Variable scope within root/child modules, public registry
6. **Navigate Terraform Workflow**
	1. local and remote state storage
	2. state locking
	3. Terraform backend block and Terraform refresh effects
	4. Backend auth and secret management in state files
7. **Implement and Maintain State**
	1. Describe Terraform workflow
	2. Initialize Terraform working dir (terraform init)
	3. Terraform commands:
		1. validate
		2. plan
		3. apply
		4. destroy
8. **Read, generate, and modify configuration**
	1. Terraform variables and outputs
	2. Create and constrat resource and data blocks
	3. Resource addressing, built-in functions, and dynamic blocks
9. **Understand Terraform Cloud and Enterprise Capabilities**
	1. Describe benefits of Sentinel, registry, and workspaces
	2. Differential Terraform OSS and Enterprise workspaces
	3. Summary of Terraform Cloud
# Understanding Infrastructure as Code
## IaC and Its Benefits
- No more clicks
	- Write down what you want to deploy (VMs, disks, apps, etc.) as human readable.
- Enables DevOps
	- Codification of deployments means it can be tracked in version control enabling better visibility and collaboration across teams.
- Declare your Infrastructure
	- Infrastructure is, for the majority of cases, written declaratively via code but can be procedural too!
- Speed, Cost, and Reduced Risk
	- Less human intervention during deployment means fewer chances of security flaws, superfluous resources, and more time is saved.

## Example TF code
```
provider "aws" {}

```

## Cloud Agnostic IaC
- Automate software defined networking
- Interacts and takes care of communication with control layer APIs with ease
- Supports a vast array of private and public cloud vendors
	- [Provider Registry](https://registry.terraform.io/browse/providers)
- Tracks state of each resource deployed
## Review Quiz for Understanding IaC
![[Pasted image 20220120120632.png]]

# IaC with Terraform
## What is the Terraform Workflow
1. Write
	1. This would generally start off with creating a GitHub repo as a common best practice
2. Plan
	1. Continually add and review changes to code in your project
3. Apply
	1. Depoy the changes to provision real infrastructure

## Terraform Init
`terraform init`: initializes the working directory that contains your Terraform code
1. Downloads ancillary components
	1. Downloads modules and plugins
2. Sets up backend
	1. Sets up the backend for storing Terraform state file, a mechanism by which Terraform tracks resources
## Terraform Key Concepts: Plan, Apply, and Destory
Workflow: Write -> Plan -> Apply
### Terraform Plan: Reviewing your Terraform Code
`terraform plan`
- Reads the code and then creates and shows a **plan** of execution/deployment
	- This command does not deploy anything, it should be considered a read-only command
- Allows the user to "review" the action plan before executing anything
- At this stage, authentication credentials are used to connect to your infrastructure, if required
### Terraform Apply: Deploy the Terraform Code
`terraform apply`
- Deploys the instructions and statements in the code
- Updates the deployment state tracking mechanism file, aka the **state file**
	- filename: `terraform.tfstate`
### Terraform Destroy: Cleaning up your Terraform Deployment
`terraform destory`
- Looks at the recorded, stored state file created during deployment and destorys all resources created by your code
- Should be used with caution, as it is a non-reversible command.
- Take backups and be sure that you want to delete infrastructure
## Resource Addressing in Terraform
### Code Snippet for configuring provider
AWS:
```json
provider "aws" {
	region = "us-east-1"
}
```

GCP w/ File load
```json
provider "google" {
	credentials = file("credentials.json")
	project = "my-gcp-project"
	region = "us-west-1"
}
```

Resource Block
```json
resource "aws_instance" "web" {
	ami = "<ami id>"
	instance_type = "t2.micro"
}
```
![[Pasted image 20220120122442.png]]

Data Source:
```json
data "aws_instance" "my-vm"
	instance_id  = "<id>"
```
![[Pasted image 20220120122533.png]]
- Resource Block is for creating resources from scratch
- Data Source Block is for already existing resources

### Terraform code
- Terraform executes code in files with the `.tf` extension
- Initially, Terraform looks for providers in the *Terraform providers registry*
## Review Quiz: IaC with Terraform
![[Pasted image 20220120123722.png]]