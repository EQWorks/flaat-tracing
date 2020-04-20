# API specs

Login
-----   

#### Login & Register: `POST /login/`

#### Auth Required: No
#### Body Example:
```
{ 
  “device_id”: “string_token” 
}
```
#### Success Response:
#### Code: `200 OK`
```
 {
   “token”: “string_token”
 }
```
#### Error Response:
#### Code: `400 BAD REQUEST`
```
 {
   “message”: “Missing fields.”
 }
```

Reporting
---------

#### Report Diagnosis: `POST /tcnreport/`
#### Auth Required: Yes
#### Body Example:
```
{
  "validationPin": "string_token",
  "report": "c432bf9538f248a8238543a89d08e098c89bb890",
  "traces": [
    {
      "geohash": "string_hash",
      "start": timestamp,
      "end": timestamp
    }
  ]
}
```
#### Success Response:
#### Code: `201 CREATED`
```
 {
   "message": "Successful upload."
 }
```
#### Error Response:
#### Code: `400 BAD REQUEST`
```
 {
   “message”: “Missing fields.”
 }
```

Local Look-up
-------------

#### Get Confirmed Reporting: `GET /tcnreport/`
#### Auth Required: Yes
#### Query Params Example:
```
{
  "verified": boolean,
  "fromDate": timestamp,
}
```
#### Body Params Example:
```
{
  "locations": [
    {
      "geohash": "string_hash",
      "start": timestamp,
      "end": timestamp
    }
  ]
}
```
#### Success Response:
#### Code: `200 OK`

```
 {
   "reports": [
     {
       "id": 1,
       "report": "c432bf9538f248a8238543a89d08e098c89bb890",
       "traces": [
         {
           "geohash": "string_hash",
           "start_time": timestamp,
           "end_time": timestamp
         }
       ]
     }
   ]
 }
```

#### Error Response:
#### Code: `400 BAD REQUEST`
```
 {
   “message”: “Missing fields.”
 }
```