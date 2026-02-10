## 75. How do you securely manage **secrets** in **Terraform projects**?-

- Managing **secrets securely** in Terraform is critical because
infrastructure code often interacts with **sensitive credentials** such
as **API keys**, **database passwords**, **tokens**, and
**certificates**. If secrets are mishandled, they may leak through
**source control**, **logs**, or **state files**, leading to **security
breaches**.

Secure secret management involves multiple best practices:

- First, secrets should never be **hardcoded** directly into .tf files.
Instead, they should be supplied through secure mechanisms like
**environment variables**, **encrypted variable files**, or **external
secret managers**.

- Second, Terraform supports marking variables as **sensitive**,
preventing them from being displayed in CLI output. However, this only
hides them visually --- it doesn't encrypt them.

- Third, organizations commonly integrate **external secret management
systems** like **Vault** or **cloud-native secret stores**, which
dynamically supply credentials during runtime.

- Fourth, **remote state** should be **encrypted** and
**access-controlled**, since **state files** may contain secrets in
plaintext.

- Finally, **CI/CD pipelines** should inject secrets dynamically at
runtime instead of storing them in repositories.

- This layered approach ensures secrets are protected both **at rest** and
**in transit**.

### Example

``` hcl
variable "db_password" {
  type      = string
  sensitive = true
}
```

Environment injection:

``` bash
export TF_VAR_db_password="securevalue"
```

### Real-World Example

A deployment pipeline retrieves database credentials from a **secret
manager** and injects them into Terraform execution without exposing
them to developers.

### Interview Punch Lines

-   "Secrets should be externalized and never hardcoded."
-   "Use environment variables or secret managers."

------------------------------------------------------------------------

## 76. Why is **hardcoding credentials** bad practice?

Hardcoding **cloud credentials** directly into Terraform configuration
creates major **security risks**. Since Terraform code is typically
stored in **version control systems**, embedding credentials exposes
them to anyone with repository access and potentially to public leaks.

Hardcoded credentials also:

-   Cannot be rotated easily
-   Increase **attack surface**
-   Violate **compliance standards**
-   Create **audit challenges**

If compromised, attackers could gain full **cloud access**.

Instead, credentials should be dynamically provided through secure
channels such as **IAM roles**, **environment variables**, or **secret
management tools**.

This aligns with modern **DevSecOps practices** where credentials are
**ephemeral** and centrally managed.

### Example (Bad Practice)

    access_key = "AKIA123"
    secret_key = "abcd123"

### Real-World Example

A leaked Git repository exposed AWS keys leading to unauthorized
crypto-mining usage.

### Interview Punch Lines

-   "Hardcoded credentials create exposure risk."
-   "They violate security best practices."

------------------------------------------------------------------------

## 77. How do **IAM roles** improve security?

**IAM roles** provide **temporary credentials** instead of static access
keys. Terraform running on cloud instances or CI pipelines can assume
roles, eliminating the need to store credentials.

Benefits:

-   No hardcoded secrets
-   Automatic rotation
-   **Limited scope permissions**
-   Reduced credential leakage

Terraform authenticates using the environment's **identity** rather than
embedded keys.

### Interview Punch Lines

-   "IAM roles remove static credential storage."
-   "They provide temporary secure access."

------------------------------------------------------------------------

## 78. Principle of **Least Privilege** in Terraform

**Least privilege** means granting only the **minimum permissions**
required to perform tasks. Terraform access policies should restrict
actions to specific resources and operations.

Applying this principle prevents misuse or damage if credentials are
compromised.

### Interview Punch Lines

-   "Grant minimum required permissions."
-   "Reduces blast radius of compromise."

------------------------------------------------------------------------

## 79. How is **Terraform state encrypted**?

**Terraform state files** may contain **sensitive information**. When
stored remotely, **encryption** ensures confidentiality.

Encryption methods include:

-   **Server-side encryption**
-   **Transport encryption**
-   **Client-side encryption**

### Interview Punch Lines

-   "State encryption protects sensitive data."
-   "Critical for infrastructure security."

------------------------------------------------------------------------

## 80. How do you restrict **backend access**?

**Access control** ensures only authorized users or systems interact
with Terraform state.

This is implemented through:

-   **Identity permissions**
-   **Role policies**
-   **Network restrictions**
-   **Multi-factor authentication**

### Interview Punch Lines

-   "Backend access must be tightly controlled."
-   "Prevents unauthorized state manipulation."

------------------------------------------------------------------------

## 81. What is **secret scanning**?

**Secret scanning tools** analyze repositories to detect exposed
credentials or sensitive data.

Scanning operates through:

-   **Pattern detection**
-   **Heuristic analysis**
-   **Policy enforcement**

### Interview Punch Lines

-   "Detects exposed credentials early."
-   "Prevents security incidents."

------------------------------------------------------------------------

## 82. How does **Vault integrate** with Terraform?

**Vault** acts as centralized **secret manager** providing **dynamic
credentials** and secure storage.

Terraform integrates by:

-   Retrieving secrets during execution
-   Generating short-lived credentials
-   Avoiding secret exposure

### Interview Punch Lines

-   "Vault externalizes secret management."
-   "Enables dynamic credentials."

------------------------------------------------------------------------

## 83. How do **workspaces** help environment separation?

**Workspaces** allow multiple isolated **state environments** using same
configuration.

This enables managing:

-   Development
-   Testing
-   Production

### Example

``` bash
terraform workspace new dev
terraform workspace new prod
```

### Interview Punch Lines

-   "Workspaces isolate environment state."
-   "They enable multi-environment management."
