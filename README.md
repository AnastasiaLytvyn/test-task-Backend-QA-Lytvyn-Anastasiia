# Test Cases for POST Request

## Test Case 1: Creating a new pet using valid data
| Field            | Description                        |
|------------------|------------------------------------|
| **Test Case ID** | TC_001                             |
| **Summary**      | Creating a new pet using valid data|
| **Priority**     | High                             |
| **Estimate**     | 5 minutes                          |
| **Preconditions**| -                                  |

### Steps
##### Step 1. 
Send `POST` request using Postman on endpoint /pet, using valid data for all fields.<br />
For example, using the following request body
```json
{
  "id": "{{$randomInt}}",
  "category": {
    "id": "{{$randomInt}}",
    "name": "{{$randomLoremWord}}"
  },
  "name": "{{$randomFirstName}}",
  "photoUrls": [
    "{{$randomAnimalsImage}}"
  ],
  "tags": [
    {
      "id": "{{$randomInt}}",
      "name": "{{$randomAbbreviation}}"
    }
  ],
  "status": "available"
}
```
##### Expected result 1.
Status code: **200 OK** <br />
Pet is created
```json
{
  "id": 5,
  "category": {
    "id": 695,
    "name": "eum"
  },
  "name": "Jerad",
  "photoUrls": [
    "http://placeimg.com/640/480/animals"
  ],
  "tags": [
    {
      "id": 34,
      "name": "HTTP"
    }
  ],
  "status": "available"
}
```
---

## Test Case 2: Validation of missing required parameters
| Field            | Description                              |
|------------------|------------------------------------------| 
| **Test Case ID** | TC_002                                   |
| **Summary**      | Send request missing required parameters |
| **Priority**     | High                                     |
| **Estimate**     | 10 minutes                               |
| **Preconditions**| -                                        |

### Steps
##### Step 1.
Send `POST` request using Postman on endpoint /pet, without "name" parameter in body <br />
For example, using the following request body
```json
{
  "id": "{{$randomInt}}",
  "category": {
    "id": "{{$randomInt}}",
    "name": "{{$randomLoremWord}}"
  },
  "photoUrls": [
    "{{$randomAnimalsImage}}"
  ],
  "tags": [
    {
      "id": "{{$randomInt}}",
      "name": "{{$randomAbbreviation}}"
    }
  ],
  "status": "available"
}
```
##### Expected result 1.
Status code: **400 Bad Request** <br />
Error message: `"Missing required fields: name"`.

##### Step 2.
Send `POST` request using Postman on endpoint /pet, without "photoUrls" parameter in body <br />
For example, using the following request body
```json
{
  "id": "{{$randomInt}}",
  "category": {
    "id": "{{$randomInt}}",
    "name": "{{$randomLoremWord}}"
  },
  "name": "{{$randomFirstName}}",
  "tags": [
    {
      "id": "{{$randomInt}}",
      "name": "{{$randomAbbreviation}}"
    }
  ],
  "status": "available"
}
```
##### Expected result 2.
Status code: **400 Bad Request** <br />
Error message: `"Missing required fields: photoUrls"`.
---

## Test Case 3: Validation of invalid data type for parameter "name" 
| Field            | Description                                         |
|------------------|-----------------------------------------------------|
| **Test Case ID** | TC_003                                              |
| **Summary**      | Send request with invalid data type for parameter "name" |
| **Priority**     | Medium                                              |
| **Estimate**     | 5 minutes                                           |
| **Preconditions**| -                                                   |
### Steps
##### Step 1.
Send `POST` request using Postman on endpoint /pet, send "name" as number <br />
For example, using the following request body
```json
{
  "id": "{{$randomInt}}",
  "category": {
    "id": "{{$randomInt}}",
    "name": "{{$randomLoremWord}}"
  },
  "name": 1.23,
  "photoUrls": [
    "{{$randomAnimalsImage}}"
  ],
  "tags": [
    {
      "id": "{{$randomInt}}",
      "name": "{{$randomAbbreviation}}"
    }
  ],
  "status": "available"
}
```
##### Expected result 1.
Status code: **400 Bad Request** <br />
Error message: `"Invalid data type for name: expected string"`.
---

## Test Case 4: Validation of 256 symbols length for parameter "name"
| Field            | Description                                        |
|------------------|----------------------------------------------------|
| **Test Case ID** | TC_004                                             |
| **Summary**      | Send request with 256 symbols for parameter "name" |
| **Priority**     | Medium                                             |
| **Estimate**     | 3 minutes                                          |
| **Preconditions**| -                                                  |
### Steps
##### Step 1.
Send `POST` request using Postman on endpoint /pet, parameter "name" containing 256 symbols, 
255 symbols must be the maximum allowed characters <br />
name = testtesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttest <br />
For example, using the following request body
```json
{
  "id": "{{$randomInt}}",
  "category": {
    "id": "{{$randomInt}}",
    "name": "{{$randomLoremWord}}"
  },
  "name": "testtesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttesttest",
  "photoUrls": [
    "{{$randomAnimalsImage}}"
  ],
  "tags": [
    {
      "id": "{{$randomInt}}",
      "name": "{{$randomAbbreviation}}"
    }
  ],
  "status": "available"
}
```
##### Expected result 1.
Status code: **400 Bad Request** <br />
Error message: `"Max size for field name equals 255 symbols"`.

---

## Test Case 5: Validate response time
| Field            | Description                                                  |
|------------------|--------------------------------------------------------------|
| **Test Case ID** | TC_005                                                       |
| **Summary**      | Validate that the response time is within acceptable limits. |
| **Priority**     | Low                                                          |
| **Estimate**     | 3 minutes                                                    |
| **Preconditions**| -                                                            |
### Steps
Send `POST` request using Postman on endpoint /pet, using valid data for all fields. <br />
For example, using the following request body
```json
{
  "id": "{{$randomInt}}",
  "category": {
    "id": "{{$randomInt}}",
    "name": "{{$randomLoremWord}}"
  },
  "name": "{{$randomFirstName}}",
  "photoUrls": [
    "{{$randomAnimalsImage}}"
  ],
  "tags": [
    {
      "id": "{{$randomInt}}",
      "name": "{{$randomAbbreviation}}"
    }
  ],
  "status": "available"
}
```
##### Expected result 1.
Status code: **200 OK** <br />
Response time is less than `1000ms`.
---

## Test Case 6: Send GET request for /pet endpoint
| Field            | Description                                                  |
|------------------|--------------------------------------------------------------|
| **Test Case ID** | TC_006                                                       |
| **Summary**      | Validate that GET request returns an error for /pet endpoint |
| **Priority**     | Low                                                          |
| **Estimate**     | 3 minutes                                                    |
| **Preconditions**| -                                                            |
### Steps
##### Step 1.
Send `GET` request using Postman on endpoint /pet, using valid data for all fields. <br />
For example, using the following request body
```json
{
  "id": "{{$randomInt}}",
  "category": {
    "id": "{{$randomInt}}",
    "name": "{{$randomLoremWord}}"
  },
  "name": "{{$randomFirstName}}",
  "photoUrls": [
    "{{$randomAnimalsImage}}"
  ],
  "tags": [
    {
      "id": "{{$randomInt}}",
      "name": "{{$randomAbbreviation}}"
    }
  ],
  "status": "available"
}
```
##### Expected result 1.
Status code: **405 Method Not Allowed** <br />
