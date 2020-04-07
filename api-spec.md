# API specs

Registration
------------
- Go to the following 2 routes if building profile using phone number.

`POST /register/get_pin/`
#### Auth Required: No
#### Body Example:
```
{ 
  “phone_number”: “+12222222222” 
}
```
#### Success Response:
#### Code: `200 OK`
```
{
   “message”: “Sms with temporary pin sent to phone.” 
}
```
#### Error Response:
#### Code: `400 BAD REQUEST`
```
{ 
  "error": "Invalid request."
}
```

`POST /register/`

#### Auth Required: No
#### Body Example:
```
 {
   “phone_number”: “+12222222222”,
   “temporary_pin”: “xxxxxx”,
   “device_id”: “xxxxxx”
 }
```
#### Success Response:
#### Code: `201 CREATED`
```
 {
   “valid”: true,
   “token”: “xxxxxx”
 }
```
#### Error Response:
#### Code: `400 BAD REQUEST`
```
 {
   “valid”: false,
   “error”: “No pin entered, or temporary pin did not match.”
 }

```

Login
-----
- Go to this route for login (and registration as well if not building profile with phone number).   

`POST /login/`
#### Auth Required: No
#### Body Example:
```
{ 
  “device_id”: “xxxxxx” 
}
```
#### Success Response:
#### Code: `200 OK`
```
 {
   “token”: “xxxxxx”
 }
```
#### Error Response:
#### Code: `400 BAD REQUEST`
```
 {
   “error”: “Invalid credentials.”
 }
```

Reporting
---------
`POST /reports/`
#### Auth Required: Yes
#### Body Example:
```
{
   "pre_auth_token": "xxxxxx",
   “info_questions”: {
        “question_1”: “answer_1”,
        “question_2”: “answer_2”,
        ...
     },
   “status”: "confirmed",
   “reported_at”: “timestamp”

}
```
#### Success Response:
#### Code: `201 CREATED`
```
 {
   "message": "Successfully created."
 }
```
#### Error Response:
#### Code: `400 BAD REQUEST`
```
 {
   “error”: “Missing fields.”
 }
```

`POST /encounters/`
#### Auth Required: Yes
#### Body Example:
```
{
   "user_id": "xxxxxx",
   “encountered_list”: [
     {
       “encountered_id”: “xxxxxx”,
       “rssi”: (bluetooth signal intensity)
       “encountered_at”: “timestamp”
      }
    ]
}
```
#### Success Response:
#### Code: `201 CREATED`
```
 {
   "message": "Successfully uploaded."
 }
```
#### Error Response:
#### Code: `400 BAD REQUEST`
```
 {
   “error”: “Missing fields.”
 }
```

`POST /traces/`
#### Auth Required: Yes
#### Body Example:
```
{
   “user_id”: “xxxxxx”,
   “trace”: [
     { geo-Json }
    ]
}
```
#### Success Response:
#### Code: `201 CREATED`
```
 {
   "message": "Successfully uploaded."
 }
```
#### Error Response:
#### Code: `400 BAD REQUEST`
```
 {
   “error”: “Missing fields.”
 }
```

Local Look-up
-------------
`GET /reports/`
#### Auth Required: Yes
#### Body Example:
```
{
  "user_id": "xxxxxx"
}
```
#### Success Response:
#### Code: `200 OK`
##### Match Found:
```
 {
   “found_diagnosed”: true,
   “diagnosed_device_id”: [
      { 
        “device_id”: "xxxxxx",
        “encountered_at”: "timestamp"
      }
   ],
   "location": [
      { geo-Json }
   ]
 }
```
##### No Match Found:
```
{
  "found_diagnosed": false
}
```
#### Error Response:
#### Code: `400 BAD REQUEST`
```
 {
   “error”: “Invalid Request.”
 }
```