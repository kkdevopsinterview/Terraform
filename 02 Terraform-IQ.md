## **16. What is input variable?**

An **input variable** in Terraform is used to make configurations
**flexible and reusable**. Instead of hardcoding values like **instance
type, region, or resource names** inside configuration files, input
variables allow values to be supplied dynamically.

They act like **function parameters** in programming. By using
variables, the same Terraform code can deploy infrastructure in
different environments without modification.

Input variables help in:

**reusability**

**environment customization**

**separating configuration from logic**

**improving maintainability**

Variables are defined in configuration and referenced wherever needed.

**Real-World Example**

Using a variable for **instance size** so dev uses small resources while
production uses larger ones.

**Interview Punch Lines**

"Input variables parameterize Terraform configuration."

"They improve flexibility and reuse."

------------------------------------------------------------------------

## **17. How to define default values?**

**Interview Explanation**

**Default values** for variables are defined within the **variable
declaration**. This allows Terraform to use predefined values if no
external value is provided.

Defining defaults improves **usability** and reduces required inputs,
especially for common settings.

Defaults are helpful for:

**standard environment values**

**reducing CLI inputs**

**simplifying module usage**

However, **sensitive or environment-specific values** should not rely on
defaults.

**Real-World Example**

Setting default **region** to avoid specifying repeatedly.

**Interview Punch Lines**

"Defaults provide fallback values."

"They simplify configuration reuse."

------------------------------------------------------------------------

## **18. What is terraform.tfvars?**

**Interview Explanation**

The **terraform.tfvars file** is used to assign values to **input
variables** automatically.

Terraform loads this file during execution and uses values defined there
without needing manual input.

Benefits include:

**separating configuration from code**

**environment-specific settings**

**easier collaboration**

It improves organization of **variable management**.

**Real-World Example**

Different tfvars files for **dev and production**.

**Interview Punch Lines**

"tfvars provides variable values externally."

"It separates configuration from logic."

------------------------------------------------------------------------

## **19. How to pass variable from CLI?**

**Interview Explanation**

Variables can be supplied during execution through **command-line
arguments**.

This is useful for:

**temporary overrides**

**pipeline automation**

**dynamic deployments**

CLI variables override many other sources and provide immediate
flexibility.

However, managing many CLI inputs can become difficult, so they are
usually used selectively.

**Real-World Example**

CI/CD pipeline injecting **environment-specific variables**.

**Interview Punch Lines**

"CLI variables allow dynamic runtime input."

"They support automation workflows."

------------------------------------------------------------------------

## **20. What is output variable?**

**Interview Explanation**

**Output variables** display useful information after Terraform
execution.

They expose values like:

**IP addresses**

**resource IDs**

**URLs**

Outputs allow other modules or systems to consume infrastructure
information.

They improve **visibility and integration**.

**Real-World Example**

Displaying **server endpoint** after deployment.

**Interview Punch Lines**

"Outputs expose infrastructure details."

"They support integration and visibility."

------------------------------------------------------------------------

## **21. Sensitive variables?**

**Interview Explanation**

**Sensitive variables** store confidential data like **passwords or API
keys**.

Terraform prevents these values from appearing in logs or output.

They protect:

**credentials**

**secrets**

**tokens**

Security of sensitive values is critical to avoid exposure.

**Real-World Example**

Database password stored as **sensitive variable**.

**Interview Punch Lines**

"Sensitive variables protect confidential data."

"They prevent accidental exposure."

------------------------------------------------------------------------

## **22. Variable precedence order**

**Interview Explanation**

Terraform resolves variable values based on **priority order**.

Highest priority overrides lower ones.

Typical order:

**1️⃣ CLI input**\
**2️⃣ tfvars files**\
**3️⃣ environment variables**\
**4️⃣ defaults**

Understanding precedence prevents unexpected values during execution.

**Real-World Example**

Pipeline value overriding **default configuration**.

**Interview Punch Lines**

"Precedence determines final variable value."

"Higher priority sources override lower."

------------------------------------------------------------------------

## **23. Environment variables in Terraform**

**Interview Explanation**

Terraform can read variables from **system environment variables**.

This enables secure and dynamic value injection without modifying files.

It's especially useful in **automation pipelines**.

Environment variables improve:

**security**

**automation**

**portability**

**Real-World Example**

CI/CD setting **credentials through environment variables**.

**Interview Punch Lines**

"Environment variables enable secure automation."

"They support dynamic configuration."

------------------------------------------------------------------------

## **24. What is locals block?**

**Interview Explanation**

**Locals** allow defining **internal reusable values** inside Terraform
configuration.

Unlike input variables, locals are not provided externally. They are
computed or defined within the configuration for internal logic.

They help:

**reduce duplication**

**improve readability**

**organize expressions**

Locals act like **internal constants**.

**Real-World Example**

Constructing **naming patterns** used across multiple resources.

**Interview Punch Lines**

"Locals define reusable internal values."

"They improve maintainability."

------------------------------------------------------------------------

## **25. When to use locals?**

**Interview Explanation**

Locals should be used when values are **derived or reused internally**
rather than passed externally.

Use cases include:

**computed expressions**

**naming conventions**

**shared configuration fragments**

They simplify complex logic and reduce repetition.

Using locals correctly improves **configuration clarity**.

**Real-World Example**

Building **environment-specific naming strings** reused across
resources.

**Interview Punch Lines**

"Use locals for internal reusable logic."

"They simplify complex configuration."
