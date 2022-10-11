## API Documentation

## FEATURE 0: USER AUTHORIZATION

### All endpoints that require authentication

All endpoints that require a current user to be logged in.

* Request: endpoints that require authentication
* Error Response: Require authentication
  * Status Code: 401
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Authentication required",
      "status_code": 401
    }
    ```

### All endpoints that require proper authorization

All endpoints that require authentication and the current user does not have the
correct role(s) or permission(s).

* Request: endpoints that require proper authorization
* Error Response: Require proper authorization
  * Status Code: 403
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Forbidden",
      "status_code": 403
    }
    ```

### Get the Current User

Returns the information about the current user that is logged in.

* Require Authentication: true
* Request
  * Method: GET
  * URL: /api/session
  * Body: none

* Successful Response
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "id": 1,
      "first_name": "John",
      "last_name": "Smith",
      "email": "john.smith@gmail.com",
      "username": "JohnSmith",
      "user_avatar":"image.url"
    }
    ```
### Get the Current User

Returns the information about the current user that is logged in.

* Require Authentication: true
* Request
  * Method: GET
  * URL: /api/session
  * Body: none

* Successful Response
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "id": 1,
      "first_name": "John",
      "last_name": "Smith",
      "email": "john.smith@gmail.com",
      "username": "JohnSmith",
      "user_avatar":"image.url"
    }
    ```
### Log In a User

Logs in a current user with valid credentials and returns the current user's
information.

* Require Authentication: false
* Request
  * Method: POST
  * URL: /api/session
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "credential": "john.smith@gmail.com",
      "password": "secret password"
    }
    ```

* Successful Response
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "id": 1,
      "first_name": "John",
      "last_name": "Smith",
      "email": "john.smith@gmail.com",
      "username": "JohnSmith",
      "token": ""
    }
    ```

* Error Response: Invalid credentials
  * Status Code: 401
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Invalid credentials",
      "status_code": 401
    }
    ```

* Error response: Body validation errors
  * Status Code: 400
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Validation error",
      "status_code": 400,
      "errors": {
        "credential": "Email or username is required",
        "password": "Password is required"
      }
    }
    ```
### Sign Up a User

Creates a new user, logs them in as the current user, and returns the current
user's information.

* Require Authentication: false
* Request
  * Method: POST
  * URL: /api/users
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "first_name": "John",
      "last_name": "Smith",
      "username": "JohnSmith",
      "email": "john.smith@gmail.com",
      "password": "secret password"
    }
    ```

* Successful Response
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "id": 1,
      "first_name": "John",
      "last_name": "Smith",
      "username": "JohnSmith",
      "email": "john.smith@gmail.com",
      "token": ""
    }
    ```

* Error response: User already exists with the specified email
  * Status Code: 403
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "User already exists",
      "status_code": 403,
      "errors": {
        "email": "User with that email already exists"
      }
    }
    ```

* Error response: User already exists with the specified username
  * Status Code: 403
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "User already exists",
      "status_code": 403,
      "errors": {
        "username": "User with that username already exists"
      }
    }
    ```

* Error response: Body validation errors
  * Status Code: 400
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Validation error",
      "status_code": 400,
      "errors": {
        "email": "Invalid email",
        "username": "Username is required",
        "first_name": "First Name is required",
        "last_name": "Last Name is required"
      }
    }
    ```
## FEATURE 0: USER AUTHORIZATION

## Get all Businesses

Returns all the businesses

Return businesses (with optional filter by query parameters).

* Require Authentication: false
* Request
  * Method: GET
  * URL: /api/businesses
  * Query Parameters
    * page: integer, minimum: 1, maximum: 10, default: 1
    * size: integer, minimum: 1, maximum: 20, default: 20
    * business_name: string, optional
    * business_tags: string, optional
  * Body: none

* Successful Response
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "businesses":[
        {
          "id": 1,
          "business_name": "Some Place",
          "email":"business@app.io",
          "phone":"123-456-8910",
          "street_address": "123 Street Ave",
          "city":"Springfield",
          "zipcode":98765,
          "state":"CA",
          "country":"United States of America",
          "about":"Some descriptive sentence",
          "longitude":130,
          "latitude":90,
          "price_range":,
          "owner_id": 1,
          "created_at":"some date string",
          "updated_at":"some other date string",
        }
      ],
      "page": 1,
      "size": 15
    }
    ```
    
## Businesses owned by Current User

Returns all Businesses owned by the current user.

* Require Authentication: True
* Request
  * Method: GET
  * URL: /api/businesses/current
  * Body: none
 * Successful Response
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body: 
  ```json
  {
      "businesses":[
        {
          "id": 1,
          "business_name": "Some Place",
          "email":"business@app.io",
          "phone":"123-456-8910",
          "street_address": "123 Street Ave",
          "city":"Springfield",
          "zipcode":98765,
          "state":"CA",
          "country":"United States of America",
          "about":"Some descriptive sentence",
          "longitude":130,
          "latitude":90,
          "price_range":,
          "owner_id": 1,
          "created_at":"some date string",
          "updated_at":"some other date string",
        }
      ]
    }
  ```
  
  ## Get details of a Business from an Id
  
  Returns details of a business specified by its id
  
   * Require Authentication: false
   * Request
     * Method: GET
     * URL: /api/businesses/:business_id
   * Successful Response
     * Status Code: 200
     * Headers:
       * Content-Type: application/json 
     * Body:
```json
{
          "id": 1,
          "business_name": "Some Place",
          "email":"business@app.io",
          "phone":"123-456-8910",
          "street_address": "123 Street Ave",
          "city":"Springfield",
          "zipcode":98765,
          "state":"CA",
          "country":"United States of America",
          "about":"Some descriptive sentence",
          "longitude":130,
          "latitude":90,
          "price_range":,
          "owner_id": 1,
          "created_at":"some date string",
          "updated_at":"some other date string",
          "Owner": {
            "id":1,
            "first_name":"Gare",
            "last_name":"Bear",
          },
          "Images" : [
            {
               "id":3,
               "business_id":1,
               "url":"image.url"
            }
          ],
          "Reviews": [
            {
              "id":1,
              "business_id":1,
              "user_id":1,
              "rating":4,
              "review":"Yummy! I'd take my wife here again!",
              "created_at":"some date",
              "updated_at":"some date"
            }
          ],
          "Tags": {
              "tag":"some tags as string here"
          }
          
          
}
```
* Error response: Couldn't find a Business with the specified id

  * Status Code: 404
  * Headers:
    * Content-Type: application/json
  * Body: 
  ```json
  {
    "message":"Sorry, this business doesn't exist",
    "status_code":404
  }
  ```
  ## Create a Business
  
  Create and return a business
  
  * Require Authentication: true
  * Request
    * Method:POST
    * URL:/api/business
    * Headers:
      * Content-Type: application/json
    * Body:
```json
{
}
```
   ## Edit Business
   
   Edit and return an existing business
   
   * Require Authentication: true
   * Request
      * Method:PUT
      * URL:/api/business/:business_id
      * Headers:
         * Content-Type: application/json
      * Body:
```json
{
}
```
  ## Delete a Business
  
  Delete an existing Business
  
   * Require Authentication: true
   * Request
      * Method:DELETE
      * URL:/api/business/:business_id
      * Headers:
         * Content-Type: application/json
      * Body:
```json
{
}
```


