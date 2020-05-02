# Features Table

Tables categorized by features / parts of functionality.

Main criteria of this analysis for each feature:

- Privacy
- Accuracy of risk analysis
- Amount of overall traffic
- Ability to collect and analyze data


### Geolocation Data Stored Locally

|Approach|Details|Pros|Cons|Actual Privacy|User Perceived Privacy|
|--- |--- |--- |--- |--- |--- |
|**Detailed and accurate<br/>(recommended)**||Data can be shared later via any possible way with any precision.||High|Moderate\*|
|Large areas only|||Doesn't give much value to reduce precision if data is stored only locally.<br/>Precision is lost - in case we need accurate data at some point, it won't be available.|High|Moderate\*|

\* In case data is stored only locally and we let users know that we don’t upload it to server.


### Geolocation Data Stored on Servers

|Approach|Details|Pros|Cons|Actual Privacy|User Perceived Privacy|
|--- |--- |--- |--- |--- |--- |
|All locations of all users||Allows very precise filtering and analytics.<br/>Minimizes notifications sent to people at risk.|Centralized storage of all locations of all users poses serious privacy and security risks.|Low|Low|
|**Large areas only<br/>(recommended)**|Geohashes with reduced precision|Allows some level of filtering when notifying users at risk.|Some security and privacy risks.<br/>Less precision when notifying users at risk.|Moderate|Low|
|No location|Store only locally on devices|No privacy or security concerns.|Either broadcasting from server or periodic polling from mobile apps required to notify users at risk.|High|Moderate*|

\* Assuming that we let users know that their location data is not shared with us.


### Bluetooth Encounters Data Stored on Servers

|Approach|Details|Pros|Cons|Actual Privacy|User Perceived Privacy|
|--- |--- |--- |--- |--- |--- |
|All encounters from of all users|Can be plain UUIDs|Allows very precise filtering and analytics.<br/>Minimizes notifications sent to people at risk.||Moderate\*|Low|
|**Only ids of confirmed cases<br/>(recommended)**|Maybe plain UUIDs or public keys|Risk data may be reused / resent to newly onboarded users.<br/>Some analytics may be done (e.g. when confirmed, when recovered).|Broadcasting or server polling may be required for notifying users (if no geolocation is available on servers)|Moderate|Low|
|Nothing|Encounters stored only locally||Broadcasting or server polling may be required for notifying users (if no geolocation is available on servers).<br/>No analytics or look-back functionality available.|High|High\*\*|

\* Only if the IDs are anonymized (without any link to phone, email etc.)

\*\* In case we make clear to users that they fully control the data to be shared


### Data Uploaded in Reports


|Approach|Details|Pros|Cons|Actual Privacy|User Perceived Privacy|
|--- |--- |--- |--- |--- |--- |
|**All data<br/>(recommended)**|All BLE encounters for infected person, their UUID/key and all location history|Precise notifications (if we can match UUIDs/keys or geohashes to devices).||Moderate\*|Low|
|Only location history|||Cannot notify specific users.<br/>Less accuracy in risk assessment.|Moderate\*|Moderate\*|
|Only BLE encounters||Ability to notify only people at risk and high accuracy of risk assessment.|May require broadcasting if no data is stored on server.|Moderate\*|Moderate\*|

\* Only if we don’t store uploaded data and let users know about that


### Other Data Stored on Servers


|Approach|Details|Pros|Cons|Actual Privacy|User Perceived Privacy|
|--- |--- |--- |--- |--- |--- |
|Phone numbers||Ability to contact people by phone.<br/>Guarantee that person is real and has Canadian number.|Security and privacy risks.|Low|Low|
|Emails||Less privacy risk than phone numbers, still allowing some level of verifying identity.|Some security and privacy risks.|Moderate|Moderate|
|**Only device IDs<br/>(recommended)**|||No way to verify person identity. (can be mitigated by verifying infection reports through HA)|High|Moderate|



### Notifying Users at Risk


|Approach|Details|Pros|Cons|
|--- |--- |--- |--- |
|Broadcasting to everyone||No need to store any ids/locations on servers.|Very high traffic volume with 99% data ignored.<br/>(Can be optimized by bundling and sending reports every X hours.)|
|**Broadcasting by geohash<br/>(recommended)**|||Need to store geohash (area) of each user.|
|**Precise notification by BLE UUID/key<br/>(recommended)**||Only specific users at risk get notified|Need to store BLE UUID/key for each user.|
|Polling server|Fetch list of geohashes or BLE UUIDs/keys periodically every X hours|No need to precisely send notifications or broadcast them.|Active cases (ids/geohashes) need to be stored on servers for a while.<br/>Downloading list may be problematic if number of active cases is high.<br/>App needs to be woken up periodically to poll from server.|



### Report Verification

HA - health authority

|Approach|Details|Pros|Cons|
|--- |--- |--- |--- |
|**Send report only with token from HA<br/>(recommended)**|HA would get unique tokens from our servers|Easy for HA where they cannot use our apps for any reasons (codes/tokens can be send in email/ on paper)|Need to generate and distribute tokens somehow and make sure they are secure.|
|**Let HA send report using QR code<br/>(recommended)**|HA will use our mobile app or website where they need to be authorized|Easy for HA and user when they can access mobile apps or servers (get authorized)|Need to establish mechanism of authorizing HA representatives on our servers.|
|*No verification<br/>(supported)*|In this case we can handle such reports in different way (for analytics, "mild" notifications etc.)|No effort needed to interact with HA and authorize reports.|No guarantee that report isn’t false.|



### BLE Message Generation and Exchange


|Approach|Details|Pros|Cons|
|--- |--- |--- |--- |
|Generate only UUID or hash on device|UUID can be constant per device or change every day (then history needs to be kept).<br/>To enable direct notifications for users at risk some data needs to be stored on the server (either UUIDs of all users or UUIDs of infected users).|Easy to generate and share.|If UUIDs are stored on the server, we can map each UUID to device ID which has moderate privacy concerns.<br/>Including any additional info about the encounter (when, where it happened) poses risks when data is broadcasted (without storing on server) because all devices will get it.<br/>UUID is plain and doesn’t provide any additional info.<br/>No analysis or limited analysis can be done (depending on what data stored on servers).|
|Generate public and private keys on device|Public key is shared to all encounters|Device of infected person can encrypt additional info about the encounter (e.g. when and where it happened) without sharing it with all devices, so only target device can decrypt the message.|No analysis can be done even if data is stored on server because it can be decrypted only by target device (of person at risk).|
|**Server-generated public and private keys<br/>(recommended)**|Unique key is provided by server to each device and only server can decrypt the message when report is submitted.|We can send push notifications directly to target users if we store user IDs &lt;-> device IDs on server and encrypt them with public key when exchanging with peers.|Requires refreshing public keys from server periodically.<br/>Requires storage of key pairs on server.<br/>Requires server to decrypt the message and have device IDs mapped to user IDs to send notifications to target users => moderate privacy concerns.|
