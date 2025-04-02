# UCO Observable Class Analysis for Modular Realignment

This document analyzes the current UCO observable classes and properties in order to realign them with the new modular structure proposed in the PRD.md document. The analysis maps each class to its most appropriate target module based on the domain-driven modular breakdown.

## Complete Analysis Approach

The observable.ttl file contains classes under the observable namespace. This analysis:
1. Identifies each observable class and its properties
2. Assigns each class to the most appropriate target module following the PRD.md modular structure
3. Provides justification for the module assignment based on domain alignment

The module structure includes:
- Core Observables Module (observable-core.ttl)
- Network Observables Module (obserbable-network.ttl)
- Host & System Observables Module (observable-host-system.ttl) 
- Identity & Account Observables Module (observable-identity-account.ttl)
- Software & Execution Observables Module (observable-software-execution.ttl)
- Communication & Messaging Observables Module (observable-communication-messaging.ttl)
- Social Media & Online Content Observables Module (observable-socialmedia-onlinecontent.ttl)
- Device & Hardware Observables Module (observable-device-hardware.ttl)
- Cloud & Virtual Infrastructure Observables Module (observable-cloud-virtualinfrastructure.ttl)
- Industrial Control Systems (ICS) Observables Module (observable-industrial-control-systems.ttl)
- Content & Media Module (for media content like audio, images, video) (observable-content-media.ttl)

## Class and Property Realignment Analysis

| Class Name | Property Name | Target Module Name | Justification for Realignment to new Module |
|------------|---------------|-------------------|----------------------------------------------|
| API | - | Software & Execution | APIs are interfaces for software, making them conceptually part of the software domain rather than host artifacts or network objects. |
| ARPCache | - | Network | ARP caches contain network address resolution data, clearly placing them in the Network module as they deal with mapping between network layers. |
| ARPCacheEntry | - | Network | Individual ARP entries are network address resolution artifacts that belong in the Network module. |
| Account | - | Identity & Account | The base Account class is the foundation of the Identity & Account module, representing digital identities. |
| AccountAuthenticationFacet | password, passwordLastChanged, passwordType | Identity & Account | Authentication data is directly related to account access and identity verification. |
| AccountFacet | accountIdentifier, accountType, isActive, etc. | Identity & Account | Core properties of account objects that define digital identity characteristics. |
| Adaptor | - | Device & Hardware | As a physical device that converts pin outputs, this is clearly a hardware component. |
| Address | - | Network | The base Address class represents identifiers for routing and managing information, a core networking concept. |
| AlternateDataStream | - | Host & System | Alternate data streams are a feature of NTFS file systems, making them part of the host/system domain. |
| AlternateDataStreamFacet | name, size, hashes | Host & System | Properties of NTFS alternate data streams that are host file system artifacts. |
| AndroidDevice | - | Device & Hardware | Physical device that runs a specific operating system, belongs in the Device module. |
| AndroidDeviceFacet | androidID, androidVersion, isADBRootEnabled, etc. | Device & Hardware | Properties specific to Android devices that characterize hardware. |
| AndroidPhone | - | Device & Hardware | Specific type of mobile device that should be categorized with other hardware devices. |
| AntennaFacet | antennaHeight, azimuth, elevation, etc. | Device & Hardware | Properties describing physical antenna characteristics of hardware devices. |
| AppleDevice | - | Device & Hardware | Apple hardware should be classified with other physical devices. |
| Appliance | - | Device & Hardware | Purpose-built computers are physical hardware devices. |
| Application | - | Software & Execution | Applications are software programs, the core of the Software module. |
| ApplicationAccount | - | Identity & Account | Accounts specific to software applications still fall under the Identity & Account domain. |
| ApplicationAccountFacet | application | Identity & Account | Properties of application-specific accounts, connecting identity to software. |
| ApplicationFacet | applicationIdentifier, version, numberOfLaunches, etc. | Software & Execution | Properties that describe software applications. |
| ApplicationVersion | version, installDate, uninstallDate | Software & Execution | Metadata about software versions, clearly within software domain. |
| ArchiveFile | - | Host & System | Archive files are a type of file, which falls under the Host & System module. |
| ArchiveFileFacet | archiveType, version, comment | Host & System | Properties specific to archive files stored on host systems. |
| Audio | - | Content & Media | Audio is digital media content rather than a host artifact or network object. |
| AudioFacet | audioType, format, bitRate, duration | Content & Media | Properties describing digital audio content. |
| AutonomousSystem | - | Network | AS numbers and routing systems are core network infrastructure components. |
| AutonomousSystemFacet | number, asHandle, regionalInternetRegistry | Network | Properties of network routing infrastructure. |
| BlackberryPhone | - | Device & Hardware | Mobile device hardware that belongs with other devices. |
| BlockDeviceNode | - | Host & System | UNIX filesystem special files are part of the host operating system. |
| BluetoothAddress | - | Network | Bluetooth addresses are network identifiers for Bluetooth communication. |
| BluetoothAddressFacet | - | Network | Properties of Bluetooth network addresses. |
| BotConfiguration | - | Software & Execution | Configuration for automated software belongs in the Software module. |
| BrowserBookmark | - | Social Media & Online Content | Browser bookmarks reference web content and are part of web browsing artifacts. |
| BrowserBookmarkFacet | application, visitCount, urlTargeted, etc. | Social Media & Online Content | Properties of web browsing artifacts. |
| BrowserCookie | - | Social Media & Online Content | Browser cookies are web browsing artifacts. |
| BrowserCookieFacet | cookieName, cookiePath, expirationTime, etc. | Social Media & Online Content | Properties describing web browsing data. |
| Calendar | - | Communication & Messaging | Calendars often contain meeting invites and shared events, making them communication artifacts. |
| CalendarEntry | - | Communication & Messaging | Individual calendar events are communication-related. |
| CalendarEntryFacet | eventStatus, endTime, startTime, etc. | Communication & Messaging | Properties of calendar events used for communication scheduling. |
| CalendarFacet | owner, application | Communication & Messaging | Properties of calendar objects used for communication planning. |
| Call | - | Communication & Messaging | Calls are direct communication between parties. |
| CallFacet | callType, duration, participant, startTime, etc. | Communication & Messaging | Properties describing communication events. |
| CapturedTelecommunicationsInformation | - | Communication & Messaging | Intercepted communications data belongs in the communication module. |
| CapturedTelecommunicationsInformationFacet | captureCellSite, startTime, endTime, etc. | Communication & Messaging | Properties of captured communications. |
| CellSite | - | Device & Hardware | Cell towers are physical network infrastructure devices. |
| CellSiteFacet | cellSiteType, cellSiteIdentifier, etc. | Device & Hardware | Properties describing cellular infrastructure hardware. |
| CharacterDeviceNode | - | Host & System | UNIX filesystem special files are part of the host operating system. |
| Code | - | Software & Execution | Source code and binary representations are software artifacts. |
| CompressedStreamFacet | compressionMethod, compressionRatio | Host & System | Data compression properties for files/data on host systems. |
| Computer | - | Device & Hardware | Computers are hardware devices. |
| ComputerSpecification | - | Device & Hardware | Technical details about computer hardware. |
| ComputerSpecificationFacet | biosVersion, cpuFamily, totalRam, etc. | Device & Hardware | Detailed properties of computer hardware specifications. |
| ConfiguredSoftware | - | Software & Execution | Installed and configured software applications. |
| Contact | - | Communication & Messaging | Contacts are used primarily for communication purposes. |
| ContactAddress | - | Communication & Messaging | Physical addresses used for communication. |
| ContactAffiliation | - | Communication & Messaging | Organizational relationships relevant to communication. |
| ContactEmail | - | Communication & Messaging | Email contact information for communication. |
| ContactFacet | contactID, lastName, firstName, etc. | Communication & Messaging | Core properties of contacts used for communication. |
| ContactList | - | Communication & Messaging | Collections of contacts for communication purposes. |
| ContactListFacet | contactListName, owner, sourceApplication | Communication & Messaging | Properties of contact lists used for communications. |
| ContactMessaging | - | Communication & Messaging | Messaging contact details for communication. |
| ContactPhone | - | Communication & Messaging | Phone contact information for communication. |
| ContactProfile | - | Social Media & Online Content | Social media profile information for contacts. |
| ContactSIP | - | Communication & Messaging | SIP (Session Initiation Protocol) contact details for VoIP. |
| ContactURL | - | Communication & Messaging | URL-based contact information. |
| ContentData | - | Host & System | Generic digital data blocks are typically found on host systems. |
| ContentDataFacet | dataPayload, hash, mimeType, byteOrder, etc. | Host & System | Properties describing data stored on systems. |
| CookieHistory | - | Social Media & Online Content | Browser cookie history is web browsing data. |
| Credential | - | Identity & Account | Login credentials are directly related to identity and account access. |
| CredentialDump | - | Identity & Account | Collections of credentials are identity & account artifacts. |
| DNSCache | - | Network | DNS caches contain domain resolution data, a network service. |
| DNSRecord | - | Network | DNS records define network name resolution. |
| DataRangeFacet | rangeOffset, rangeSize, rangeOffsetType | Host & System | Properties describing ranges within data blocks on systems. |
| DefinedEffectFacet | - | Core Observables | Base facet for defining effects of actions on observable objects. |
| Device | - | Device & Hardware | The base Device class is foundational to the Device & Hardware module. |
| DeviceFacet | deviceType, model, manufacturer, etc. | Device & Hardware | Core properties that describe hardware devices. |
| DigitalAccount | - | Identity & Account | Base class for digital accounts across platforms. |
| DigitalAccountFacet | displayName | Identity & Account | Properties of digital accounts. |
| DigitalAddress | - | Network | Digital addresses are used for network routing and communication. |
| DigitalAddressFacet | displayName | Network | Properties of digital addresses used in networking. |
| DigitalCamera | - | Device & Hardware | Physical camera devices. |
| DigitalSignatureInfo | - | Identity & Account | Digital signatures relate to identity verification. |
| DigitalSignatureInfoFacet | certificateIssuer, signatureExists, etc. | Identity & Account | Properties of digital signatures used for identity verification. |
| Directory | - | Host & System | Directories are fundamental file system components. |
| Disk | - | Device & Hardware | Physical storage devices. |
| DiskFacet | diskSize, diskType, freeSpace, etc. | Device & Hardware | Properties of physical storage devices. |
| DiskPartition | - | Device & Hardware | Storage partitions are more closely tied to physical media than file contents. |
| DiskPartitionFacet | partitionID, partitionLength, spaceLeft, etc. | Device & Hardware | Properties of disk partition structures. |
| DomainName | - | Network | Domain names are network addressing artifacts. |
| DomainNameFacet | isTLD, value | Network | Properties of network domain names. |
| Drone | - | Device & Hardware | Unmanned aerial vehicles are hardware devices. |
| EXIFFacet | height, width, meteringMode, etc. | Content & Media | Properties embedded in digital image files. |
| EmailAccount | - | Identity & Account | Email accounts are a type of digital identity. |
| EmailAccountFacet | emailAddress | Identity & Account | Properties of email accounts. |
| EmailAddress | - | Identity & Account | Email addresses are identifiers linked to accounts. |
| EmailAddressFacet | displayName, value | Identity & Account | Properties of email addresses used for account identification. |
| EmailMessage | - | Communication & Messaging | Email messages are communications between parties. |
| EmailMessageFacet | body, sentTime, recipients, subject, etc. | Communication & Messaging | Properties of email communications. |
| EmbeddedDevice | - | Device & Hardware | Embedded systems and devices are hardware components. |
| EncodedStreamFacet | encodingMethod | Host & System | Properties of encoded data streams on systems. |
| EncryptedStream | - | Host & System | Encrypted data on host systems. |
| EncryptedStreamFacet | encryptionMethod, encryptionKey, etc. | Host & System | Properties of encrypted data on host systems. |
| EnvironmentVariable | - | Host & System | System environment variables are OS configuration artifacts. |
| EnvironmentVariableFacet | value, name | Host & System | Properties of OS environment variables. |
| Event | - | Host & System | System events are host-based observables. |
| EventFacet | eventType, observableCreatedTime, etc. | Host & System | Properties of system events. |
| EventRecord | - | Host & System | Individual event log records. |
| EventRecordFacet | eventRecordID, eventType, observableCreatedTime, etc. | Host & System | Properties of individual event records. |
| File | - | Host & System | Files are core artifacts of host systems. |
| FileFacet | fileName, extension, size, etc. | Host & System | Properties describing files on host systems. |
| FilePermissionsFacet | owner, group, permissions, etc. | Host & System | Properties related to file permissions on host systems. |
| FileSystem | - | Host & System | File systems are fundamental host storage structures. |
| FileSystemObject | - | Host & System | Base class for file system artifacts. |
| ForumPost | - | Social Media & Online Content | Content from online forums is social media content. |
| ForumThread | - | Social Media & Online Content | Collections of forum posts are social media content. |
| GamingConsole | - | Device & Hardware | Gaming devices are hardware devices. |
| GeoLocationEntry | - | Location | Geographic location information. |
| GeoLocationEntryFacet | altitude, latitude, longitude, etc. | Location | Properties describing geographic locations. |
| GeoLocationLog | - | Location | Historical log of geographic locations. |
| GeoLocationLogFacet | application | Location | Properties of location history logs. |
| GeoLocationTrack | - | Location | Series of locations forming a movement track. |
| GeoLocationTrackFacet | endTime, startTime | Location | Properties of geographic movement tracks. |
| HTTPConnection | - | Network | HTTP network connections. |
| HTTPConnectionFacet | httpMethod, host, port, etc. | Network | Properties of HTTP network connections. |
| ICMPConnection | - | Network | ICMP network communications. |
| ICMPConnectionFacet | icmpCode, icmpType | Network | Properties of ICMP network traffic. |
| IPAddress | - | Network | IP addresses are fundamental network identifiers. |
| IPv4Address | - | Network | IP addresses are fundamental network identifiers. |
| IPv4AddressFacet | value | Network | Properties of IPv4 network addresses. |
| IPv6Address | - | Network | IP addresses are fundamental network identifiers. |
| IPv6AddressFacet | value | Network | Properties of IPv6 network addresses. |
| Image | - | Content & Media | Digital images are media content. |
| ImageFacet | imageType, width, height, etc. | Content & Media | Properties of digital images. |
| InstantMessaging | - | Communication & Messaging | Chat and instant messaging communications. |
| InstantMessagingAddress | - | Communication & Messaging | Addresses for instant messaging communications. |
| JSONFileFacet | keyValues | Host & System | Properties of JSON format files. |
| Laptop | - | Device & Hardware | Portable computers are hardware devices. |
| Library | - | Software & Execution | Software libraries are reusable code components. |
| MACAddress | - | Network | MAC addresses are hardware network identifiers. |
| MACAddressFacet | value | Network | Properties of MAC addresses. |
| MFTRecordFacet | mftFileNameTimeStamp, mftFlags, etc. | Host & System | Master File Table records for NTFS file systems. |
| Memory | - | Host & System | Computer memory is a host system resource. |
| MemoryFacet | isVolatile, regionSize, regionStartAddress | Host & System | Properties of computer memory. |
| Message | - | Communication & Messaging | Generic message communications. |
| MessageFacet | application, sentTime, from, etc. | Communication & Messaging | Properties of message communications. |
| MessageThread | - | Communication & Messaging | Threads of related message communications. |
| MessageThreadFacet | visibility, participants | Communication & Messaging | Properties of message conversation threads. |
| MftRecord | - | Host & System | Master File Table records in NTFS. |
| MobileAccount | - | Identity & Account | Accounts on mobile devices. |
| MobileAccountFacet | IMSI, MSISDN | Identity & Account | Properties of mobile device accounts. |
| MobileDevice | - | Device & Hardware | Mobile phones and tablets are hardware devices. |
| MobileDeviceFacet | IMEI, bluetoothDeviceName, etc. | Device & Hardware | Properties of mobile device hardware. |
| Mutex | - | Host & System | Mutual exclusion objects for process synchronization. |
| MutexFacet | isNamed, name | Host & System | Properties of process synchronization objects. |
| NTFSFilePermissionsFacet | sid, mode | Host & System | NTFS-specific file permission properties. |
| NTFSFileFacet | alternateDataStreams, SID | Host & System | NTFS-specific file system properties. |
| NetworkConnection | - | Network | Network connections represent communication paths between network nodes. |
| NetworkConnectionFacet | protocols, destinationPort, etc. | Network | Properties of network connections. |
| NetworkFlow | - | Network | Network traffic flows. |
| NetworkFlowFacet | source, destination, ipfix, etc. | Network | Properties of network traffic flows. |
| NetworkInterface | - | Network | Interfaces connect hosts to networks, a network boundary component. |
| NetworkInterfaceFacet | IP, mac, dhcpLeaseExpires, etc. | Network | Properties of network interface cards. |
| NetworkRoute | - | Network | Network routing information. |
| NetworkRouteFacet | destinationAddress, gateway, etc. | Network | Properties of network routes. |
| NetworkSocket | - | Network | Network sockets for communication. |
| NetworkSocketFacet | socketType, socketDescriptor, etc. | Network | Properties of network socket connections. |
| NetworkSubnet | - | Network | Network subnet groupings. |
| NetworkSubnetFacet | cidr, networkAddressFamily, etc. | Network | Properties of network subnet structures. |
| Note | - | Content & Media | User-created notes are content. |
| NoteFacet | application, content, author, etc. | Content & Media | Properties of user-created notes. |
| ObservableAction | - | Core Observables | Actions performed on or by observable objects. |
| ObservableObject | - | Core Observables | Base class for all observable objects. |
| ObservablePattern | - | Core Observables | Patterns of observable objects. |
| ObservableRelationship | - | Core Observables | Relationships between observable objects. |
| OperatingSystem | - | Host & System | Operating systems manage host hardware and provide execution environments. |
| OperatingSystemFacet | manufacturer, version, etc. | Host & System | Properties of operating systems. |
| PDFFile | - | Host & System | PDF document files. |
| PDFFileFacet | documentInfo, pdfId0, pdfId1, etc. | Host & System | Properties of PDF files. |
| PathRelationFacet | path | Host & System | Properties relating to file paths. |
| PhoneAccount | - | Identity & Account | Accounts associated with telephony services. |
| PhoneAccountFacet | phoneNumber | Identity & Account | Properties of telephone accounts. |
| PhoneCall | - | Communication & Messaging | Telephone calls are communications. |
| PhotoAlbum | - | Content & Media | Collections of digital photos. |
| PhysonAlbumFacet | albumTitle, createdTime, etc. | Content & Media | Properties of digital photo collections. |
| Process | - | Host & System | Running processes exist on host systems. |
| ProcessFacet | pid, command, arguments, etc. | Host & System | Properties of running processes. |
| ProfilingData | - | Software & Execution | Data about software execution profiling. |
| ProfilingDataFacet | programCounter, stackPointer, etc. | Software & Execution | Properties of software execution profiling. |
| RasterPicture | - | Content & Media | Raster format digital images. |
| RasterPictureFacet | bitsPerPixel, pictureType, etc. | Content & Media | Properties of raster image files. |
| RecoveredObject | - | Host & System | Objects recovered from systems. |
| RecoveredObjectFacet | contentRecoveredStatus | Host & System | Properties of recovered digital artifacts. |
| RegistryDatatype | - | Host & System | Windows registry data types. |
| RegistryDatatypeFacet | registryDataTypeValue | Host & System | Properties of Windows registry data types. |
| RegistryHive | - | Host & System | Windows registry hives. |
| RegistryHiveFacet | hiveType | Host & System | Properties of Windows registry hives. |
| RegistryKey | - | Host & System | Windows registry keys. |
| RegistryKeyFacet | key, modifiedTime, numberOfSubkeys, etc. | Host & System | Properties of Windows registry keys. |
| RegistryValue | - | Host & System | Windows registry values. |
| RegistryValueFacet | dataType, name, value | Host & System | Properties of Windows registry values. |
| SIMCard | - | Device & Hardware | SIM cards are hardware devices for mobile networks. |
| SIMCardFacet | ICCID, IMSI, carrier, etc. | Device & Hardware | Properties of SIM card hardware. |
| SMSMessage | - | Communication & Messaging | Text messages are communications between parties. |
| SMSMessageFacet | messageBody, messageType, etc. | Communication & Messaging | Properties of SMS text messages. |
| SQLiteBlob | - | Host & System | Binary objects in SQLite databases. |
| SQLiteBlobFacet | rowIndex, columnName, etc. | Host & System | Properties of SQLite database binary objects. |
| SecurityAppliance | - | Device & Hardware | Security hardware devices. |
| Semaphore | - | Host & System | Process synchronization mechanisms. |
| SemaphoreFacet | current, maximum | Host & System | Properties of process synchronization mechanisms. |
| SendControlCodeEffectFacet | controlCode | Host & System | Properties of control code operations. |
| Server | - | Device & Hardware | Server hardware. |
| ShopListing | - | Social Media & Online Content | Online shop/e-commerce listings. |
| ShopListingFacet | price, currency, etc. | Social Media & Online Content | Properties of online marketplace listings. |
| SimpleAddressFacet | country, locality, postalCode, etc. | Identity & Account | Properties of physical addresses associated with accounts. |
| SmartDevice | - | Device & Hardware | Internet of Things and smart devices. |
| SmartPhone | - | Device & Hardware | Smartphones are mobile computing devices. |
| Snapshot | - | Device & Hardware | System state snapshots. |
| Socket | - | Network | Socket communication endpoints. |
| Software | - | Software & Execution | General software programs and applications. |
| SoftwareFacet | swid, version, etc. | Software & Execution | Properties describing software. |
| SourceCode | - | Software & Execution | Software source code. |
| SymbolicLink | - | Host & System | Symbolic links in file systems. |
| SymbolicLinkFacet | targetFile | Host & System | Properties of symbolic links. |
| TCPConnection | - | Network | TCP network connections. |
| TCPConnectionFacet | sourceFlags, destinationFlags, etc. | Network | Properties of TCP connections. |
| Thread | - | Host & System | Execution threads within processes. |
| ThreadFacet | threadID, createdTime | Host & System | Properties of process threads. |
| Tweet | - | Social Media & Online Content | Twitter posts are social media content. |
| TwitterProfileFacet | profileBackgroundLocation, etc. | Social Media & Online Content | Properties of Twitter user profiles. |
| UDPConnection | - | Network | UDP network connections. |
| UDPConnectionFacet | destinationPort, sourcePort | Network | Properties of UDP connections. |
| URL | - | Network | URLs are network resource locators. |
| URLFacet | fullValue, host, etc. | Network | Properties of network URLs. |
| URLHistory | - | Social Media & Online Content | Web browsing history. |
| URLHistoryEntry | - | Social Media & Online Content | Individual web browsing history entries. |
| URLHistoryFacet | browserInformation, etc. | Social Media & Online Content | Properties of web browsing history. |
| URLVisit | - | Social Media & Online Content | Individual visits to web URLs. |
| URLVisitFacet | visitTime, urlHistoryEntry | Social Media & Online Content | Properties of individual web page visits. |
| UNIXAccount | - | Identity & Account | User accounts on UNIX systems. |
| UNIXAccountFacet | gid, shell, homeDirectory, etc. | Identity & Account | Properties of UNIX user accounts. |
| UNIXFilePermissionsFacet | owner, group, mode, etc. | Host & System | UNIX file permission properties. |
| UNIXProcess | - | Host & System | Processes on UNIX systems. |
| UNIXProcessFacet | openFileDescriptors, pid, etc. | Host & System | Properties of UNIX processes. |
| UNIXVolumeFacet | mountPoint, options, etc. | Host & System | Properties of UNIX storage volumes. |
| UserAccount | - | Identity & Account | User accounts represent digital identities for individuals. |
| UserAccountFacet | canEscalatePrivs, isPrivileged, etc. | Identity & Account | Properties of user accounts. |
| UserSession | - | Host & System | User login sessions on systems. |
| UserSessionFacet | effectiveGroup, effectiveUser, etc. | Host & System | Properties of user login sessions. |
| VoIP | - | Communication & Messaging | Voice over IP communications. |
| VoIPFacet | application, etc. | Communication & Messaging | Properties of VoIP communications. |
| Volume | - | Host & System | Logical storage volumes. |
| VolumeFacet | sectorSize, volumeID, etc. | Host & System | Properties of logical storage volumes. |
| Web | - | Social Media & Online Content | Generic web content. |
| WebPage | - | Social Media & Online Content | Web pages are online content. |
| WebPageFacet | expirationTime, links, etc. | Social Media & Online Content | Properties of web pages. |
| WhoIs | - | Network | Domain registration information. |
| WhoIsFacet | domainName, registrarInfo, etc. | Network | Properties of domain registration information. |
| WiFiAddress | - | Network | WiFi network addresses. |
| WiFiAddressFacet | value | Network | Properties of WiFi addresses. |
| WikiArticle | - | Social Media & Online Content | Wiki-based content. |
| WikiArticleFacet | contributors, etc. | Social Media & Online Content | Properties of wiki articles. |
| WindowsAccount | - | Identity & Account | User accounts on Windows systems. |
| WindowsAccountFacet | groups | Identity & Account | Properties of Windows user accounts. |
| WindowsActiveDirectoryAccount | - | Identity & Account | Active Directory accounts. |
| WindowsActiveDirectoryAccountFacet | activeDirectoryGroups, etc. | Identity & Account | Properties of Active Directory accounts. |
| WindowsComputerSpecificationFacet | registryValues, etc. | Device & Hardware | Windows-specific computer hardware properties. |
| WindowsPEBinaryFile | - | Host & System | Windows PE format executable files. |
| WindowsPEBinaryFileFacet | peType, importedFunctions, etc. | Host & System | Properties of Windows executable files. |
| WindowsPrefetchFacet | accessedDirectories, etc. | Host & System | Properties of Windows prefetch files. |
| WindowsProcess | - | Host & System | Processes on Windows systems. |
| WindowsProcessFacet | aslr, dep, handleList, etc. | Host & System | Properties of Windows processes. |
| WindowsRegistryHive | - | Host & System | Windows registry hive files. |
| WindowsRegistryKey | - | Host & System | Registry keys are Windows system configuration artifacts. |
| WindowsRegistryValue | - | Host & System | Windows registry key values. |
| WindowsService | - | Host & System | Windows background services. |
| WindowsServiceFacet | displayName, serviceType, etc. | Host & System | Properties of Windows services. |
| WindowsSystem | - | Host & System | Windows operating systems. |
| WindowsSystemFacet | globalFlagList | Host & System | Properties of Windows systems. |
| WindowsTask | - | Host & System | Windows scheduled tasks. |
| WindowsTaskFacet | account, application, etc. | Host & System | Properties of Windows scheduled tasks. |
| WindowsThread | - | Host & System | Threads in Windows processes. |
| WindowsThreadFacet | createdTime, priority, etc. | Host & System | Properties of Windows threads. |
| WindowsVolumeFacet | driveLetter, driverName, etc. | Host & System | Windows-specific volume properties. |
| Wireless | - | Network | Wireless network connections. |
| WirelessNetworkConnection | - | Network | Wireless network connection sessions. |
| WirelessNetworkConnectionFacet | baseStation, ssid, etc. | Network | Properties of wireless network connections. |
| X509Certificate | - | Identity & Account | Digital certificates relate to identity verification. |
| X509CertificateFacet | isSelfSigned, version, etc. | Identity & Account | Properties of X.509 digital certificates. |
| X509V3Extensions | - | Identity & Account | X.509 certificate extensions. |
| X509V3ExtensionsFacet | basicConstraints, etc. | Identity & Account | Properties of X.509 certificate extensions. |

This analysis provides a mapping of all observable classes from the current UCO observable ontology to the new modular structure.

For new additions mentioned in the PRD:
- Cloud instances, containers, and cloud services would go to the new Cloud & Virtual Infrastructure module
- PLCs, RTUs, HMIs, and ICS devices would go to the new Industrial Control Systems module
- Video files would be added to the Content & Media module (alongside existing Audio and Image classes)
