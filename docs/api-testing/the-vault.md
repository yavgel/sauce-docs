---
id: the-vault
title: "Storing Reusable Variables and Code Snippets with the Vault"
sidebar_label: Using the Vault
description: "The vault allows you to store variables and code snippets that can be used across an entire project."
---

import useBaseUrl from '@docusaurus/useBaseUrl';

The vault feature allows you to store variables and code snippets to use in your tests in one project, or across all projects.

<!--[Explanation Video](https://www.youtube.com/watch?v=cBNMi30Fj9Q)-->

## Company Vault vs. Project Vault

There are two types of API Testing vaults:

* **Company Vault**, which you can access from the main API Testing dashboard, where your projects are listed:
   <img src={useBaseUrl('img/api-fortress/2021/04/fromDashboard.png')} alt="Access Vault from Dashboard" width="400" />

* **Project Vault**, which you can access from inside one of your projects:
   <img src={useBaseUrl('img/api-fortress/2021/04/vaultFromProject.png')} alt="Access Vault from Project View" />


## Variables Section

In the **Variables** section, you'll have the option to define environment variables to use in your tests. The screenshot below shows the **Company Vault**; these variables are available across all projects.

<img src={useBaseUrl('img/api-fortress/2021/04/company_vault.png')} alt="Company Vault View"/>

Variables you create under the **Project Vault** are only available in that specific project. You should define a variable at this level when you need to use the same one across multiple tests. This way, you don't need to rewrite it every time.

As an example, you could save a password as a variable and reuse it in multiple places. See [password variable example](#the-password-variable) below for more details.

:::info variable scope
If a variable that exists in the Company Vault, also exists in the Project Vault with the same name definition, the latter will override the Company Vault value.
:::

:::tip Import Postman Collections into The Vault
Additionally, you can import variables from Postman. See [here](/api-testing/importing-postman-collections/) for more details.
:::

### Creating a Variable

To create a variable:

1. Navigate to the Project Vault.
1. Select **New Entry**.
1. Add the Key: `domain`.
1. Add the value: `api.us-west-1.com`.
1. Select **Confirm**.

<img src={useBaseUrl('img/api-fortress/2021/04/variableEntry2.png')} alt="Domain Variables"/>

Reference the variable by the key, and the following syntax: `${domain}`.


#### Product Variable

Consider a scenario where an `/product` endpoint requires a specific `id` query parameter.

<img src={useBaseUrl('img/api-fortress/2021/04/productID0.png')} alt="Product ID 0"/>

While this is a perfectly valid request parameter, it can be hard to manage and update if you scale out your tests. Therefore rather than continuously hard-coding this value into the **Query Params** field, a safer and more efficient approach is to export this value into to a variable.

Here is an example of how it could look like in the **Project Vault**:

<img src={useBaseUrl('img/api-fortress/2021/04/productID1.png')} alt="Product ID 1"/>

Now you can switch the **Query Params** field from **String value** to **Variable** and enter the variable name: `product_id` (see the screenshot below). This way if you have multiple tests in your project using the same password.

<img src={useBaseUrl('img/api-fortress/2021/04/productID2.png')} alt="Product ID 2"/>

:::tip code view example
You can also reference this parameter in Code view with the following syntax: `params="['id':product_id]"`.
:::


## Code Snippets Section

All created or imported test component/code examples exist in the snippets section.

:::tip What is a Snippet?
See [here](/api-testing/on-prem/reference/composer-snippets) for more details.
:::

Much like with variable scope, code snippets saved in the specific **Project Vault** are only available in that project. Likewise, snippets saved in the **Company Vault** are available across all projects.

A good use case for the snippets feature is an authentication flow; you don't need nor want to rewrite all authentication steps for every test. Instead, call the snippet that contains these authentication details. See [The Authentication Snippet example below for more details](#the-authentication-snippet). Another good example is integration testing, where you can reuse various tests to create one larger flow.

:::warning Code Snippet Scope
If you have a snippet saved for the current project, but you need to make it available across all projects, you can **export** the snippet from your current project to the Company Vault by using the import/export feature (see screenshot below).

<img src={useBaseUrl('img/api-fortress/2021/04/exportSnippet.png')} alt="Snippet"/>

:::


### Creating a Code Snippet

To create a code snippet:

* Navigate to the desired test
* Select the desired test component
* Select the "Export snippet from selection" icon
* Give the snippet a name
* Select **Save Snippet**

<img src={useBaseUrl('img/api-fortress/2021/04/createSnippet.png')} alt="Creating a Snippet"/>

<img src={useBaseUrl('img/api-fortress/2021/04/snippetDetails.png')} alt="Snippet Details"/>


#### Authentication Snippet

Below is an example of how to create an Authentication Snippet.

1. First, create a new test with a request component that requires basic authentication. For examples, check the [Sauce Labs REST API endpoints](/dev/api/) for ideas.
   <img src={useBaseUrl('img/api-fortress/2021/04/exampleSnippetRequest.png')} alt="Example Snippet Request"/>

1. Select to the **+ Add Request Headers** section below the request component
   <img src={useBaseUrl('img/api-fortress/2021/04/addRequestHeader.png')} alt="Add Request Header"/>

1. Select **Basic Authentication** from the list
   <img src={useBaseUrl('img/api-fortress/2021/04/basicAuth.png')} alt="Basic Auth Component"/>

1. Enter the details for `username` and `password`, then select **Save**.
   <img src={useBaseUrl('img/api-fortress/2021/04/basicAuthDetails.png')} alt="Basic Auth Details Component"/>

1. Once the **Authorization Header** appears, highlight it in the UI, then select the **Export snippet from selection** icon in the toolbar.
   <img src={useBaseUrl('img/api-fortress/2021/04/authSnippet.png')} alt="Auth Snippet screenshot"/>

Consider a scenario where this login will be required for all the endpoints we have to test. It makes sense for this call to be stored in the Vault.

Now you can choose to insert or invoke this snippet in future tests that require a Basic Authentication header.
