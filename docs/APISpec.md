# API Specification
Base URL: `~/api`
## 1. Properties
### 1.1 Show Properties `/properties` - GET
Allows users to see all properties available on the database

Returns: 
```commandline
[
    {
        "properties_id": <id>,
        "property_name": <string>,
        "estimated_cleaning_mins": <smallint>,
        "double_unit": Array<id>,
        "address": {
            "city": <string>,
            "address": <string>,
            "country": <string>,
            "state_name": <string>,
            "postal_code": <int>
        },
        "status": {
            "status": <string>,
            "status_id": <smallint>
        }
    }
]
```
### 1.2 Get Property - `/properties/{properties_id}` - GET
Gets full information about a single property

Returns:
```commandline
{
    "properties_id": <id>,
    "property_name": <string>,
    "estimated_cleaning_mins": <smallint>,
    "double_unit": Array<id>,
    "address": {
        "city": <string>,
        "address": <string>,
        "country": <string>,
        "state_name": <string>,
        "postal_code": <int>
    },
    "status": {
        "status": <string>,
        "status_id": <smallint>
    }
}
```
### 1.3 Assign Property settings - `/properties/{properties_id}` - PUT
Gets full information about a single property

Input:
```commandline
{
    "estimated_cleaning_mins": <smallint>,
    "double_unit": Array<id>
}
```
Returns:
```commandline
{
    "properties_id": <id>,
    "property_name": <string>,
    "estimated_cleaning_mins": <smallint>,
    "double_unit": Array<id>,
    "address": {
        "city": <string>,
        "address": <string>,
        "country": <string>,
        "state_name": <string>,
        "postal_code": <int>
    },
    "status": {
        "status": <string>,
        "status_id": <smallint>
    }
}
```

## 2. Staff
### 2.1 Show Staff - `/staff` - GET
Allows users to see all staff populated from ResortCleaning and any information
linked from Homebase

Returns:
```commandline
[
    {
        "user_id": <id>,
        "name": <string>,
        "first_name": <string>,
        "last_name": <string>,
        "role": {
            "role_id": <id>,
            "title": <string>
        },
        "status": {
            "status": <string>,
            "status_id": <smallint>
        }
    }
]
```
### 2.2 Get Staff - `/staff/{user_id}` - GET
Gets full information about a single staff member including more detailed 
information about their role

Returns:
```commandline
{
    "user_id": <id>,
    "name": <string>,
    "first_name": <string>,
    "last_name": <string>,
    "role": {
        "role_id": <id>,
        "title": <string>,
        "priority": <int>,
        "can_clean": <bool>,
        "description": <string>,
        "can_lead_team": <bool>
    },
    "status": {
        "status": <string>,
        "status_id": <smallint>
    }
}
```
<!-- ### 2.3 Assign Staff Role - `/staff/{user_id}/role` - PUT
Change the role of the given staff member

Input:
```commandline
{
    "role_id": <id>
}
```
Returns:
```commandline
[
    {
        
    }
]
``` -->

## 3. Roles
### 3.1 Show Roles - `/roles` - GET
Returns all roles linked from Homebase

```commandline
[
    {
        "role_id": <id>,
        "title": <string>,
        "description": <string>,
        "priority": <int>,
        "can_lead_team": <bool>,
        "can_clean": <bool>
    }
]
```
### 3.2 Get Role - `/roles/{role_id}` - GET
Gets full information about a single role

```commandline
{
    "role_id": <id>,
    "title": <string>,
    "description": <string>,
    "priority": <int>,
    "can_lead_team": <bool>,
    "can_clean": <bool>
}
```
### 3.3 Assign Role Settings - `/roles/{role_id}` - PUT
Change settings for specified role

Input:
```commandline
{
    "description": <string>,
    "priority": <int>,
    "can_lead_team": <bool>,
    "can_clean": <bool>
}
```
Returns:
```commandline
{
    "role_id": <id>,
    "title": <string>,
    "description": <string>,
    "priority": <int>,
    "can_lead_team": <bool>,
    "can_clean": <bool>
}
```

## 4. Appointments
### 4.1 Show Appointments - `/appointments` - GET
Allows users to see all properties available on the database
#### Note: Appointment data is only regularly updated for appointments ranging from the previous day to plus 9 days

Query Parameters:
- `per_page`: number from 1 to 1000 - indicates maximum number of appointment records to return
- `page`: number from 0 - indicates which page of results to return
- `from_service_date`: date YYYY-MM-DD - filters out any appointments with service date before this value
- `to_service_date`: date YYYY-MM-DD - filters out any appointments with service date after this value

Returns:
```commandline
[
    {
        "appointment_id": <id>,
        "arrival_time": <string (ISO Timestamp)>,
        "service_time": <string (ISO Timestamp)>,
        "next_arrival_time": <string (ISO Timestamp)>,
        "turn_around": <bool>,
        "cancelled_date": <string (ISO Timestamp)>,
        "service": <id>,
        "property": {
            "properties_id": <id>,
            "property_name": <string>
        },
        "staff": [
            {
                "user_id": <id>,
                "staff_info": {
                    "name": <string>
                }
            }
        ],
        "status": {
            "status": <string>,
            "status_id": <smallint>
        }
    }
]
```
### 4.2 Get Appointment - `/appointments/{appointment_id}` - GET
Gets full information about a single appointment

Returns:
```commandline
{
    "appointment_id": <id>,
    "arrival_time": <string (ISO Timestamp)>,
    "service_time": <string (ISO Timestamp)>,
    "next_arrival_time": <string (ISO Timestamp)>,
    "turn_around": <bool>,
    "cancelled_date": <string (ISO Timestamp)>,
    "service": <id>,
    "property": {
        "properties_id": <id>,
        "property_name": <string>
    },
    "staff": [
        {
            "user_id": <id>,
            "staff_info": {
                "name": <string>
            }
        }
    ],
    "status": {
        "status": <string>,
        "status_id": <smallint>
    }
}
```

## 5. Schedule Plans
### 5.1 Show Plans - `/plans` - GET

Query Parameters:
- `per_page`: number from 1 to 1000 - indicates maximum number of appointment records to return
- `page`: number from 0 - indicates which page of results to return
- `from_plan_date`: date YYYY-MM-DD - filters out any appointments with service date before this value
- `to_plan_date`: date YYYY-MM-DD - filters out any appointments with service date after this value

### 5.2 Get Plan - `/plans/{plan_id}` - GET

### 5.3 Add Staff to Plan - `/plans/{plan_id}/staff/{user_id}/add` - POST

### 5.4 Remove Staff from Plan - `/plans/{plan_id}/staff/{user_id}/remove` - DELETE

### 5.5 Add Appoinment to Plan - `/plans/{plan_id}/appointment/{appoinment_id}/add` - POST

### 5.6 Remove Appoinment from Plan - `/plans/{plan_id}/appointment/{appoinment_id}/remove` - DELETE

### 5.7 Send Plan to ResortCleaning - `/plans/send/{plan_date}` - POST