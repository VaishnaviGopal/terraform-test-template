# terraform-test-template

A minimal Terraform template used as a test scaffold for IBM Cloud Schematics workspaces.

IBM Cloud Schematics is a managed IaC-as-a-service platform (similar to Terraform Cloud)
that executes Terraform plans in IBM Cloud. This template includes a `schematics.tfvars`
file for supplying variable overrides when running via Schematics workspaces.

I built and maintained Schematics infrastructure at IBM Cloud for ~7 years, including:
- The `ibm_schematics_workspace` and `ibm_schematics_agent` resources in
  [terraform-provider-ibm](https://github.com/IBM-Cloud/terraform-provider-ibm)
- The Schematics Agent platform (Go CLI + Terraform provider + ROKS networking)

---

## Contents

| File | Purpose |
|---|---|
| `main.tf` | Minimal Terraform config using a `null_resource` local-exec provisioner |
| `schematics.tfvars` | Variable overrides for IBM Cloud Schematics workspace execution |

## How IBM Cloud Schematics uses this

When you create a Schematics workspace pointing at this repo, Schematics will:
1. Clone the repo into an isolated execution environment
2. Run `terraform init` using the provider registry
3. Apply variable overrides from `schematics.tfvars`
4. Execute `terraform plan` / `terraform apply` on demand or via automation

## Usage — Local

```bash
git clone https://github.com/VaishnaviGopal/terraform-test-template
cd terraform-test-template
terraform init
terraform apply -var-file=schematics.tfvars
```

## Usage — IBM Cloud Schematics

1. Go to [IBM Cloud Schematics](https://cloud.ibm.com/schematics/workspaces)
2. Create a new workspace
3. Point the repository URL to this repo
4. Set the Terraform version and apply

## Related

- [terraform-provider-ibm](https://github.com/IBM-Cloud/terraform-provider-ibm) —
  IBM Cloud's official Terraform provider (I'm a top-5 contributor)
- [IBM Cloud Schematics docs](https://cloud.ibm.com/docs/schematics)
