# ☁️ Terraform AWS Infrastructure Setup

This project provisions a basic AWS infrastructure using **Terraform**, following best practices like **remote state storage** and parameterization with variables.

---

## 🚀 Features

- ✅ Custom **VPC** with user-defined CIDR
- ✅ **Internet Gateway** and **Public Route Table**
- ✅ **Public Subnet** with auto-assigned public IPs
- ✅ **Security Group** allowing SSH and application port (`3000`)
- ✅ **EC2 instance** launched in the public subnet
- ✅ **Key Pair** using your public key for SSH access
- ✅ **Remote state** stored securely in **S3**
- ✅ Outputs the **public IP** of the EC2 instance

---

## 📁 Project Structure

```bash
.
├── main.tf
├── outputs.tf
├── variable.tf
├── user_data.sh
├── .gitignore
└── README.md
```

---

## ⚙️ Variables

These variables are defined in `variables.tf`:

| Variable         | Description                       | Default Value       |
|------------------|-----------------------------------| ------------------- |
| `vpc_cidr`       | CIDR block for the VPC            | "10.0.0.0/16"       |
| `prefix_tag`     | Tag prefix for all resources      |     ----            |
| `public_key_path`| Path to your public SSH key       | "~/.ssh/id_rsa.pub" |
| `instance_type`  | EC2 instance type (e.g., t2.micro)| "t2.micro "         |

Define actual values in `terraform.tfvars`:

```hcl
vpc_cidr        = "10.0.0.0/16"
prefix_tag      = "devops-lab"
public_key_path = "~/.ssh/id_rsa.pub"
instance_type   = "t2.micro
```

---

## ☁️ Remote State (S3)

This project uses Amazon S3 to store Terraform's remote state.

Example `backend.tf`:
```hcl
terraform {
  backend "s3" {
    bucket = "your-terraform-state-bucket"
    key    = "terraform.tfstate"
    region = "us-east-1"
  }
}
```
Run this once to initialize the backend:
```bash
terraform init
```

---

## 🛠 Usage

### 1. Clone the repo
```bash
git clone https://github.com/yourusername/terraform-aws-infra.git
cd terraform-aws-infra
```
### 2. Initialize Terraform
```bash
terraform init
```
### 3. Review the plan
```bash
terraform plan
```
### 4. Apply infrastructure
```bash
terraform apply -auto-approve
```

---

## 📤 Outputs

After apply, Terraform will display:
```bash
Outputs:

public_ip = "54.xxx.xxx.xxx"
```
You can now SSH into your instance:
```bash
ssh -i ~/.ssh/id_rsa ec2-user@"54.xxx.xxx.xxx"
```

---

## 🧹 Cleanup
To destroy all resources:
```bash
terraform destroy -auto-approve
```

---

## 🙌 Author

Ahmed Elhgawy – [GitHub](https://github.com/Ahmed-Elhgawy) | [LinkedIn](https://linkedin.com/in/ahmed-mahmoud-a16310268)
