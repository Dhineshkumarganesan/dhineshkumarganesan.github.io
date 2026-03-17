---
layout: post
title: "Agentic Azure Resource Provisioning using GitHub Copilot Skills and Agents"
date: 2026-03-17
---

**Agentic Azure Resource Provisioning with GitHub Copilot Agents and Skills**

Create a new project named lab1 and create .github and .vscode directory

<img width="230" height="196" alt="image" src="https://github.com/user-attachments/assets/c6085514-3c73-40c3-a7f9-2155cc3a3590" />

Add copilot-instructions.md under lab1 and add below instructions

<img width="281" height="217" alt="image" src="https://github.com/user-attachments/assets/7d1fe1b9-33b5-4e12-8e9b-bc5cef4ba13f" />

# Copilot Instructions — Azure Storage Account Lab

## Scope
This project is focused solely on creating an Azure Storage Account Terraform module.
Do not suggest or generate code for other Azure resources unless explicitly asked.

## Terraform Structure
- Use separate files: `main.tf`, `variables.tf`, `outputs.tf`
- Pin the AzureRM provider version (e.g., ~> 3.0 or ~> 4.0)
- Use `terraform.tfvars` for environment-specific values

## Azure Storage Account Rules
- Default location: `uksouth` (adjust to your region)
- Default account_tier: `Standard`
- Default replication: `LRS` (for lab/dev use)
- Always set `https_traffic_only_enabled = true`
- Always set `min_tls_version = "TLS1_2"`
- Disable public blob access: `allow_nested_items_to_be_public = false`

## Naming Convention
- Format: `st<environment><purpose>001` (Azure CAF style)
- Example: `stdevlabstorage001`
- Lowercase, no hyphens (Azure storage account restriction)

## Tagging
- Always include tags: environment, owner, created_by = "terraform"

## Outputs
- Always output: storage account id, name, primary blob endpoint

## Security
- Never hardcode subscription IDs, credentials, or access keys
- Use `sensitive = true` for any key/connection string outputs

## Workflow Commands

# Initialize Terraform
terraform init

# Validate configuration
terraform validate

# Format code
terraform fmt -recursive

# Generate plan
terraform plan -out=tfplan

# Apply changes
terraform apply tfplan

# Destroy resources after lab
terraform destroy

## Development Context
- This is a local development environment
- Authentication is via `az login` (Azure CLI)
- No CI/CD pipeline — all commands run locally in terminal
- No remote state backend — use local state for this lab

Under .vscode → edit mcp.json and add below 

{
"servers": {
"terraform": {
"command": "docker",
"args": [
"run",
"-i",
"--rm",
"-e", "TFE_TOKEN=${input:tfe_token}",
"-e", "TFE_ADDRESS=${input:tfe_address}",
"hashicorp/terraform-mcp-server:0.3.3"
]
}
},
"inputs": [
{
"type": "promptString",
"id": "tfe_token",
"description": "HCP Terraform / Terraform Enterprise API Token (leave empty for public registry only)",
"password": true
},
{
"type": "promptString",
"id": "tfe_address",
"description": "HCP Terraform / Terraform Enterprise Address (default: https://app.terraform.io)",
"password": false
}
]
}


From github-copilot-skills- terraform repo, get the agents and skill directory and copy within lab1 folder

<img width="454" height="216" alt="image" src="https://github.com/user-attachments/assets/be8d99fe-6af3-4ce4-8697-09b5d4575d05" />

now under lab1 , you can see agents and skills folder as below

<img width="387" height="255" alt="image" src="https://github.com/user-attachments/assets/a3be529b-108a-4c7b-90f3-5f39d7ce1b5e" />

Once it is done, you can go to copilot and ask to Create an Azure storage account module


<img width="1401" height="730" alt="image" src="https://github.com/user-attachments/assets/aad989ee-1dfc-4e2f-9e8a-fce694d85d78" />

<img width="1139" height="653" alt="image" src="https://github.com/user-attachments/assets/b0d4bfa0-e1dc-4c99-b52b-650774f6b83a" />

<img width="1117" height="628" alt="image" src="https://github.com/user-attachments/assets/c9161f28-cb34-422a-8670-946068bb443b" />

<img width="1129" height="388" alt="image" src="https://github.com/user-attachments/assets/20d45ab3-8463-4b37-8596-0c9a89b69f6e" />

<img width="1164" height="459" alt="image" src="https://github.com/user-attachments/assets/4759ef17-75a7-45da-9737-681373459534" />

<img width="1144" height="502" alt="image" src="https://github.com/user-attachments/assets/8bfa611e-c398-46ce-bbe5-17cdb6870632" />

<img width="1146" height="737" alt="image" src="https://github.com/user-attachments/assets/7c57b816-05ea-467b-bed4-ae3644084183" />

<img width="1104" height="241" alt="image" src="https://github.com/user-attachments/assets/897490d7-a766-4ac4-b825-99592ce69a4e" />

<img width="1142" height="826" alt="image" src="https://github.com/user-attachments/assets/edfdd799-12b5-45a1-842c-0a2fd246c0df" />

<img width="1113" height="782" alt="image" src="https://github.com/user-attachments/assets/3a83c2db-4ce5-42a1-a6f5-64cd1ce8ae2f" />

<img width="1159" height="103" alt="image" src="https://github.com/user-attachments/assets/e69431d6-5430-4de5-84e5-fc1b29ddf161" />

<img width="1148" height="824" alt="image" src="https://github.com/user-attachments/assets/bfc6a44d-3b44-47d9-85c0-e96b63ed189b" />

<img width="1158" height="539" alt="image" src="https://github.com/user-attachments/assets/5f02e0c5-b96c-4152-806f-fed78db7cdd6" />

Below shows previous step has perform scaffold terraform

Earlier

<img width="487" height="251" alt="image" src="https://github.com/user-attachments/assets/e3ab9c65-db47-4e41-8f96-49b07bd3b766" />

After scaffold, you see there are files created within modules directory

<img width="490" height="436" alt="image" src="https://github.com/user-attachments/assets/0fd24ec3-4333-4805-bb45-f0e7b6390ed7" />

After this, you can perform terraform init and validate. You can copilot to perform this step.

<img width="1135" height="494" alt="image" src="https://github.com/user-attachments/assets/2464cc3c-56a3-437b-a671-2494131c5277" />

Here I prompted – could you check terraform validate succeeded or not and got response it is succeeded

<img width="1139" height="434" alt="image" src="https://github.com/user-attachments/assets/a22e6e45-5d47-4c7e-8aa4-54a77744f302" />

Here I prompted do terraform plan

<img width="1142" height="413" alt="image" src="https://github.com/user-attachments/assets/8549e823-d2e7-4da8-be8d-90259b2037aa" />

<img width="1138" height="414" alt="image" src="https://github.com/user-attachments/assets/02cfccc3-9e2d-424b-9256-9444df1533b5" />

<img width="1160" height="427" alt="image" src="https://github.com/user-attachments/assets/e0709bfd-4ba3-4d29-97d5-a70b0e0cc769" />

<img width="1179" height="441" alt="image" src="https://github.com/user-attachments/assets/c46bbafb-7352-4714-af29-68a754c8b94d" />

<img width="1139" height="775" alt="image" src="https://github.com/user-attachments/assets/7d60755f-148e-4090-a249-ddc457319a2e" />

Terraform plan failed due to authentication. Hence I prompted to use az login as below

<img width="1136" height="623" alt="image" src="https://github.com/user-attachments/assets/7ea48ccf-5283-48dd-9d5c-8d47a43d8d4b" />

<img width="1155" height="758" alt="image" src="https://github.com/user-attachments/assets/0d995438-8aab-40ed-ad16-4f119f1af5bd" />

Next I prompted to explain terraform plan and it resulted a Summary

<img width="1159" height="867" alt="image" src="https://github.com/user-attachments/assets/1532519f-374c-489b-b19d-cbad456b1401" />

Next I prompt to show it as json and save it

<img width="1183" height="871" alt="image" src="https://github.com/user-attachments/assets/eac90368-e856-4f90-9e48-94214d79ea54" />

<img width="1162" height="476" alt="image" src="https://github.com/user-attachments/assets/adf4900e-4a0b-4f0e-9818-36191602a357" />

<img width="1181" height="426" alt="image" src="https://github.com/user-attachments/assets/9b90d224-73cb-4b1b-a673-cf43d4a4e5f2" />

Next I prompt to proceed with apply ( terraform apply)

<img width="1155" height="828" alt="image" src="https://github.com/user-attachments/assets/d5200b90-6cf4-4250-8a37-ad96268acabe" />

<img width="1168" height="672" alt="image" src="https://github.com/user-attachments/assets/3e60963b-de6b-42b6-abc1-571d60a9b6c9" />

<img width="1155" height="447" alt="image" src="https://github.com/user-attachments/assets/dd94a7e8-0966-4824-a975-f2cceb73bde6" />

apply failed, as storage account already has another account with similar name. Hence it asked  me to change it but it did created the resource group rg-learning-lab.

You can see below resource group rg-learning-lab created

<img width="1658" height="605" alt="image" src="https://github.com/user-attachments/assets/be2ddc6b-03fd-430c-baf2-f9003a21f423" />


I prompt to destroy all resource as below

<img width="1169" height="880" alt="image" src="https://github.com/user-attachments/assets/4a0e7657-32ce-4648-bc27-658107cf4c99" />

<img width="1163" height="488" alt="image" src="https://github.com/user-attachments/assets/118ba0d0-50bc-484e-9b85-e356e26f7835" />


It destroyed the resource group

<img width="1719" height="537" alt="image" src="https://github.com/user-attachments/assets/7904a846-fef4-4e27-8968-f701dde24496" />


I changed the storage account name to stlabdevjohn001. If you ask Copilot, it will change the file name

<img width="1121" height="531" alt="image" src="https://github.com/user-attachments/assets/a2125c3e-71c4-4a1e-a2e6-4044c4e41a31" />


I then enter prompt that account name changed . Now reapply

<img width="1165" height="685" alt="image" src="https://github.com/user-attachments/assets/a8cb50a2-fb91-4ed0-81f4-e503d3a4ffb4" />

<img width="1161" height="203" alt="image" src="https://github.com/user-attachments/assets/49bb6fec-697e-42f7-bdad-857493c79150" />

<img width="1183" height="507" alt="image" src="https://github.com/user-attachments/assets/55f27b65-ae96-4d51-bea4-8e9ceb37f0dd" />

It applied and new resources created

<img width="1654" height="539" alt="image" src="https://github.com/user-attachments/assets/cc1d4313-67e3-4283-9488-bab4173f2b58" />

<img width="1895" height="593" alt="image" src="https://github.com/user-attachments/assets/b099023b-a3df-4cb5-bfb1-59bf6f764c15" />

Again destroyed the resources

<img width="1168" height="265" alt="image" src="https://github.com/user-attachments/assets/ad6c81cd-5a90-4582-8eaa-eb096c23aa5d" />

<img width="1193" height="479" alt="image" src="https://github.com/user-attachments/assets/5b3959d3-d473-41a3-89e2-09de8afedaf5" />

<img width="1208" height="519" alt="image" src="https://github.com/user-attachments/assets/f376a9f1-e63a-4312-9532-8674ece3c9d8" />

<img width="1891" height="583" alt="image" src="https://github.com/user-attachments/assets/0f9b7246-f01d-4cdb-8e3a-a1ffb47f992e" />












































