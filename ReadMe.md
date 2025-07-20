# Terraform AWS EC2 + ALB Deployment Script

This project automates the deployment of an AWS EC2 instance behind an Application Load Balancer (ALB) using Python, Jinja2 templates, and Terraform.

## 📁 Project Structure

```
.
├── Terraform/               # Contains the generated Terraform config (main.tf)
├── source/                  # Contains the Jinja2 template (template.txt.j2)
├── main.py                  # Main deployment script
└── README.md
```

## ✅ Requirements

### Python Modules

Install dependencies using pip:

```bash
pip install python-terraform boto3 jinja2
```

### Terraform

Make sure Terraform is installed and available in your system PATH:  
👉 https://www.terraform.io/downloads

### AWS Credentials

You must export valid AWS credentials and a default region before running the script:

```bash
export AWS_ACCESS_KEY_ID="YOUR_AWS_ACCESS_KEY"
export AWS_SECRET_ACCESS_KEY="YOUR_AWS_SECRET_KEY"
export AWS_DEFAULT_REGION="us-east-2"
```

### IAM Permissions

Ensure your IAM user/role has sufficient permissions to:
- Launch EC2 instances
- Create security groups
- Manage ALBs
- Describe resources via boto3

## 🚀 How to Use

From the **root directory (`./`)**, run the script:

```bash
python3 main.py
```

You can choose between:
- **Manual input:** uncomment the `get_user_input()` line in `main.py`.
- **Defaults:** use the predefined configuration (Ubuntu, `t3.small`, `us-east-2`, AZs `a` and `b`, and `nof-lb1` as the ALB name).

The script will:
1. Render the `./source/template.txt.j2` into `./Terraform/main.tf`
2. Run `terraform init`, `plan`, and `apply`
3. Fetch outputs: instance ID, public IP, ALB DNS
4. Validate resources via boto3
5. Save instance details to `aws_validation.json`

## 📤 Outputs

After deployment, you'll see:
- EC2 instance ID
- Public IP address
- ALB DNS name
- Validation results saved to `aws_validation.json`

## ⚠️ Notes

- Subnet and VPC IDs in the template must exist in your AWS account in `us-east-2`.
- Terraform state is stored locally (no remote backend).
- The script assumes a basic setup and is not production-ready without improvements like:
  - Environment separation
  - Remote state management
  - Parameterization of subnet/VPC IDs
  - Better error handling

---

Happy automating! 🚀
