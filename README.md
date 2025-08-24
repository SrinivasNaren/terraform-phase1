

# 🚀 Terraform Learning – Phase 1 (With Code Structure)

---

## 🔹 Step 1: What is Terraform?

Terraform is an **Infrastructure as Code (IaC)** tool.
It lets you **describe your infrastructure (servers, databases, files, etc.) as code**, and Terraform will **create/destroy/update** it for you.

Think of it like:
👉 Instead of clicking buttons in AWS / Azure / GCP console, you **write code once**, and Terraform does the job.

---

## 🔹 Step 2: Key Terraform Commands

| Command             | Meaning                                          |
| ------------------- | ------------------------------------------------ |
| `terraform init`    | Initializes project (downloads provider plugins) |
| `terraform plan`    | Shows what Terraform will do before applying     |
| `terraform apply`   | Actually creates/updates resources               |
| `terraform destroy` | Removes everything created                       |

---

## 🔹 Step 3: Terraform Code Structure

Think of a Terraform project like a **recipe book**.
Every recipe (resource) has **ingredients (provider, variables)** and **instructions (resource definition)**.

### 📌 Basic Blocks

1. **Provider block** – tells Terraform which platform to use

```hcl
provider "local" {
  # config (optional)
}
```

2. **Resource block** – the actual thing Terraform will create

```hcl
resource "local_file" "example" {
  content  = "Hello, Terraform!"
  filename = "hello.txt"
}
```

3. **Variable block** (optional, for flexibility)

```hcl
variable "filename" {
  default = "myfile.txt"
}
```

4. **Output block** (optional, shows results after apply)

```hcl
output "file_path" {
  value = local_file.example.filename
}
```

---

## 🔹 Step 4: Project File Structure

When projects grow, files are usually split:

```
my-project/
 ├── main.tf        → main resources & provider
 ├── variables.tf   → variable definitions
 ├── outputs.tf     → outputs
 ├── terraform.tfstate → state file (auto-created)
 └── .terraform/    → provider plugins (auto-created)
```

👉 For beginners: keep **everything inside `main.tf`** (simple & clean).

---

## 🔹 Step 5: Minimum Terraform Code

At the very least, you need:

* `provider`
* `resource`

Later we add `variable` + `output` for better practice.

---

## 🔹 Step 6: Full Example (Local Provider)

Here’s a **complete working code** in `main.tf`:

```hcl
# Provider
provider "local" {}

# Variable
variable "filename" {
  default = "hello.txt"
}

# Resource
resource "local_file" "example" {
  content  = "Hello, Terraform!"
  filename = var.filename
}

# Output
output "file_path" {
  value = local_file.example.filename
}
```

---

## 🔹 Step 7: How to Run

1. Save the above code in `main.tf`
2. Run:

   ```bash
   terraform init
   terraform plan
   terraform apply -auto-approve
   ```
3. Terraform will create a file **hello.txt**
4. To delete it:

   ```bash
   terraform destroy -auto-approve
   ```

