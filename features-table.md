# Features Table

Tables categorized by features / parts of functionality.

Main criteria of this analysis for each feature:

- Privacy
- Accuracy of risk analysis
- Amount of overall traffic
- Ability to collect and analyze data

### Geolocation Data Stored Locally

<table>
  <tr>
   <td><strong>Approach</strong>
   </td>
   <td><strong>Details</strong>
   </td>
   <td><strong>Pros</strong>
   </td>
   <td><strong>Cons</strong>
   </td>
   <td><strong>Actual Privacy</strong>
   </td>
   <td><strong>User Perceived Privacy</strong>
   </td>
  </tr>
  <tr>
   <td><strong>Detailed and accurate</strong>
   </td>
   <td>
   </td>
   <td>Data can be shared later via any possible way with any precision.
   </td>
   <td>
   </td>
   <td>High
   </td>
   <td>Moderate<sup>*</sup>
   </td>
  </tr>
  <tr>
   <td><strong>Large areas only</strong>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Doesn’t give much value to reduce precision if data is stored only locally.

   Precision is lost - in case we need accurate data at some point, it won’t be available.
   </td>
   <td>High
   </td>
   <td>Moderate<sup>*</sup>
   </td>
  </tr>
</table>

<sup>*</sup> In case data is stored only locally and we let users know that we don’t upload it to server.

### Geolocation Data Stored on Servers

<table>
  <tr>
   <td><strong>Approach</strong>
   </td>
   <td><strong>Details</strong>
   </td>
   <td><strong>Pros</strong>
   </td>
   <td><strong>Cons</strong>
   </td>
   <td><strong>Actual Privacy</strong>
   </td>
   <td><strong>User Perceived Privacy</strong>
   </td>
  </tr>
  <tr>
   <td><strong>All locations of all users</strong>
   </td>
   <td>
   </td>
   <td>Allows very precise filtering and analytics.

Minimizes notifications sent to people at risk.
   </td>
   <td>Centralized storage of all locations of all users poses serious privacy and security risks.
   </td>
   <td>Low
   </td>
   <td>Low
   </td>
  </tr>
  <tr>
   <td><strong>Large areas only</strong>
   </td>
   <td>Geohashes with reduced precision
   </td>
   <td>Allows some level of filtering when notifying users at risk.
   </td>
   <td>Some security and privacy risks, less precision when notifying users at risk.
   </td>
   <td>Moderate
   </td>
   <td>Low
   </td>
  </tr>
  <tr>
   <td><strong>No location</strong>
   </td>
   <td>Store only locally on devices
   </td>
   <td>No privacy or security concerns.
   </td>
   <td>Either broadcasting from server or periodic polling from mobile apps required to notify users at risk.
   </td>
   <td>High
   </td>
   <td>Moderate<sup>*</sup>
   </td>
  </tr>
</table>

<sup>*</sup> Assuming that we let users know that their location data is not shared with us.

### Bluetooth Encounters Data Stored on Servers

<table>
  <tr>
   <td><strong>Approach</strong>
   </td>
   <td><strong>Details</strong>
   </td>
   <td><strong>Pros</strong>
   </td>
   <td><strong>Cons</strong>
   </td>
   <td><strong>Actual Privacy</strong>
   </td>
   <td><strong>User Perceived Privacy</strong>
   </td>
  </tr>
  <tr>
   <td><strong>All encounters from of all users</strong>
   </td>
   <td>Maybe plain UUIDs
   </td>
   <td>Allows very precise filtering and analytics.

Minimizes notifications sent to people at risk.
   </td>
   <td>
   </td>
   <td>Moderate<sup>*</sup>
   </td>
   <td>Low
   </td>
  </tr>
  <tr>
   <td><strong>Only ids of confirmed cases</strong>
   </td>
   <td>Maybe plain UUIDs or public keys
   </td>
   <td>Risk data may be reused / resent to newly onboarded users.

Some analytics may be done (e.g. when confirmed, when recovered).
   </td>
   <td>Broadcasting or server polling may be required for notifying users (if no geolocation is available on servers)
   </td>
   <td>Moderate
   </td>
   <td>Low
   </td>
  </tr>
  <tr>
   <td><strong>Nothing</strong>
   </td>
   <td>Encounters stored only locally
   </td>
   <td>
   </td>
   <td>Broadcasting or server polling may be required for notifying users (if no geolocation is available on servers).

No analytics or look-back functionality available.
   </td>
   <td>High
   </td>
   <td>High<sup>**</sup>
   </td>
  </tr>
</table>

<sup>*</sup> Only if the IDs are anonymized (without any link to phone, email etc.)

<sup>**</sup> In case we make clear to users that they fully control the data to be shared

### Data Uploaded in Reports

<table>
  <tr>
   <td><strong>Approach</strong>
   </td>
   <td><strong>Details</strong>
   </td>
   <td><strong>Pros</strong>
   </td>
   <td><strong>Cons</strong>
   </td>
   <td><strong>Actual Privacy</strong>
   </td>
   <td><strong>User Perceived Privacy</strong>
   </td>
  </tr>
  <tr>
   <td><strong>All data</strong>
   </td>
   <td>All BLE encounters for infected person, their UUID/key and all location history
   </td>
   <td>Precise notifications (if we can match UUIDs/keys or geohashes to devices).
   </td>
   <td>
   </td>
   <td>Moderate<sup>*</sup>
   </td>
   <td>Low
   </td>
  </tr>
  <tr>
   <td><strong>Only location history</strong>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Cannot notify specific users, less accuracy in risk assessment.
   </td>
   <td>Moderate<sup>*</sup>
   </td>
   <td>Moderate<sup>*</sup>
   </td>
  </tr>
  <tr>
   <td><strong>Only BLE encounters</strong>
   </td>
   <td>
   </td>
   <td>Ability to notify only people at risk and high accuracy of risk assessment.
   </td>
   <td>May require broadcasting if no data is stored on server.
   </td>
   <td>Moderate<sup>*</sup>
   </td>
   <td>Moderate<sup>*</sup>
   </td>
  </tr>
</table>

<sup>*</sup> Only if we don’t store uploaded data and let users know about that

### Other Data Stored on Servers

<table>
  <tr>
   <td><strong>Approach</strong>
   </td>
   <td><strong>Details</strong>
   </td>
   <td><strong>Pros</strong>
   </td>
   <td><strong>Cons</strong>
   </td>
   <td><strong>Actual Privacy</strong>
   </td>
   <td><strong>User Perceived Privacy</strong>
   </td>
  </tr>
  <tr>
   <td><strong>Phone numbers</strong>
   </td>
   <td>
   </td>
   <td>Ability to contact people by phone.

Guarantee that person is real and has Canadian number.
   </td>
   <td> Security and privacy risks.
   </td>
   <td>Low
   </td>
   <td>Low
   </td>
  </tr>
  <tr>
   <td><strong>Emails</strong>
   </td>
   <td>
   </td>
   <td>Less privacy risk than phone numbers, still allowing some level of verifying identity.
   </td>
   <td>Some security and privacy risks.
   </td>
   <td>Moderate
   </td>
   <td>Moderate
   </td>
  </tr>
  <tr>
   <td><strong>Only device IDs</strong>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>No way to verify person identity. (can be mitigated by verifying infection reports through HA)
   </td>
   <td>High
   </td>
   <td>Moderate
   </td>
  </tr>
</table>

### Notifying Users at Risk

<table>
  <tr>
   <td><strong>Approach</strong>
   </td>
   <td><strong>Notes</strong>
   </td>
   <td><strong>Pros</strong>
   </td>
   <td><strong>Cons</strong>
   </td>
  </tr>
  <tr>
   <td><strong>Broadcasting to everyone</strong>
   </td>
   <td>
   </td>
   <td>No need to store any ids/locations on servers.
   </td>
   <td>Very high traffic volume with 99% data ignored.

(Can be optimized by bundling and sending reports every X hours.)
   </td>
  </tr>
  <tr>
   <td><strong>Broadcasting by geohash</strong>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Need to store geohash (area) of each user.
   </td>
  </tr>
  <tr>
   <td><strong>Precise notification by BLE UUID/key</strong>
   </td>
   <td>
   </td>
   <td>Only specific users at risk get notified
   </td>
   <td>Need to store BLE UUID/key for each user.
   </td>
  </tr>
  <tr>
   <td><strong>Polling server</strong>
   </td>
   <td>Fetch list of geohashes or BLE UUIDs/keys periodically every X hours
   </td>
   <td>No need to precisely send notifications or broadcast them.
   </td>
   <td>Active cases (ids/geohashes) need to be stored on servers for a while.

Downloading list may be problematic if number of active cases is high.

App needs to be woken up periodically to poll from server.
   </td>
  </tr>
</table>

### Report Verification

HA - health authority

<table>
  <tr>
   <td><strong>Approach</strong>
   </td>
   <td><strong>Notes</strong>
   </td>
   <td><strong>Pros</strong>
   </td>
   <td><strong>Cons</strong>
   </td>
  </tr>
  <tr>
   <td><strong>Send report only with token from HA</strong>
   </td>
   <td>
   </td>
   <td>Easy for HA where they cannot use our apps for any reasons (codes/tokens can be send in email/ on paper)
   </td>
   <td>Need to generate and distribute tokens somehow and make sure they are secure.
   </td>
  </tr>
  <tr>
   <td><strong>Let HA send report using 2d code</strong>
   </td>
   <td>
   </td>
   <td>Easy for HA and user when they can access mobile apps or servers (get authorized)
   </td>
   <td>Need to establish mechanism of authorizing HA representatives on our servers.
   </td>
  </tr>
  <tr>
   <td><strong>No verification</strong>
   </td>
   <td>
   </td>
   <td>No effort needed to interact with HA and authorize reports.
   </td>
   <td>No guarantee that report isn’t false.
   </td>
  </tr>
</table>

### BLE Message Generation and Exchange

<table>
  <tr>
   <td><strong>Approach</strong>
   </td>
   <td><strong>Notes</strong>
   </td>
   <td><strong>Pros</strong>
   </td>
   <td><strong>Cons</strong>
   </td>
  </tr>
  <tr>
   <td><strong>Generate just UUID on device</strong>
   </td>
   <td>UUID can be constant per device or change every day (then history needs to be kept).
   </td>
   <td>Easy to generate and share.
   </td>
   <td>If UUIDs are stored on the server, we can map each UUID to device ID which has moderate privacy concerns.

Including any additional info about the encounter (when, where it happened) poses risks when data is broadcasted (without storing on server) because all devices will get it.

UUID is plain and doesn’t provide any additional info.
   </td>
  </tr>
  <tr>
   <td><strong>Generate public and private keys on device</strong>
   </td>
   <td>Public key is shared to all encounters
   </td>
   <td>Device of infected person can encrypt additional info about the encounter (e.g. when and where it happened) without sharing it with all devices, so only target device can decrypt the message.
   </td>
   <td>No analysis can be done even if data is stored on server because it can be decrypted only by target device (of person at risk).
   </td>
  </tr>
  <tr>
   <td><strong>Server-generated public and private keys</strong>
   </td>
   <td>Unique key is provided by server to each device and only server can decrypt the message when report is submitted.
   </td>
   <td>We can send push notifications directly to target users if we store user IDs &lt;-> device IDs on server and encrypt them with public key when exchanging with peers.
   </td>
   <td>Requires refreshing public keys from server periodically.

Requires storage of key pairs on server.

Requires server to decrypt the message and have device IDs mapped to user IDs to send notifications to target users => moderate privacy concerns.
   </td>
  </tr>
</table>
