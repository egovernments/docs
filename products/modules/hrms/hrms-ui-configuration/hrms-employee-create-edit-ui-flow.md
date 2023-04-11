# HRMS Employee Create-Edit UI Flow

### Case: **Create**

URL- digit-ui/employee/hrms/create

Logged Users can Create Employees by providing the necessary Details

If a user enters a mobile number that already exists in the system - Then the application will give an error message.

The Boundary is auto-filled with current `TenantId`. The user is able to add Multiple Jurisdictions and Assignments.

![](<../../../../.gitbook/assets/image (256).png>)

![](<../../../../.gitbook/assets/image (258).png>)

![](<../../../../.gitbook/assets/image (179).png>)

![](<../../../../.gitbook/assets/image (171) (1).png>)

| Sl.No. | API                            | Role        | Access ID |
| ------ | ------------------------------ | ----------- | --------- |
| 1      | `/egov-hrms/employees/_create` | HRMS\_ADMIN | 1750      |
| 2      | `/egov-hrms/employees/_search` | HRMS\_ADMIN | `1752`    |

Primary Files: [https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/createEmployee.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/createEmployee.js)

### Case: **Edit**

URL- digit-ui/employee/hrms/edit/{Employee Id}

Logged Users can Edit Employee Details. Employee Id is disabled.

| API                            | Role        | Access ID |
| ------------------------------ | ----------- | --------- |
| `/egov-hrms/employees/_update` | HRMS\_ADMIN | `1751`    |

Primary Files: [https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EditEmployee/EditForm.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EditEmployee/EditForm.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EditEmployee/index.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EditEmployee/index.js)

### MDMS API

```
 moduleDetails: [
    {
      moduleName: "common-masters",
      masterDetails: [
        { name: "Department", filter: "[?(@.active == true)]" },
        { name: "Designation", filter: "[?(@.active == true)]" },
      ],
    },
    {
      moduleName: "tenant",
      masterDetails: [{ name: "tenants" }],
    },
    {
      moduleName: "ACCESSCONTROL-ROLES",
      masterDetails: [{ name: "roles", filter: "$.[?(@.code!='CITIZEN')]" }],
    },
    { moduleName: "egov-location", masterDetails: [{ name: "TenantBoundary" }] },
  ]
```
