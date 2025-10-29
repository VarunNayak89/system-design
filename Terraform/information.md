# ☁️ Terraform Best Practices & Variable Management

---

## 💰 Cost: Dependencies

C# is a language to create software — similarly, **Terraform** is a language to **create infrastructure**.

---

## 🧱 Terraform Configuration and State Comparison

When you change configuration in Terraform scripts, Terraform compares:
- **Desired State:** Defined in `main.tf`
- **Actual State:** Stored in `terraform.tfstate`

Terraform then plans updates to align your infrastructure with your desired configuration.

---

## 🧠 Terraform Best Practices

1. Manipulate state only through **Terraform commands**  
2. Always set up a **shared remote state**  
3. Use **state locking**  
4. Back up your state files  
5. Use **one state per environment**  
6. Host Terraform scripts in a **Git repository**  
7. Enable **Continuous Integration (CI)** for Terraform code  
8. Apply Terraform **only through CD pipelines**  

---

## 🏗️ Provider Block

A **provider block** defines which infrastructure provider (AWS, Azure, GCP, etc.) Terraform will use.

```hcl
provider "google" {
  project     = "terraform-on-gcp-377819"   # Project ID
  credentials = file("credentials.json")
  region      = "us-central1"
  zone        = "us-central1-c"
}
```

---

## 🧩 Resource Block

A **resource block** defines components of your infrastructure.  
The first word is the resource **type**, and the second is the **resource name**.

**Example:** Creating a VM instance on Google Cloud

```hcl
resource "google_compute_instance" "my_instance" {
  name         = "terraform-instance"
  machine_type = "f1-micro"
  zone         = "us-central1-a"
  allow_stopping_for_update = true

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-10"
    }
  }

  network_interface {
    network = "default"
    access_config {}  # Required even if empty
  }
}
```

---

## 💣 How to Destroy Resources

1. **Remove resource code** from config file and run:
   ```bash
   terraform apply
   ```
   (This removes deleted resources from the state file.)
2. **Destroy all resources** in a configuration file:
   ```bash
   terraform destroy
   ```

Terraform automatically determines the correct order of destruction based on resource dependencies.

---

## 📁 terraform.tfstate

The **state file** is crucial in Terraform — it keeps track of what’s created and what hasn’t.  
It’s also used to determine what to **update or delete**.

> ⚠️ Never edit the `.tfstate` file manually.

---

## 🔐 Security Keys

Never store **access** or **secret keys** directly in Terraform files.

### Two Secure Methods:

1. **Environment Variables**
   ```bash
   export AWS_ACCESS_KEY_ID="<YOUR_ACCESS_KEY>"
   export AWS_SECRET_ACCESS_KEY="<YOUR_SECRET_KEY>"
   ```

2. **AWS CLI**
   ```bash
   aws configure
   ```
   This stores credentials securely in a hidden file under your home directory.

---

## 🧮 Variables in Terraform

### Why Use Variables?
- Avoid repeating hardcoded values.
- Improve reusability and maintainability.
- Recommended to keep all variable definitions in a separate file named **`variables.tf`**.

### How to Use Variables
To reference a variable, use:
```hcl
var.<variable_name>
```

Example:
```hcl
project     = var.project
credentials = file(var.credentials_file)
```

---

## 📥 Three Ways to Pass Variable Values

### 1️⃣ CLI Arguments
```bash
terraform plan -var="project=terraform-on-gcp-377819" -var="credentials_file=credentials.json"
```

### 2️⃣ Environment Variables
```bash
export TF_VAR_project="terraform-on-gcp-377819"
export TF_VAR_credentials_file="credentials.json"
terraform plan
```

### 3️⃣ Variable Files
Terraform automatically loads variables from any of the following files:
- `terraform.tfvars`
- `terraform.tfvars.json`
- `*.auto.tfvars`
- `*.auto.tfvars.json`

Example **terraform.tfvars**:
```hcl
project          = "terraform-on-gcp-377819"
credentials_file = "credentials.json"
```

Run command:
```bash
terraform plan
```

---

## 🧠 More About Variables

You can define **description**, **type**, **validation**, and **sensitivity** in variables.

Example:
```hcl
variable "project" {
  description = "The GCP project ID"
  type        = string
}

variable "instance_count" {
  description = "Number of instances to create"
  type        = number
  default     = 3
}
```

### Supported Variable Types

#### Simple Types
- `string`
- `number`
- `bool`
- `any`
- `null`

#### Complex Types
- `list`
- `set`
- `tuple`
- `map`
- `object`

### Collection Types
| Type | Example |
|------|----------|
| **List** | `["us-east-1", "us-west-1"]` |
| **Set** | `set(["t2.micro", "t3.micro"])` |
| **Map** | `{ env = "dev", region = "us-central1" }` |

### Structural Types
| Type | Example |
|------|----------|
| **Tuple** | `["dev", 3, true]` |
| **Object** | `{ name = "vm1", size = "medium" }` |

> `Object` is like a **Map**, and `Tuple` is like a **List** with mixed data types.

---

## ✅ Variable Validation Example

```hcl
variable "region" {
  type = string
  validation {
    condition     = can(regex("^us-", var.region))
    error_message = "Region must start with 'us-'"
  }
}
```

---

## ⚡ Run & Destroy Commands Summary

```bash
terraform plan      # Preview what will change
terraform apply     # Apply the configuration
terraform destroy   # Tear down infrastructure
```

When running `terraform apply`, Terraform shows outputs like VPC ID.  
It won’t appear in `plan` since resources aren’t created yet.

Example:
```
Run: terraform plan → input “inputvpc” → no output  
Run: terraform apply → input “inputtest” → confirm “yes” → shows VPC ID  
Then run: terraform destroy → confirm “yes”
```

---

📘 **Summary**
- Use variable files and avoid hardcoding.  
- Secure credentials using AWS CLI or environment variables.  
- Always back up your Terraform state.  
- Follow best practices for scalability and safety.

