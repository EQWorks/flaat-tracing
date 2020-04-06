# FLAAT Tracing


### Privacy-safe Decentralized Tracing with Informed Consent

EQ Works

First Published: April 6, 2020

There is an immediate need for health and government officials across the country to have access to high-quality contact tracing data, and a variety of different mechanisms that this data can be collected. Several trade-offs exist between accuracy and privacy and need to be analyzed to create an optimal solution between accurate, verifiable data and widespread consumer adoption to reach the critical mass required to inform policy changes during the COVID-19 crisis.

Below we are going to analyze the different mechanisms in which cellular technology can be used for reliable contact tracing while still keeping the public's privacy intact using the frameworks in place by the Office of the Privacy Commissioner in Canada, instilling the confidence required in users that their data can’t be used for anything other than minimizing the spread of COVID-19. The three main categories we will get into are: how to collect and store the data, how and when users should be informed when it is believed they may have come into contact with someone who is COVID-19 positive, and how it is possible to verify users are COVID-19 positive without collecting identity-based identifiers.


### How to Log and Store the Data

**Privacy-safe Identifier** - To remove all traceability back to an individual, we’re proposing the adoption of the CEN<sup>[8]</sup> identifier sequencing mechanism proposed by CoEpi<sup>[6]</sup>. This would be the only identifier that is either broadcasted or uploaded. This identifier will not be associated with any other identifiers in any identity-linked datapoint outside of the scope of the mobile application environment. It is possible to utilize identity linked identifiers (telephone numbers, MAIDs, etc.) within the mobile application environment provided these identifiers were acquired user consent. All validation against these identifiers must happen at the edge, locally within the mobile application scope using hashed or cryptological encrypted information broadcast. Under no circumstances must any Privacy-safe Identifier be broadcast, communicated or uploaded beyond the scope of the mobile application’s local scope and sandbox.

**On data logging** - There are two mechanisms in which data can be collected and transformed back into COVID-19 contact tracing: geolocation and bluetooth<sup>[4][6]</sup>. Geolocation would track the user when their cell phone is active and location sharing is turned on via permissions management, creating a map and timestamps of where they went. If the user happened to be in the same area around the same time as any of the verified COVID-19 positive devices were, they could then be notified that they may be at risk<sup>[1]</sup>. This has major privacy implications. For the data to be useful, the location history would need to be as precise as possible. This would make it relatively easy to determine a user's home address, and remove the ability for the data to be truly anonymized. Geolocation can be stripped back to large areas only for more privacy, but that would come at the cost of the accuracy of the data provided back to health officials, and users in any relatively high population density area would be bombarded with risk notifications to the point of them getting ignored. Bluetooth on the other hand, would not require specific geolocation data to function, only an anonymized unique identifier created on the device. The Bluetooth mechanism would search the immediate area for other Bluetooth signals, and upon finding them would create a “handshake” between the two devices that verifies these two devices were in the same area at the same time. In this methodology, you don’t need the precise location of the device at any given time, as it creates a relationship table of all of the anonymized identifiers within the devices that have come into contact with each other. The geolocation log can be further scrubbed of the home/residential location of the user using a heuristic driven approach locally on the mobile device, detect the most likely location and scrub it from the data before any upload. This allows health and government officials to accurately determine how many devices any given device has come into contact with, notify the users if they have been in contact with a device that has been verified as COVID-19 positive, and does not reveal sensitive detailed location data that could trace back the identity of the user.

**Fastest path to mass adoption** - We believe the best possible chance of mass adoption depends on packaging the discovery, data logging, and secure-report validation into a mobile software library. The library will implement both geolocation tagging as well as Bluetooth handshake logs, allowing the applications to implement the protocol to manage various variables that govern the tracing behavior. This flexibility would allow easy adoption by various parties that are trying to satisfy ground realities and public health challenges unique to each region. Using a single software library would enable a lot of individual apps with a big existing user base to incorporate this package and release a new binary. This would avoid the adoption curve that otherwise would hold most solutions back. Simultaneously, this also solves the problem of saturation occurring between two or more competing applications whether by alternate strategies or geographically-centric independent solutions overlapping due to human movement patterns within a country. There is also a significant advantage especially in at least one such library implementing mobile application to be in the foreground or recently have been in the foreground, to be highly likely. There is also considerable technical evidence that one foreground application on a mobile device that activates a sensor also benefits other background applications that depend on that sensory input. This would allow an “official” COVID-19 tracing app to piggyback on top of support apps that implement the common-library and trigger the same sensors in a predictable synchronized pattern.

**On data storing** - There are also two mechanisms in which to store the data: centralized servers or locally. Whether using geolocation or Bluetooth, transmitting and storing the data in a centralized manner would allow for health officials to get an accurate view at any given time of either where all devices are or have been, mapping all of those users back to infected devices using geolocation, or up to date relationship tables on which devices have come into contact with a COVID-19 positive device<sup>[3]</sup>. There is a trade-off in privacy for this mass dataset, as it would be on all devices, all the time, regardless of if a user has or will ever come into contact with a COVID-19 positive device. Storing the data locally (on a users device, unretrievable without the explicit consent of the user) would limit authorities access, and when a user has tested positive for COVID-19, they can then make the conscious decision that their data is critical in tracking the spread of COVID-19 and elect to report it and share their data back in a centralized manner. The data stored locally would be deleted as its epidemiological value diminishes over time. Therefore we’ve proposed making available multiple mechanisms for a user to contribute with consent to their logged epidemiologically valuable data for the explicit purpose of contact tracing once a confirmed positive diagnosis has been achieved.


### How, when and at what frequency to inform users of cases spreading near them

Broadcasting possible contact with users is vital in stopping the spread early. This needs to be done accurately, as bombarding users with notifications with false-positive warnings will lead to all of the notifications being ignored. The trade-off on user notification isn’t as much between privacy and accuracy (although there are some implications), but around how as the frequency in user notifications increases, the impact that that notification has on the user will diminish. In an ideal state, a user would only be notified if they have an immediate health risk to maximize the impact it has on that user. There are a few notification systems that could be implemented. You could either notify everyone of new cases and the general area using geohash protocol<sup>[7]</sup> to abstract precise locations, which would require no real accurate information but will be irrelevant the vast majority of the time, notify users who were only in an epidemiologically relevant geohash<sup>[7]</sup> of precise geolocation at the same time as a COVID-19 positive device or only notify users devices who have had a direct Bluetooth “handshake” with the positive device<sup>[5]</sup>  using the Privacy-safe Identifier to communicate positive diagnosed individual. The further we go along in this list, the fewer users receive notifications and the more accurate they become. The goal is to only notify the user if they have an immediate health risk, prompting them to either self-isolate to flatten the curve or to seek medical attention, so either precise geolocation notification (accepting the privacy compromise) or Bluetooth “handshake” contact reporting is optimal to prompt the user into immediate action, as over notifying individuals would render the notifications ineffective.

**Verifying Reports** - Verification of COVID-19 positive devices is crucial to not spoil the data set entirely. False verifications would ping the users with false notifications, and as discussed above would then render all notifications ineffective in prompting users to either self-isolate or seek medical attention. There are two mechanisms in which a device can be officially verified. The first is using the SDK of the app as an ID in the form of a 2D barcode, in which the health official can scan that with a simpler app to log and verify it as a COVID-19 positive device. The device will then ping the device owner, who can then elect to share back their data and notify users they may have come into contact with. In areas where the infrastructure is not in place for this option to be technologically feasible, the health official will have a series of pre-generated one-time use alphanumeric tokens<sup>[2]</sup> they can provide to the COVID-19 positive device owner, who can then input that token into their device and select whether or not to share their data to notify other devices they may have come into contact with.

### Conclusion

Given the trade-offs between privacy and accuracy listed above, the most accurate mechanism for contact tracing COVID-19 is storing Bluetooth handshakes locally, verifying COVID-19 positive devices through a token generated by health officials, and then the user gives explicit consent to transmit their data back to notify anyone that they have come in contact with. This minimized data collected only to what is needed to properly contact trace requires user consent and only notifies people of an immediate health risk, which will have a higher chance of prompting them to either self-isolate or seek medical attention.

### References

[1]    Ramesh Raskar, MIT (March 19, 2020) _Apps Gone Rogue: Maintaining Personal Privacy in an Epidemic_ \
[https://arxiv.org/pdf/2003.08567.pdf](https://arxiv.org/pdf/2003.08567.pdf)


[2]    Singapore Government Digital Services (April 1, 2020) _Trace together, safer together_ \
[https://www.tracetogether.gov.sg/](https://www.tracetogether.gov.sg/)


[3]    Dilshan Kathriarachchi & Global News (April 2, 2020) _Should Canada use our cell phones to slow the spread of COVID-19?_ \
[https://omny.fm/shows/wait-theres-more/should-canada-use-our-cell-phones-to-slow-the-spre](https://omny.fm/shows/wait-theres-more/should-canada-use-our-cell-phones-to-slow-the-spre)


[4]    WeTrace & Andreas Gassmann (March 30, 2020) _Privacy-Preserving Bluetooth Covid-19 Contract Tracing_ \
[https://wetrace.ch/](https://wetrace.ch/), [https://devpost.com/software/wetrace-g9ocyi](https://devpost.com/software/wetrace-g9ocyi)


[5]    Prof. Carmela Troncoso (April 3, 2020) _DP-3T - Decentralized Privacy-Preserving Proximity Tracing_
https://github.com/DP-3T/documents](https://github.com/DP-3T/documents)


[6]    CoEpi (Community Epidemiology In Action) \
[https://www.coepi.org/](https://www.coepi.org/)


[7]    G.M. Morton, IBM (1966) _A computer oriented geodetic data base and a new technique in file sequencing_  \
[https://domino.research.ibm.com/library/cyberdig.nsf/papers/0DABF9473B9C86D48525779800566A39/$File/Morton1966.pdf](https://domino.research.ibm.com/library/cyberdig.nsf/papers/0DABF9473B9C86D48525779800566A39/$File/Morton1966.pdf)

[8]    CoEpi (April 3, 2020) _CEN Protocol_ \
[https://github.com/Co-Epi/CEN](https://github.com/Co-Epi/CEN)
