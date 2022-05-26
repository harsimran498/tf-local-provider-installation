# tf-local-provider-installation

// This document provides steps to install and use a local provider downloaded from tf registry in your local disk and bypassing tf to check for registry.terraform.io for any providers, instead only search in local dir.

1	Create dir structure - /Users/ha20342587/.terraform.d/plugins/sca-terraform/venafi/venafi/0.1.0/darwin_amd64/ and place terraform-provider-venafi_v0.1.0 
	2	Create file - $HOME/.terraformrc and copied below contents in it:  plugin_cache_dir   = "$HOME/.terraform.d/plugin-cache" disable_checkpoint = true
	3	run command - export TF_PLUGIN_CACHE_DIR="$HOME/.terraform.d/plugin-cache" 
	4	create a seperate dir somewhere like - /Users/ha20342587/sca-terraform and create main.tf with the below contents: terraform {   required_providers {     venafi = {       source = "sca-terraform/venafi/venafi"       version = "0.1.0"     }   } }   provider "venafi" {   url          = "https://tpp.venafi.example"   trust_bundle = "${file("/opt/venafi/bundle.pem")}"   access_token = "p0WTt3sDPbzm2BDIkoJROQ=="   zone         = "DevOps\\Terraform" }
	5	And run terraform init command

[Yesterday 22:46] Harsimran Kaur (Europe - iDEAS-Cloud Transformation)
ha20342587@C02DQ2RXMD6M scatf % terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of sca-terraform/venafi/venafi from the dependency lock file
- Using previously-installed sca-terraform/venafi/venafi v0.1.0

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

