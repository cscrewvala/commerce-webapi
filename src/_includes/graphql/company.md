The `Company` object can contain the following attributes:

Attribute | Data type | Description
--- | --- | ---
`acl_resources` | [[CompanyAclResource]](#companyaclresource-attributes) | Returns the list of all resources defined within the company
`company_admin` | [Customer](/src/pages/graphql/schema/customer/queries/customer.md) | An object containing information about the company administrator
`credit` | CompanyCredit! | The company credit balance
`credit_history(filter: CompanyCreditHistoryFilterInput, pageSize: Int = 20, currentPage: Int = 1)` | CompanyCreditHistory! | A history of company credit operations
`email` | String | The email address of the company contact
`id` | ID! | The unique ID of a `Company` object
`legal_address` | [CompanyLegalAddress](#companylegaladdress-attributes) | The address where the company is registered to conduct business
`legal_name` | String | The full legal name of the company
`name` | String | The name of the company
`payment_methods` | [String] | The list of payment methods available to a company
`reseller_id` | String | The resale number that is assigned to the company for tax reporting purposes
`role(id: ID!)` | [CompanyRole](#companyrole-attributes) | Returns a company role filtered by the unique ID for a `CompanyRole` object
`roles(pageSize: Int = 20, currentPage: Int = 1 )` | [CompanyRoles!](#companyroles-attributes) | Returns the list of company roles
`sales_representative` |  [CompanySalesRepresentative](#companysalesrepresentative-attributes) | The company sales representative
`structure(rootId: ID = 0 depth: Int = 10 )` | [CompanyStructure](#companystructure-attributes) | Returns the company structure of teams and customers in depth-first order
`team(id: ID!)` | [CompanyTeam](#companyteam-attributes) | Returns company team data filtered by the unique ID for a `CompanyTeam` object
`user(id: ID!)` | [Customer](/src/pages/graphql/schema/customer/queries/customer.md) | Returns a company user filtered by the unique ID for a `Customer` object
`users(filter: CompanyUsersFilterInput, pageSize: Int = 20, currentPage: Int = 1)`| [CompanyUsers](#companyusers-attributes) | Returns a list of company users based on activity status
`vat_tax_id` | String | The value-added tax number that is assigned to the company by some jurisdictions for tax reporting purposes

### CompanyAclResource attributes

The `CompanyAclResource` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`children` | [CompanyAclResource!] | An array of sub-resources
`id` | ID! | The unique ID for a `CompanyAclResource` object
`sort_order` | Int | The sort order of an ACL resource
`text` | String | The label assigned to the ACL resource

### CompanyAdmin attributes

The `CompanyAdmin` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`email` | String! | The email address of the company administrator
`firstname` | String! | The company administrator's first name
`gender` | Int | The company administrator's gender (Male - 1, Female - 2, Not Specified - 3)
`id` | ID! | The unique ID for a `CompanyAdmin` object
`job_title` | String | The job title of the company administrator
`lastname` | String! | The company administrator's last name

### CompanyCredit

The `CompanyCredit` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`available_credit` | Money! | The amount of company credit available
`credit_limit` | Money! | The company's credit limit
`outstanding_balance` | Money! | The outstanding company credit amount

### CompanyCreditHistory attributes

The `CompanyCreditHistory` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`items` | [[CompanyCreditOperation]!](#companycreditoperation-attributes) | An array of company credit operations
`page_info` | SearchResultPageInfo! | Metadata for pagination rendering
`total_count` | Int | The number of the company credit operations matching the specified filter

### CompanyCreditHistoryFilterInput attributes

The `CompanyCreditHistoryFilterInput` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`custom_reference_number` | String | Filters by the purchase order number associated with the company credit operation
`operation_type` | CompanyCreditOperationType | An enum that defines the type of the company credit operation. Possible values are ADMIN and CUSTOMER
`updated_by` | String | Filters by the name of the person submitting the company credit operation

### CompanyCreditOperation attributes

The `CompanyCreditOperation` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`amount` | Money | The amount of the company credit operation
`balance` | [CompanyCredit!](#companycredit) | The credit balance after the company credit operation
`custom_reference_number` | String | The purchase order number associated with the company credit operation
`date` | String! | The date the operation was performed
`type` | CompanyCreditOperationType! | The type of the company credit operation. Possible values are ALLOCATION, PURCHASE, REFUND, REIMBURSEMENT, REVERT, UPDATE
`updated_by` | [CompanyCreditOperationUser!](#companycreditoperationuser-attributes) | The company user submitting the company credit operation

### CompanyCreditOperationUser attributes

The `CompanyCreditOperationUser` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`name` | String! | The name of the company user submitting the company credit operation
`type` | CompanyCreditOperationUserType! | The type of the company user submitting the company credit operation. Possible values are ADMIN and CUSTOMER

### CompanyLegalAddress attributes

The `CompanyLegalAddress` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`city` | String! | The city where the company is registered to conduct business
`country_code` | CountryCodeEnum! | Company's country ID. See the [`countries` query](/src/pages/graphql/schema/store/queries/countries.md)
`postcode` | String! | The company's postal code
`region` | CustomerAddressRegionInput! | An object containing the region name and/or region ID where the company is registered to conduct business
`street` | [String!]! | An array of strings that define the street address where the company is registered to conduct business
`telephone` | String! | The primary phone number of the company.

### CompanyRole attributes

The `CompanyRole` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`id`| ID! | The unique ID for a `CompanyRole` object
`name` | String | The name assigned to the role
`permissions` | [CompanyAclResource] | A list of permission resources defined for a role
`users_count` | Int | The total number of users assigned the specified role

### CompanyRoles attributes

The `CompanyRoles` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`items` | [CompanyRole]! | A list of company roles that match the specified filter criteria
`page_info` | SearchResultPageInfo | Pagination metadata
`total_count` | Int! | The total number of roles matching the specified filter

### CompanySalesRepresentative attributes

The `CompanySalesRepresentative` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`email` | String! | The email address of the company sales representative
`firstname` | String! | The company sales representative's first name
`lastname` | String! | The company sales representative's last name

### CompanyStructure attributes

The `CompanyStructure` object can contain the following attribute.

Attribute |  Data Type | Description
--- | --- | ---
`items` | [CompanyStructureItem] | An array of elements in a company structure

### CompanyStructureItem attributes

The `CompanyStructureItem` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`entity` | CompanyStructureEntity | A union of [CompanyTeam](#companyteam-attributes) and [Customer](/src/pages/graphql/schema/customer/queries/customer.md) objects
`id` | ID! | The unique ID for a `CompanyStructureItem` object
`parent_id` | ID | The ID of the parent item in the company hierarchy

### CompanyTeam attributes

import CompanyTeam from '/src/_includes/graphql/company-team.md'

<CompanyTeam />

### CompanyUsers attributes

The `CompanyUsers` object can contain the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`items` | [[Customer]!](/src/pages/graphql/schema/customer/queries/customer.md) | An array of `CompanyUser` objects that match the specified filter criteria
`page_info` | SearchResultPageInfo | Pagination metadata
`total_count` | Int! | The number of objects returned
