---
title: createCompanyRole mutation
contributor_name: Atwix
contributor_link: https://www.atwix.com/
edition: b2b
---

# createCompanyRole mutation

The `createCompanyRole` mutation defines a new company role. To create a role, you must provide an array of permissions that determine which resources the user can access.

import B2BRoles from '/src/_includes/graphql/b2b-roles.md'

<B2BRoles />

Also, you can get the list of all resources defined within the company using the [`company`](../queries/company.md) query.

## Syntax

```graphql
mutation {
    createCompanyRole(
        input: CompanyRoleCreateInput!
    ) {
        CreateCompanyRoleOutput
    }
}
```

## Example usage

This example creates a new company role with a list of company permissions available to the company.

**Request:**

```graphql
mutation {
  createCompanyRole(
    input: {
      name: "Company Admin"
      permissions: [
        "Magento_Company::index"
        "Magento_Company::view"
        "Magento_Company::view_account"
        "Magento_Company::edit_account"
        "Magento_Company::view_address"
        "Magento_Company::edit_address"
        "Magento_Company::contacts"
        "Magento_Company::payment_information"
        "Magento_Company::shipping_information"
        "Magento_Company::user_management"
        "Magento_Company::roles_view"
        "Magento_Company::roles_edit"
        "Magento_Company::users_view"
        "Magento_Company::users_edit"
        "Magento_Company::credit"
        "Magento_Company::credit_history"
      ]
    }
  ) {
    role {
      id
      name
      permissions {
        id
        text
        sort_order
        children {
          id
          text
          sort_order
        }
      }
    }
  }
}
```

**Response:**

```json
{
  "data": {
    "createCompanyRole": {
      "role": {
        "id": "Mg==",
        "name": "Company Admin",
        "permissions": [
          {
            "id": "Magento_Company::index",
            "text": "All",
            "sort_order": 100,
            "children": [
              {
                "id": "Magento_Company::view",
                "text": "Company Profile",
                "sort_order": 100
              },
              {
                "id": "Magento_Company::user_management",
                "text": "Company User Management",
                "sort_order": 200
              },
              {
                "id": "Magento_Company::credit",
                "text": "Company Credit",
                "sort_order": 500
              }
            ]
          }
        ]
      }
    }
  }
}
```

## Input attributes

The `CompanyRoleCreateInput` input object defines the company role data for creating.

### CompanyRoleCreateInput attributes

The `CompanyRoleCreateInput` object contains the following attributes:

Attribute |  Data Type | Description
--- | --- | ---
`name` | String! | The name of the role to create
`permissions` | [String!]! | A list of resources the role can access

## Output attributes

The `CreateCompanyRoleOutput` output object contains the following attribute:

Attribute |  Data Type | Description
--- | --- | ---
`role` | CompanyRole! | Contains company role data

### CompanyRole attributes

import CompanyRole from '/src/_includes/graphql/company-role.md'

<CompanyRole />

## Errors

Error | Description
--- | ---
`User role with this name already exists. Enter a different name to save this role.` | The company cannot have multiple company roles with the same name.
`Unable to set "allow" for the resource because its parent resource(s) is set to "deny".` | To allow permission for the company role, you must allow all the permissions of the parent tree.
