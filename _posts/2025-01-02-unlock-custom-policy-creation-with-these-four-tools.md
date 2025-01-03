---
title: "Unlock Custom Azure Policy Creation With These Four Tools"
categories:
  - Blog
tags:
  - Azure
  - Azure Policy
---

At some point in our Azure Policy journey, we will want to start creating our own custom Policies.

## The Initial Approach

In the beginning, my approach looked like this:

1. Find an existing policy that looks like what I’m after.
2. Copy the code, then modify it until it looked right.
3. Continue modifying it until the JSON errors finally stopped.
4. Save it.
5. Assign it.
6. Pray.

Sound familiar?

I’d eventually get it to work, but I didn’t understand how it was working. I relied heavily on existing examples, missing out on key knowledge.

It wasn’t until I learned a simple yet critical part of Azure Policy that the guesswork finally ended. In a true lightbulb moment, it magically 'clicked':

**Azure Policy uses Aliases.**

Today, we’ll unlock freestyle Azure Policy creation by learning about **Aliases** and the four tools that make working with them a breeze.



## What Are Aliases?

Azure Policy uses an Alias system to map Policy Rules to resource properties in Azure's backend APIs.

When we want to evaluate a resource property, we must specify its **Alias** in the Policy Rule instead of the property itself.

Lets take a look:

![Azure Policy Rule](/assets/images/unlock-custom-policy-creation-with-these-four-tools/img_1.png)


- **Alias**: `Microsoft.Storage/storageAccounts/publicNetworkAccess`

This is the Alias of the Storage Account Public Network Access property.



The actual property path, including namespace and resource type is:



- **Actual property path**:
  `Microsoft.Storage/storageAccounts.properties.publicNetworkAccess`

### Key Points:
- Azure Policy only supports Aliases in Policy Rules.
- There are over **72,000 Aliases** available.
- Not all properties have an Alias.
- Aliases are of two types: **Single** and **Array**.
- Aliases are fully managed by Microsoft.

So with lots of Aliases available, yet not all properties covered, how can we find the right ones, and avoid ones that don't exist?



## Finding Aliases

Finding Aliases quickly is key to fast and effective policy creation.

There are several tools available to help:

### 1. **[AzAdvertizer](https://www.azadvertizer.net/azpolicyaliasesadvertizer_singlelinesx.html)**

AzAdvertizer is a must-have tool for anyone working with Azure Policy. It provides a massive directory of existing Policies and Aliases with extensive search and filter capabilities.

#### Features:
- Search over 4k policies and 72k Aliases.
- View every Alias and its associated path in one place.
- Quickly discover Aliases and resource properties using filters.
- Find Aliases already used by existing Policies to avoid duplication.
- Stay updated with changes.

As it’s a website, you can keep it open in a browser while developing Policy Rules in VS Code.



### 2. **Azure Policy Visual Studio Code Extension**

The [Azure Policy VS Code Extension](https://learn.microsoft.com/en-us/azure/governance/policy/how-to/extension-for-vscode) provides a local, offline playground for creating and testing Policies.

#### Features:
- View deployed resources and policies in one place.
- Discover Aliases immediately by hovering over resource properties.
- Perform evaluations locally, with no need to deploy to Azure.
- Export JSON files for use elsewhere (e.g., Policy-as-Code).

[Install it via VS Code](https://marketplace.visualstudio.com/items?itemName=AzurePolicy.azurepolicyextension).



### 3. **PowerShell & CLI**

The command-line approach is always available if needed.

#### PowerShell Example:
```powershell
# Use Get-AzPolicyAlias to list available providers
Get-AzPolicyAlias -ListAvailable

# Get Azure Policy aliases for a specific Namespace
(Get-AzPolicyAlias -NamespaceMatch 'compute').Aliases
```

#### CLI Example:

```shell
# List namespaces
az provider list --query [*].namespace

# Get Azure Policy aliases for a specific Namespace

az provider show --namespace Microsoft.Compute --expand "resourceTypes/aliases" --query "resourceTypes[].aliases[].name"
```

It’s less efficient then previous tools, but it’s always there if needed.

[https://learn.microsoft.com/en-us/azure/governance/policy/concepts/definition-structure-alias](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/definition-structure-alias)



### 4. **Resource Explorer**

Resource Explorer is a helpful tool when testing and troubleshooting Policies. It gives behind the scene insights of our resources, showing their properties in raw json code.

We can:

 - Verify properties of existing resources.
 - Validate resource conditions when testing Policy implementations.
 - Troubleshoot policies which aren't evaluating as expected.



For example:

I wanted to audit Storage Accounts with SFTP enabled (it’s expensive).

Here’s the Rule:


Some Storage Accounts weren’t evaluating correctly. Looking in Resource Explorer I quickly found the problem:




My Policy Rule was checking if the isSftpEnabled property exists, not if it was enabled. I wasn't bothered about it existing, as long as it was disabled.

When I changed the Policy Rule to “exists”: “true” it evaluated as expected.

Resource explorer highlighted this almost immediately and the Policy Rule was fixed in a couple of minutes.



Resource Explorer can be accessed directly in the Azure Portal via the search bar. We can keep it open in a separate tab when troubleshooting policies.







That's it!

Hopefully discovering Aliases has triggered a lightbulb moment for you, just as it did for me.

All that remains is practice, practice, practice, and you'll be an Azure Policy Machine in no time!



If this has been helpful please give it a thumbs up!