# API specs

Login
-----   

#### Login & Register: `POST /login/`

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

#### Report Diagnosis: `POST /reports/`
#### Auth Required: Yes
#### Body Example:
```
{
   "device_id": "xxxxxx"
   "ha_token": "xxxxxx",
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

#### Upload BLE Encounters: `POST /encounters/`
#### Auth Required: Yes
#### Body Example:
```
{
   "device_id": "xxxxxx",
   “encountered_list”: [
     {
       “encountered_id”: “xxxxxx”,
       “rssi”: -70,
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

#### Upload Location History: `POST /traces/`
#### Auth Required: Yes
#### Body Example:
```
{
   “device_id”: “xxxxxx”,
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

Broadcast (Deliver by Health Authorities)
------------------------------------------------------------

#### Confirmed Reports to Broadcast: `POST /reports/broadcast`
#### Auth Required: Yes
#### Body Example:
```
{
   "device_id": "xxxxxx"
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

Local Look-up
-------------

#### Get Confirmed Reporting: `GET /reports/broadcast`
#### Auth Required: Yes
#### Body Example:
```
{
  "device_id": "xxxxxx"
}
```
#### Success Response:
#### Code: `200 OK`
##### Match Found:
```
 {
   “found_diagnosed”: true,
   “device”: [
      { 
        “device_id”: "xxxxxx",
        "rssi": -70,
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