# ⚙️ Terraform Commands & Secure Key Storage

---

## 🧱 Terraform Core Commands

### `terraform init`
Initializes local settings, backend configurations, and downloads provider plugins.  
This must be run **before** any other Terraform commands.

### `terraform plan`
Generates an execution plan showing resources that will be **created**, **modified**, or **deleted**.  
Review the plan, then use `terraform apply` to execute the changes.

### `State File`
Terraform maintains a **state file** to track what’s been created, modified, or destroyed.  
This allows Terraform to know the **current infrastructure state** versus your configuration.

### `terraform apply`
Executes the actions defined in the plan — creates or modifies infrastructure.  
You’ll be prompted to confirm the action:
```
Do you want to perform these actions? (yes/no)
```
Reply **“yes”**, and Terraform will apply the changes.  
> Example: It may return outputs such as your **VPC ID** or **instance IP**.

### `terraform destroy`
Destroys all managed resources and deletes entries from the Terraform state file.  
Use this to **tear down** your infrastructure completely.

### `terraform taint <resource_type>.<resource_name>`
Marks a specific resource as **tainted** — meaning Terraform considers it damaged or invalid.  
When you next run `terraform apply`, Terraform will **destroy and recreate** that resource automatically.

---

## 🔐 How to Securely Store Your Keys

### Steps:

1. **Install the AWS Command Line Interface (CLI):**  
   Refer to AWS CLI installation instructions.

2. **Configure AWS Credentials:**
   ```bash
   aws configure
   ```
   Provide your AWS credentials when prompted.

3. **Remove credentials from your Terraform file:**  
   Delete the access key and secret key lines from your `main.tf` file.

   ```hcl
   access_key = "<YOUR_AWS_ACCESS_KEY>"
   secret_key = "<YOUR_SECRET_KEY>"
   ```

4. **Save the file** and then run:
   ```bash
   terraform plan
   ```

This ensures your credentials are **stored securely in your local AWS configuration** instead of being exposed in code.

---

## ✅ Example Command

```bash
aws configure
```
Follow prompts to enter:
- AWS Access Key ID  
- AWS Secret Access Key  
- Default region name  
- Output format

---

### 💡 Best Practice
- Never hardcode credentials in Terraform `.tf` files.  
- Use **environment variables**, **AWS CLI config**, or **Terraform Cloud workspaces** for secure authentication.  
- Always commit `.tfstate` files and `.tfvars` containing secrets to **.gitignore**.

