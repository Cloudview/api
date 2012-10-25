# Account

When [authenticated](./authentication.md) the user will have access to very basic **account** details.

## Endpoints

* [Details](#get-account-details) - `GET /account/details.[json|xml]`


*******************

## Get Account Details

Gets basic account details for currently [authenticated](./authentication.md) user.

```
GET /account/details.[json|xml]
```

### Parameters

*No parameters needed*

### Results

An `account detail` object, containing:
   - display_name
   - first_name
   - last_name
   - email
   - address_1
   - address_2
   - address_3
   - postcode
   - county
   - country
   - mobile
   - day_phone
   - company   


******************

[Back to main page](../README.md)

