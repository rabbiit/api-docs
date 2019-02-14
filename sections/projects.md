# Projects

* [The project object](#object)
    * [Attributes](#object-attributes)
    * [Response JSON](#object-json)
* [Get all projects](#list)
* [Retrieve a project](#retrieve)
* [Create a project](#create)
* [Update a project](#update)
* [Delete a project](#delete)

<a name="object"></a>
## The project object

<a name="object-attributes"></a>
#### Project attributes

Attribute|Type|Description
---------|----|-----
id | integer | `Readonly` Unique identifier for project
name | text | Project name 
description | text | Project description
active | boolean | If active is `true` project members can create and edit time entries.
privacy | integer | Possible values are `1` for public and `2` for private.
customer_id | integer | Id of the customer
required_task | boolean | Define if field task is required on time entries children
billable | boolean | Define if project is billable per hour
bill_by | text | Type of billable. Possible values are `project` or `user`.
rate | decimal | Rate per hour per project when project is billable. Deafult is `0`.
template | boolean | Define project as template. Default is `false`.
date_created | datetime | `Readonly` Date and time when the project was created
date_updated | datetime | `Readonly` Date and time when the project was last updated
privacy_s | text | `Readonly` Type of privacy.
customer_name | integer |  `Readonly` Name of the customer
created_by | integer | `Readonly` Id of user who created the project
status | text | `Readonly` If active field is `true` retrieve `active` or if is `false` then `archived`.
is_member | boolean | `Readonly` Indiques if the current user is a team member of the project.
is_manager | boolean | `Readonly` Indiques if the current user is a project manager member of the project.
value_total | decimal | `Readonly` Amount total calculated of honoraries for the project.
time_total | time | `Readonly` Time total of time entries for the project.
total_members | integer | `Readonly` Counter of team members active on project.
total_active_tasks | integer | `Readonly` Counter of tasks active on project.

<a name="object-json"></a>
#### Project Response JSON

```json
{
    "data": {
        "id": 60,
        "customer_id": 3,
        "customer_name": "My Customer",
        "name": "New Project",
        "description": null,
        "date_created": "2019-02-14T02:59:42-0200",
        "date_changed": null,
        "privacy": 2,
        "privacy_s": "private",
        "required_task": 0,
        "created_by": 1,
        "deleted_by": null,
        "billable": 0,
        "bill_by": "project",
        "active": true,
        "status": "active",
        "template": false,
        "is_member": true,
        "is_manager": true,
        "rate": null,
        "value_total": null,
        "time_total": "00:00:00",
        "total_members": 1,
        "total_active_tasks": 0
    }
} 
```

<a name="list"></a>
## List all projects

**GET** `/api/v1/projects`

Example request

```shell
curl https://app.rabbiit.com/api/v1/projects
-H "Authorization: Bearer FrxRtCwWut3PMp9Boj7FQ9ndyZYQggcIF8xtpByI0Fis6-KPOzB1Ownj0b"
```

Example response:
```json
{
    "data": [
        {
            "id": 60,
            "customer_id": 3,
            "customer_name": "My Customer",
            "name": "New Project",
            "description": null,
            "date_created": "2019-02-10T22:59:42-0200",
            "date_changed": null,
            "privacy": 2,
            "privacy_s": "private",
            "required_task": 0,
            "created_by": 1,
            "deleted_by": null,
            "billable": 0,
            "bill_by": "project",
            "active": true,
            "status": "active",
            "template": false,
            "is_member": true,
            "is_manager": true
        },
        {
            "id": 88,
            "customer_id": 4,
            "customer_name": "Big Customer",
            "name": "Project Teste",
            "description": null,
            "date_created": "2019-02-12T12:59:42-0200",
            "date_changed": null,
            "privacy": 2,
            "privacy_s": "private",
            "required_task": 0,
            "created_by": 1,
            "deleted_by": null,
            "billable": 0,
            "bill_by": "project",
            "active": true,
            "status": "active",
            "template": false,
            "is_member": true,
            "is_manager": true
        }
    ]
} 
```

<a name="retrieve"></a>
## Retrieve a project

**GET** `/api/v1/projects/60`

Example request

```shell
curl https://app.rabbiit.com/api/v1/projects/60
-H "Authorization: Bearer FrxRtCwWut3PMp9Boj7FQ9ndyZYQggcIF8xtpByI0Fis6-KPOzB1Ownj0b"
```

Example response:
* See [Project response JSON](#object-json)

<a name="create"></a>
## Create a project

**POST** `/api/v1/projects`

Arguments:

* Can be used the `non-readonly` [project attributes](#project-attributes).

Example request:

```shell
curl https://app.rabbiit.com/api/v1/projects
-H "Authorization: Bearer FrxRtCwWut3PMp9Boj7FQ9ndyZYQggcIF8xtpByI0Fis6-KPOzB1Ownj0b"
-d name="New Project"
-d privacy=2
-d customer_id=3
```

Example response:
* See [Project response JSON](#object-json)

<a name="update"></a>
## Update a project

**POST** `/api/v1/projects/60`

Arguments:

* Can be used the `non-readonly` [project attributes](#project-attributes).
* You can informe only attributes that you want change.

Example request to archive a project:

```shell
curl https://app.rabbiit.com/api/v1/projects/60
-H "Authorization: Bearer FrxRtCwWut3PMp9Boj7FQ9ndyZYQggcIF8xtpByI0Fis6-KPOzB1Ownj0b"
-d active=false
```

Example response:
* See [Project response JSON](#object-json)

<a name="delete"></a>
## Delete a project

**DELETE** `/api/v1/projects/60`

Example request:

```shell
curl -X DELETE https://app.rabbiit.com/api/v1/projects/60
-H "Authorization: Bearer FrxRtCwWut3PMp9Boj7FQ9ndyZYQggcIF8xtpByI0Fis6-KPOzB1Ownj0b"
```

Response body empty with status code `200`.
