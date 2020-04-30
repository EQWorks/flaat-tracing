# API specs

Login
-----   

#### Login & Register: `POST /login/`

#### Auth Required: No
#### Body Example:
```
{ 
  “device_id”: “string_token”
  "app_name": “string_token”
  "access_key": “string_token”
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
#### Body Example (application/json) :
```
{
  "validationPin": "string_token",
  "report": "c432bf9538f248a8238543a89d08e098c89bb890",  // base64 TCN report
  "traces": [
    {
      "geohash": "string_hash",
      "start": timestamp,
      "end": timestamp
    }
  ]
}
```
#### Body Example (text/plain; charset=iso-8859-1) :
```
c432bf9538f248a8238543a89d08e098c89bb890  // base 64 TCN report
```
#### Success Response:
#### Code: `200 OK`
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
  "verified": boolean,        // exclude unverified reports
  "fromDate": number,         // unix time (in seconds)
  "toDate": number,           // unix time (in seconds)
  "fullReport": boolean,      // return report || signature
  "locations": Array<string>, // array of geohashes
  "intervalNumber": number.   // 6-hour time window since unix epoch (superseded by fromDate) 
}
```
#### Success Response:
#### Code: `200 OK`

```
 {
   "reports": [
     "c432bf9538f248a8238543a89d08e098c89bb890",  // base64 TCN report
     "Dv32bf9532dssdi938543a89d08e0yuec89bb8a0"
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
