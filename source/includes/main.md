# Introduction

Welcome to the TeylorMade API! You can use our API to access TeylorMade API endpoints, and how to call them on your different interfaces.

TeylorMade uses Firebase for authentication and mongodb database from data storage and management.

The api was written with Node.js and the results/ responses examples are in the dark area to the right.

All responses are in JSON and will work perfectly on all platform if implimented correctly.

# Note

> The base URL: BASE URL = https://apis.builtby.rudigo.com/teylormade


Adher to all `PARAMETER` naming convention `STRICTLY` else you will have error issues.

`TOKEN` gotten from either `signup` or `login` CAN BE SEND AS `req.body.token` || `req.query.token` || `req.headers['x-access-token']`"

`TOKEN` are very necessary to be able to navigate through some protected user endpoints

TeylorMade expects for Everyone calling these endpoints to use the base URL in all API requests to the server in a header that looks like the following:

`BASE URL: https://apis.builtby.rudigo.com/teylormade`

<aside class="notice">
You must use  this base Url<code>https://apis.builtby.rudigo.com/teylormade</code> with your codes else you wont get access to the endpoints.
</aside>




# Account Endpoints

## Signup A New User

> JSON Resquest Sample:

```json
  {
    "name": "okoro mike",
    "password": "*******",
    "designer": false,
    "email": "test@test.com",
    "d_o_b": "11122333229900411"
  }
  ```

> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "name": "okoro mike",
    "designer": false,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj"
  }
```
> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "name is required and must be string",
    "code": 400,
    "error": error
  }
```

```json
  {
    "status": "error",
    "description": "A user already exist with same email address",
    "code": 400,
    "error": error
  }
```
```json
  {
    "status": "error",
    "description": "Minors cannot open accounts on teylormade. Minimum age requirement is 13 years",
    "code": 400,
    "error": error
  }
```
This endpoint registers a new user using Basic Authentication.

### HTTP Request

`Method POST`
#### Basic Authentication

`account/signup`


### Post Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
name | string (required)| okoro mike | name must be string else error.
password | string (required)| ****5**f** | password must be string and 6 characters and above else error.
email | string (required)| test@test.com | email must be string and valid email else error.
designer | Boolean (required)| false | if set to true user will be registered as designer else ordinary user.
d_o_b | number (required)| timestamp(1112223345443) | Date of birth must be a valid timestamp (number).



## Login A User

> JSON Resquest Sample:

```json
  {
    "name": "okoro mike",
    "password": "*******",
    "designer": false,
    "email": "test@test.com",
    "d_o_b": "11122333229900411"
  }
  ```

> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "name": "okoro mike",
    "designer": false,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj"
  }
```

```json
  {
    "newUser": true,
    "name": "okoro mike",
    "photo": "photoUrl/gf/jpeg",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj",
  }
```
> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "email or username is required and must be string",
    "code": 400,
    "error": error
  }
```

```json
  {
    "status": "error",
    "description": "no user with the email address or username provided",
    "code": 400,
    "error": error
  }
```

```json
  {
    "status": "error",
    "description": "password is incorrect",
    "code": 400,
    "error": error
  }
```
This endpoint logs a registered user into the system using Basic Authentication.

### HTTP Request

`Method POST`

#### Basic Authentication

`account/login`

### Post Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
password | string (required) | ****5**f** | password must be string and 6 characters and above else error.
email/username | string (required)| test@test.com/mike2000 | email or username must be string and valid email else error.

<aside class="success">
Note: The new user success response are for those that are using either facebook, pinterest or instagram authentication for the first time then use the token and call the endpoint `http://Base Url/account/signup/complete`</aside>


## Auth0 login(F, P, I)

> JSON Resquest Sample:

```json
  {
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj"
  }
  ```

> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "name": "okoro mike",
    "designer": false,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj"
  }
```

```json
  {
    "newUser": true,
    "name": "okoro mike",
    "photo": "photoUrl/gf/jpeg",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj",
  }
```
> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "email or username is required and must be string",
    "code": 400,
    "error": error
  }
```

```json
  {
    "status": "error",
    "description": "no user with the email address or username provided",
    "code": 400,
    "error": error
  }
```

```json
  {
    "status": "error",
    "description": "password is incorrect",
    "code": 400,
    "error": error
  }
```
This endpoint logs a registered user into the system using facebook, instagram, pinterest.

### HTTP Request

`Method POST`

#### Facebook Authentication

`account/login/facebook`

### Post Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
access_token | string (required)| "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj" | token from facebook or instagram or pinterest when using Auth0 authentication

<aside class="success">
Note: The new user success response are for those that are using either facebook, pinterest or instagram authentication for the first time then use the token and call the endpoint `http://Base Url/account/signup/complete`</aside>



## Complete A New User Registration

> JSON Resquest Sample:

```json
  {
    "designer": false,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj",
  }
  ```

> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "name": "okoro mike",
    "designer": false,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj"
  }
```
> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "something unexpected happened",
    "code": 400,
    "error": error
  }
```

This endpoint completes the registration process of a user who used either `facebook`, `pinterest`, `instagram` for authentication the first time to enable them choose a designer flag.

### HTTP Request

`Method POST`

#### New Facebook, Pinterest, or Instagram users

`account/signup/complete`


### Post Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
designer | Boolean (required)| false | if set to true user will be registered as designer else ordinary user.
token | string (required)| "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj" |  token from login using either facebook, pinterest or instagram (only for use with the `newUser: true`flag from any login).



## Get User Profile

> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "coverImageUrl": "coverphotoUrl/gf/jpeg",
    "name": "okoro mike",
    "photo": "photoUrl/gf/jpeg",
    "designer": false,
    "email": "test@test.com",
    "username": "mike12345",
    "phone_number": "080454545444",
    "address": "hiltop avenure",
    "bio": "dark boy",
    "measurement": [{

    }],
    "d_o_b": "11111222333",
    "followers": [{

      }],
    "followers": [{
      
      }],    "status": "be happy",
    "rating": [{
    
    }],   
  }
```
> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "user not found",
    "code": 400,
    "error": error
  }
```
```json
  {
    "status": "error",
    "description": "something unexpected happened",
    "code": 400,
    "error": error
  }
```

This endpoint logs a registered user into the system using Basic Authentication, facebook, instagram, pinterest.

### HTTP Request

`Method GET`

#### get user profile

`/account/profile`

### Query Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
token | string (required)| "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj" | token from either Basic Authentication, facebook ,instagram or pinterest.


<aside class="success">
Note: `TOKEN` gotten from either `signup` or `login` CAN BE SEND AS `req.body.token` || `req.query.token` || `req.headers['x-access-token']`</aside>



## Edit User Profile

> JSON Resquest Sample:

```json
  {
    "name": "okoro mike",
    "username": "mike12345",
    "phone_number": "080454545444",
    "address": "hiltop avenure",
    "bio": "dark boy",
    "d_o_b": 112223444332
  }
  ```


> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "coverImageUrl": "coverphotoUrl/gf/jpeg",
    "name": "okoro mike",
    "photo": "photoUrl/gf/jpeg",
    "designer": false,
    "email": "test@test.com",
    "username": "mike12345",
    "phone_number": "080454545444",
    "address": "hiltop avenure",
    "bio": "dark boy",
    "measurement": [{

    }],
    "d_o_b": "11111222333",
    "followers": [{

      }],
    "followers": [{
      
      }],    "status": "be happy",
    "rating": [{
    
    }],   
  }
```
> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "user not found",
    "code": 400,
    "error": error
  }
```
```json
  {
    "status": "error",
    "description": "something unexpected happened",
    "code": 400,
    "error": error
  }
```

This endpoint logs a registered user into the system using Basic Authentication, facebook, instagram, pinterest.

### HTTP Request

`Method PUT`

#### edit user profile

`account/profile`

### Query Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
name | String (optioal) | okoro mike | new name to be changed to,
phone_number | String (optioal) | 080765444 | new phone number
username | String (optioal) | mikerer | new username,
address | String (optioal)| home | new address,
d_o_b | number(timestamp) (optioal)| 123432230 | new birthday ,
bio | string(optioal) | still black | new discription
token | string (required) | "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj" | token from either Basic Authentication, facebook ,instagram or pinterest.


<aside class="success">
Note: `TOKEN` gotten from either `signup` or `login` CAN BE SEND AS `req.body.token` || `req.query.token` || `req.headers['x-access-token']`</aside>



## Add User measurements

> JSON Resquest Sample:

```json
  {
    "name": "length",
    "value": 41,
    "unit": "cm",
  }
  ```


> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "coverImageUrl": "coverphotoUrl/gf/jpeg",
    "name": "okoro mike",
    "photo": "photoUrl/gf/jpeg",
    "designer": false,
    "email": "test@test.com",
    "username": "mike12345",
    "phone_number": "080454545444",
    "address": "hiltop avenure",
    "bio": "dark boy",
    "measurement": [{
      {
      "name": "length",
      "value": 41,
      "unit": "cm",
      },
      {
      "name": "waist",
      "value": 31,
      "unit": "cm",
      }
    }],
    "d_o_b": "11111222333",
    "followers": [{

      }],
    "followers": [{
      
      }],    "status": "be happy",
    "rating": [{
    
    }],   
  }
```
> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "user not found",
    "code": 400,
    "error": error
  }
```
```json
  {
    "status": "error",
    "description": "something unexpected happened",
    "code": 400,
    "error": error
  }
```

This endpoint enable a logged in user to input his or her measurement details.

### HTTP Request

`Method POST`

#### edit user profile

`account/profile/measurement`

### Query Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
name | String (required) | length | measurement name to be added to user measurement,
value | number (required) | 41 | actual measurement
unit | String (required) | cm | unit of measurement,
token | string (required) | "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj" | token from either Basic Authentication, facebook ,instagram or pinterest.



## Edit user measurements

> JSON Resquest Sample:

```json
  {
    "name": "length",
    "value": 39,
    "unit": "cm",
  }
  ```


> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "coverImageUrl": "coverphotoUrl/gf/jpeg",
    "name": "okoro mike",
    "photo": "photoUrl/gf/jpeg",
    "designer": false,
    "email": "test@test.com",
    "username": "mike12345",
    "phone_number": "080454545444",
    "address": "hiltop avenure",
    "bio": "dark boy",
    "measurement": [{
      {
      "name": "length",
      "value": 39,
      "unit": "cm",
      },
      {
      "name": "waist",
      "value": 31,
      "unit": "cm",
      }
    }],
    "d_o_b": "11111222333",
    "followers": [{

      }],
    "followers": [{
      
      }],    "status": "be happy",
    "rating": [{
    
    }],   
  }
```
> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "user not found",
    "code": 400,
    "error": error
  }
```
```json
  {
    "status": "error",
    "description": "something unexpected happened",
    "code": 400,
    "error": error
  }
```

This endpoint logs a registered user into the system using Basic Authentication, facebook, instagram, pinterest.

### HTTP Request

`Method PUT`

#### edit user measurement based on the query parameters

`account/profile/measurement/:measurementId`

### Query Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
name | String (required) | length | measurement name to be added to user measurement,
value | number (required) | 41 | actual measurement,
unit | String (required) | cm | unit of measurement,
measurementId | String (required) | 34rd2 | ID of the measurment as a request headder,
token | string (required) | "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj" | token from either Basic Authentication, facebook ,instagram or pinterest.




## Delete measurements

> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "data": "Measurement deleted successfully"
  }
```

This deletes a measurement from the user profile based on the ID of the request measurement.

### HTTP Request

`Method DELETE`

#### delete measurement

`account/profile/measurement/:measurementId`

### Query Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
measurementId | String (required) | 34rd2 | ID of the measurment as a request headder,
token | string (required) | "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj" | token from either Basic Authentication, facebook ,instagram or pinterest.




## Change Password

> JSON Resquest Sample:

```json
  {
    "password": "******",
  }
  ```

> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj"
  }
```

Change a user password by the logged in user

### HTTP Request

`Method POST`

#### change user password

`account/profile/edit_password`

### Query Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
password | String (required) | "******" | new user passwsord,
token | string (required) | "eyJhbGciOiJIUzI1NiIsInR5cCI6 *** DlsdkaiwADWRWRfqwdnj" | token from either Basic Authentication, facebook ,instagram or pinterest.



## Account Recovery

> JSON Resquest Sample:

```json
  {
    "email": "test@test.com",
  }
  ```

> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "message": "An email has been sent to test@test.com with further instructions.",
  }
```

> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "No user found with Email",
    "code": 400,
    "error": error
  }
```
```json
  {
    "status": "error",
    "description": "something unexpected happedned",
    "code": 400,
    "error": error
  }
```

Endpoint to recover a user account

### HTTP Request

`Method POST`

#### recover account

`account/recovery/password`

### Query Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
email | String (required) | test@test.com | registered user email for account to be recovered



## Account Recovery changePassword

> JSON Resquest Sample:

```json
  {
    "newPassword": "******",
    "oobCode": "eyadfewfswasdwd769"
  }
  ```

> JSON Response Sample: `STATUS 200 Ok SUCCESS`

```json
  {
    "message": "Password changed successfully. You can now login with your new password.');
  }
```

> JSON Response Sample: `STATUS 400 Bad Request`

```json
  {
    "status": "error",
    "description": "something unexpected happedned",
    "code": 400,
    "error": error
  }
```

Endpoint to change password from account recovery

### HTTP Request

`Method POST`

#### recover account

`account/recovery/password/change`

### Query Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | ----------- 
oobCode | String (required) | pqedwewr45554ffse | oobCode from the email sent to the email
newPassword | String (required) | "*******" | new password user would love to reset to.