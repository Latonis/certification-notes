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
# Terraform Fundamentals
## Terraform Providers
- Providers are Terraform's way of abstracting integrations with API control layer of the infrastructure vendors.
- Terraform, by default, looks for providers in the *Terraform Providers Registry*
- Providers are plugins. They are released on a separate rhythm from Terraform itself, and each provider has its own series of version numbers.
- You can write your own custom providers as well.
- Terraform finds and installs providers when intializing working directories (via `terraform init`)
- As a best practice, Providers should be pegged down to a specific version, so that any changes across provider version doesn't break the Terraform code.
```json
provider "azurerm" {
	version = "2.20.0"
	features {}
}
```
## Terraform State
Why State Matters? Resource Tracking
- A way for Terraform to keep tabs on what has been deployed
- Critical for Terraforms functionality
- ![[Pasted image 20220121114509.png]]
- Stored in flat files, by default named `terraform.tfstate`
- Helps Terraform calcualte deployment delta and create new deployment plans
- **Never** lose your Terraform State file.
## Terraform Variables and Outputs
```json
variable "example-variable" {
	description = "This is a variable"
	type = string
	default = "Hello World"
}

variable "my-var" {}
```
Referencing a variable: 
- `var.example-variable`
- `var.my-var`
Variables can be stored in the `terraform.tfvars` file

### Variable Validation
```json
variable "example-variable" {
	description = "This is a variable"
	type = string
	default = "Hello World"
	validation {
	condition = length (var.my-var) > 4
	error_message = "The string must be more than 4 characters in length!"
	}
}
```

If you do not want variable values to be shown in plain-text during execution, you can set the `sensitive` property to `true`
```json
variable "example-variable" {
	description = "This is a variable"
	type = string
	default = "Hello World"
	sensitive = true
}
```

### Variable Types Constraints
#### Base Types
- string
- number
- bool
#### Complex Types
- list
- set
- map
- object
- tuple
#### Examples
##### String
```json
variable "image_id" {
	type = string
	default = "image111"
}
```
##### List
```json
variable "az_names" {
	type = list(string)
	default = ["us-west-1a", "us-east-1"]
}
```

##### List of Objects
```json
variable "docker_ports" {
	type = list(object ({
	internal = number
	external = number
	protocol = string
	}))
	default = [{
		internal = 8300
		external = 8300
		protocol = "tcp"
	}]
}
```

### Terraform Output - Output Values

```json
output "instance_ip" {
	description = "The VM's private IP address"
	value = aws_instance.my-vm.private_ip
}
```

- Output variable values are shown on the shell after running `terraform apply`
- Output values are like return values that you want to track after a successful Terraform deployment.
## Terraform Provisioners
- Terraform's way of boostrapping custom scripts, commands, or actions
- Can be run either locally (on the same system where Terraform commands are being issued from) or remotely on resources spun up through the Terraform deployment
- Within Terraform code, each individual resource can have its own "provisioner" defining the connection method (if required such as SSH or WinRM) and the actions/commands or script to execute
- There are 2 types of provisoners which you can set to run when a resource is being created or destroyed:
	1. **Creation-time**
		1. This is the default
	2. **Destroy-time

### Best Practices and Cautions
- **Disclaimer**: HashiCorp recommends using Provisioners as a last resort and to try using inherent mechanisms within your infrastructure deployment to carry out custom tasks when possible.
- Terraform cannot track changes to provisioners as they can take any independent action, hence they are not tracked by Terraform state files
- Provisioners are recommended for use when you want to invoke actions not covered by Terraform's declarative model
- If the command within a provisioner returns non-zero return codes, it is considered a failure and the underlying resource is considered tainted.

```json
resource "null_resource" "dummy_resource" {
	provisioner "local-exec" {
		command = "echo '0' > status.txt"
	}
	
	provisioner "local-exec" {
		when = destroy
		command = "echo '1' > status.txt"
	}
}
```

# Terraform State
## Terraform State Command
### Terraform State
- Maps real-world resources to a Terraform configuration
- State is stored locally in a file called `terraform.tfstate`
- Prior to any modification operation, Terraform refreshes the state file
- Resource dependency metadata is also tracked via the state file
- Helps boost deployment performance by caching resource attributes for subsequent use
### State Command
- Terraform State command is a utility for manipulating and reading the Terraform state file
- Scenario
	- Advanced state management
	- manually remove a resource from Terraform state file so that it's not managed by terraform
	- Listing out tracked resources and their details (via state and list subcommands)
![[Pasted image 20220130211509.png]]

## Local and Remote State Storage
### Local State Storage
- Save Terraform state locally on your system
- Terraforms default behavior
### Remote State Storage
- Saves state to a remote data source
	- S3, GCP, Azure, etc
- Allows sharing state file between distributed teams
- Allows locking state so parallel executions don't coincide
	- S3, GCP, HashiCorp
- Enables sharing output values with other Terraform confiuguration or code
![[Pasted image 20220130212142.png]]
```json
terraform {
	backend "s3" {
		region = ""
		key = ""
		bucket = ""
	}
}
```

# Terraform Modules
## Accessing and Using Terraform Modules
### Modules
- A module is a container for multiple resources that are used together
- Every Terraform configuration has at least one module, called the *root* module, which consists of code files in your main working directory
### Accessing Terraform Modules
- Modules can be downloaded or referenced from:
	- Terraform Public Registry
	- A private registry
	- local system
- Modules are referenced using a **module** block
	- allowed parameters: `count`, `for_each`, `providers`, `depends_on`
```json
module "my-vpc-module" {
	source = "./modules/vpc" // mandatory
	version = "0.0.01"
	region = var.region // input parameter
}
```

### Using Terraform Modules
- Modules can optionally take input and provide outputs to plug back into your main code
**Accessing module outputs in your code**:
- `module.<module name>.<var name>`
```json
resource "aws_instance" "my-vpc-module" {
	// # other arguments
	subnet_id = module.my-vpc-module.subnet_id
}
```

## Interacting with Terraform Module Inputs and Outputs
### Declaring Module in Code
- Module inputs are arbitrarily named parameters that you pass inside the module block
- These inputs can be used as variables inside the module code
```json
module "my-vpc-module" {
	source = "./modules/vpc"
	server-name = 'us-east-1'

}
```

Inside module: `var.server-name`
### Terraform Module Outputs
- The outputs declared inside Terraform module code can be fed back into the root module or your main code
outside module: `module.my-vpc-module.server-name`

```json
module "my-vpc-module" {
	source = "./modules/vpc"
	server-name = 'us-east-1'
	output "ip_address" {
		value = aws_instance.private_ip
	}
}

```
Accessing above ip_address:
`module.my-vpc-module.ip_address`