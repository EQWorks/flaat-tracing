# FLAAT Tracing


### Privacy-safe Decentralized Tracing with Informed Consent

EQ Works

First Published: April 6, 2020

There is an immediate need for health and government officials across the country to have access to high-quality contact tracing data, and there exists a variety of different mechanisms through which this data can be collected. However, as in any endeavor dealing with potentially sensitive information, maximizing the accuracy of the data obtained usually entails a consequent loss in privacy, and it is this balancing act between accuracy and privacy that deserves greater scrutiny. Any solution trying to address this issue will have to toe the line between the procurement of accurate and verifiable data while allowing consumers to rest assured behind a privacy shield. Such a solution would then open the doorway to widespread consumer adoption needed to reach the critical mass required to inform policy changes during the current COVID-19 crisis.

In this whitepaper, we are going to analyze the different ways in which cellular technology can be used for reliable contact tracing while still keeping the public's privacy intact using the frameworks in place by the Office of the Privacy Commissioner in Canada, thereby assuring users that their data can’t be used for anything other than minimizing the spread of COVID-19. This paper will deal with the following topics:

*   How the relevant data will be collected and stored.
*   How and when users will be informed when it is believed they may have come into contact with someone who is COVID-19 positive.
*   How users found/claiming to be COVID-19 positive will be verified without collecting identifiers that might compromise their identity.


### How to Log and Store the Data

**Privacy-safe identification** - In order to remove all traceability back to an individual, we’re proposing the adoption of the CEN identifier sequencing mechanism proposed by CoEpi<sup>[7]</sup>. This would be the only identifier that is either broadcast or uploaded to the repository. This identifier will not be associated with any other identifiers outside of the scope of the mobile application environment. It is possible to utilize other identity-linked identifiers (telephone numbers, MAIDs, etc.) within the mobile application environment subject to the users’ consent to share these attributes with the application in question. All validation against these identifiers must happen at the edge, locally within the mobile application scope using a hashing or encryption process to protect the sanctity of the user’s privacy. Under no circumstances must any non-privacy-safe identifier be broadcast, communicated or uploaded beyond the scope of the mobile application’s local scope and sandbox.

**Data logging specifics** - There are two mechanisms — geolocation and bluetooth<sup>[4]</sup> — by which data can be collected and used for COVID-19 contact tracing.

Geolocation can be used to track a user when their cell phone is active and location-sharing is turned on via permission management, allowing one to create a map tracing a user’s journey together with any associated timestamps. If a user happens to be in the vicinity of any of the verified COVID-19 positive devices at around the same time, he/she could then be notified of his/her elevated risk status<sup>[1]</sup>. This has major privacy implications. In order for the data to be useful, the location history would need to be as precise as possible. This would make it relatively easy to determine a user's home address, and remove the ability for the data to be truly anonymized. Geolocation can be stripped back to large areas for more privacy, but this would come at the cost of the accuracy of the data provided back to health officials. Moreover, users in any relatively high population density area run the risk of being bombarded with notifications, which could possibly result in widespread disengagement with the application in question.

Bluetooth on the other hand, would not require specific geolocation data to function; rather, only an anonymized unique identifier created on the device is required. The Bluetooth mechanism would search the immediate area for other Bluetooth signals, and upon finding them would create a “handshake” between the two devices that verifies these two devices were in the same area at the same time. In this approach, the precise location of the device at any given time is not required, as this process creates a relationship table of all of the anonymized identifiers within the devices that have come into contact with each other. The residential location of the user could be further scrubbed off of the geolocation log by using various heuristic techniques running locally on the mobile device. This allows health and government officials to accurately determine how many devices any given device has come into contact with, and notify the users if they have been in contact with a device that has been verified as COVID-19 positive, all without revealing any sensitive detailed location data that could be traced back to the user.

**Mass adoption strategy** - We believe the best possible chance of mass adoption depends on packaging the discovery, data logging, and secure-report validation into a mobile software library. The library will implement both geolocation tagging as well as Bluetooth handshake logs, allowing the applications to implement the protocol to manage various different variables that govern the tracing behavior. This flexibility would allow easy adoption by all the various parties trying to satisfy ground realities and public health challenges unique to each region. Using a single software library would enable a lot of individual apps with a big existing user base to incorporate this package and release a new binary, thereby avoiding a steep adoption curve that might otherwise hold most solutions back. Simultaneously, this also solves the problem of saturation occurring between two or more competing applications.

Once this library has been adopted by a sufficient number of applications, the chance of having an application that implements this library running in the foreground of a mobile device’s operating system increases drastically. There is also considerable technical evidence that one application on a mobile device running in the foreground that activates a sensor also benefits other background applications depending on that sensory input. This would allow an “official” COVID-19 tracing app to piggyback on top of support apps that implement the common library.

**Data storage specifics** - The data collected by the process outlined above can be stored either in centralized servers or locally on the mobile device itself.

Irrespective of the approach used, be it geolocation or Bluetooth, storing the data in a centralized repository will allow public health officials to accurately determine where all devices are/have been. This would make seamless the process of mapping all the users back to infected devices via geolocation or by the use of up-to-date relationship tables which maintain a record of devices that have come into contact with a COVID-19 positive device<sup>[3]</sup>. However, this increase in the accuracy of the data obtained comes with a corresponding concession in privacy. The issue lies in the fact that this mass dataset would be available on all devices all the time, regardless of whether a user has or will ever come into contact with a COVID-19 positive device.

Storing the data locally (on a user’s device, irretrievable without the explicit consent of the user) would limit the public authorities’ access. When a user has tested positive for COVID-19, he/she can then make the conscious decision to report and share their data back to a centralized repository for the public good. Data stored locally in this manner would then be deleted periodically as its epidemiological value diminishes over time.

Given the lack of a solution that covers all the various bases and the nature of the various compromises the two solutions mentioned above entail, we propose making available multiple mechanisms for a user to contribute (with consent) their logged epidemiologically valuable data for the explicit purpose of contact tracing, in the event of a positive COVID-19 diagnosis.


### How and when to inform users of cases spreading near them

**Notification frequency pitfalls** - Broadcasting possible contact with individuals who have a positive COVID-19 status in a timely manner to users is vital in stopping the spread early. This needs to be done accurately, as bombarding users with false-positive warnings can only lead to a gradual disengagement with the application in question. In the ideal scenario, a user would only be notified if they have an immediate health risk in order to maximize the impact this notification would have on that user.

Keeping this in mind, there are a few notification systems that could be implemented via a geohash protocol<sup>[6]</sup> as listed below:

*   Everyone in a general area is notified of new cases.
*   Only users who were in an epidemiologically relevant geohash of precise geolocation at the same time as a COVID-19 positive device are notified.
*   Only users whose devices have had a direct Bluetooth “handshake” with a positive device<sup>[5]</sup> are notified. Here, as mentioned earlier in the paper, a privacy-safe identifier is used to log the records of an individual found to be diagnosed with COVID-19.

It is worth pointing out that as we proceed further along in this list from top to bottom, the number of users receiving notifications gradually decreases, leading to a corresponding increase in the accuracy of these notifications.

We feel that a goal worth pursuing is to only notify the user if they have an immediate health risk, prompting them to either self-isolate or to seek medical attention. This warrants the use of either precise geolocation notification (accepting the privacy compromise) or Bluetooth “handshake” contact reporting as notification systems that can prompt the user into immediate action without running the risk of overexposure noted earlier in this section.

### How to verify reports

The verification of devices belonging to individuals with a positive COVID-19 status is crucial in order to preserve the purity of the dataset. False observations run the risk of pinging users with false notifications, and, as discussed in the preceding section, can render the entire notification system moot.

To deal with this issue, we propose two ways of implementing device verification:

*   The SDK of the app is used as an ID in the form of a 2D barcode, which the health official can scan to log and verify as a COVID-19 positive device. The device will then ping the device owner, who can then elect to share their data and notify users they may have come into contact with.
*   In the absence of the necessary infrastructure for this option to be technologically feasible, the health official will have a series of pre-generated one-time use alphanumeric tokens<sup>[2]</sup> they can provide to the COVID-19 positive device owner, who can then input that token into their device and select whether or not to share their data to notify other devices they may have come into contact with.


### Conclusion

Apropos of the discussion in the preceding paragraphs, we feel that the most accurate mechanism for contact tracing COVID-19 entails the following steps:

*   Bluetooth handshakes between devices are stored locally.
*   COVID-19 positive individuals are verified through their devices by means of a token generated by health officials.
*   Users are explicitly asked for consent to transmit their data in order to notify anyone that they have come in contact with.
*   Finally, geolocation for mapping high-risk areas can also be utilized in a privacy centric manner. Locally run heuristic techniques can be used that would strip out personally identifiable user information (such as home addresses, etc.) and ensure that the users’ privacy remains intact while still being able to provide public health officials with extremely valuable and relevant data.

This process offers the following undeniable advantages — it minimizes the data collected only to the bare minimum for the purpose at hand, it requires explicit user consent for any transmission of data and finally, it only notifies people of an immediate health risk. We are hopeful that these three facets of the system being proposed here will engender the general populace’s trust in the application, making it an effective tool with which to combat the spread of COVID-19.

[View API Specs](api-spec.md).

**References**

[1]	Ramesh Raskar, MIT (March 19, 2020) _Apps Gone Rogue: Maintaining Personal Privacy in an Epidemic_ [https://arxiv.org/pdf/2003.08567.pdf](https://arxiv.org/pdf/2003.08567.pdf)

[2]	Singapore Government Digital Services (April 1, 2020) _Trace together, safer together_ [https://www.tracetogether.gov.sg/](https://www.tracetogether.gov.sg/)

[3]	Dilshan Kathriarachchi & Global News (April 2, 2020) _Should Canada use our cell phones to slow the spread of COVID-19?_ [https://omny.fm/shows/wait-theres-more/should-canada-use-our-cell-phones-to-slow-the-spre](https://omny.fm/shows/wait-theres-more/should-canada-use-our-cell-phones-to-slow-the-spre)

[4]	WeTrace & Andreas Gassmann (March 30, 2020) _Privacy-Preserving Bluetooth COVID-19 Contract Tracing_ [https://wetrace.ch/](https://wetrace.ch/), [https://devpost.com/software/wetrace-g9ocyi](https://devpost.com/software/wetrace-g9ocyi)

[5]	Prof. Carmela Troncoso (April 3, 2020) _DP-3T - Decentralized Privacy-Preserving Proximity Tracing_ [https://github.com/DP-3T/documents](https://github.com/DP-3T/documents)

[6]	G.M. Morton, IBM (1966) _A computer oriented geodetic data base and a new technique in file sequencing_ [https://domino.research.ibm.com/library/cyberdig.nsf/papers/0DABF9473B9C86D48525779800566A39/$File/Morton1966.pdf](https://domino.research.ibm.com/library/cyberdig.nsf/papers/0DABF9473B9C86D48525779800566A39/$File/Morton1966.pdf)

[7]	CoEpi (April 3, 2020) _CEN Protocol_ [https://github.com/Co-Epi/CEN](https://github.com/Co-Epi/CEN)
