# 🧱 Terraform — Locals vs Variable & Output

---

## ⚙️ Local Vs Variable

- **Locals values** are not set by user input or values in `.tfvars` files. Instead, they are defined *locally* within the configuration (hence the name).  
  Rather than hardcoding values, local values can produce a more **meaningful** or **readable** result.
- The ability to change values that are likely to change in the future is the key benefit of using **Terraform locals**.
- Unlike variable values, **local values can use dynamic expressions** and **resource arguments**.
- Recommended practice: put locals in a **separate file** called `locals.tf` so they can be easily referenced.

### 🧩 Example 1
```hcl
locals {
  name_prefix = "JacksDemo-${var.environment}"
}

module "appgateway" {
  application_gateway_name = "${local.name_prefix}-${var.application}"
  ...
}
```

### 🧩 Example 2
```hcl
locals {
  mandatory_tags = {
    cost_center = var.cost_center
    environment = var.environment
  }
}

tags = merge(var.resource_tags, local.mandatory_tags)
```

---

## 🖥️ TERRAFORM OUTPUT

- Works like `console.writeLine` — a way to **print values to the terminal**.
- **Terraform output values** are extremely useful for **debugging** and **verifying resource attributes** such as:
  - `arn`
  - `instance_state`
  - `outpost_arn`
  - `public_ip`
  - `public_dns`

### 🧩 Example 1
```hcl
output "random_output" {
  value = "Hello this is output"
}
```
**When you run `terraform plan`**, the terminal will display:
```
random_output = hello this is output
```

### 🧩 Example 2
```hcl
output "my_console_output" {
  value = aws_instance.ec2_example.public_ip
}
```
- The above output **won’t appear during** `terraform plan` because it’s a **dynamic value**.
- It will be displayed **after running**:
  ```bash
  terraform apply
  ```

### 🔒 Example (Hide Sensitive Information)
```hcl
output "my_console_output" {
  value     = aws_instance.ec2_example.public_ip
  sensitive = true
}
```

> Use `sensitive = true` to hide secret or private values from being displayed in terminal output.

---

✅ **Summary**
- Use `locals` for reusability and better organization.  
- Use `outputs` to display or debug Terraform values effectively.  
- Always hide secrets using `sensitive = true`.

