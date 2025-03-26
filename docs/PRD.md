# Revised Modular Structure for UCO Observable Ontology

## Overview of Existing UCO Observables
The Unified Cyber Ontology (UCO) Observable module currently contains a broad range of classes representing cyber artifacts (files, network packets, user accounts, etc.) and associated Facet classes that group their properties. In total there are hundreds of observable classes and facets in UCO (over 150 under the uco:observable namespace) spanning many domains​. For example, UCO defines classes like File, Process, IPAddress, DomainName, EmailMessage, UserAccount, etc., each with a corresponding Facet class capturing its attributes. This facet-based design (inherited from the CASE ontology) groups properties into re-usable bundles attached to objects​. While this provides flexibility and detail, the monolithic structure of the observables ontology can be overwhelming. There is a need to partition the ontology into disjoint modules aligned with distinct cyber domains to improve clarity and adoption.

Currently, many observable classes are direct subclasses of a generic ObservableObject without higher-level grouping, meaning concepts like files, network traffic, and accounts all live in one namespace. Some mid-level abstractions exist (e.g. Device with subclasses like DigitalCamera or GamingConsole​, or Account with subclasses like DigitalAccount​), but by and large the ontology isn't yet segmented by domain. The goal is to define clear modular groupings – each covering a disjoint area of cyber observables – such that no class overlaps between modules. Disjoint modules will help avoid confusion (an IP address won't also be classified as a file, for example) and make the ontology easier to extend for specific domains.

## Gaps and Additional Domains for Observables
Before defining the modules, it's important to identify which cyber domains are not fully covered by the current ontology. By reviewing industry frameworks and literature, we find a few notable gaps:

### Cloud Infrastructure and Virtualization
UCO has extensive host and network artifacts but lacks explicit representation of cloud or virtual resources (no classes for virtual machines, containers, cloud services, etc.). Modern frameworks like MITRE ATT&CK treat Cloud and Container environments as distinct platforms, indicating the need for cloud-specific observables​. For example, ATT&CK defines data sources for Cloud Service activity​, and Elastic's common schema notes that hosts can be physical or virtual (including Docker containers and Kubernetes nodes)​. Introducing cloud/virtualization observables (e.g. VM instances, container images, cloud storage objects) will fill this gap.

### Industrial Control Systems (ICS) and OT
The current ontology is focused on IT artifacts; it does not define observables unique to industrial control systems (e.g. PLC devices, SCADA tags, field sensor readings). MITRE has a dedicated ICS ATT&CK matrix​ and identifies ICS-specific data sources (like device asset inventories and control logs)​. Practitioners in critical infrastructure security would expect observables for control system components. A new ICS module can introduce classes for controllers, actuators, sensor telemetry, etc., kept disjoint from IT network observables.

### Social Media and Online Content
UCO does include some classes for social media (e.g. Tweet, WikiArticle, ForumPost) and web artifacts (BrowserBookmark, Cookie, URLHistory), but these could be better consolidated into their own module. The ontology can be improved to cover online content observables such as social media profiles, posts, and metadata in a coherent way. This is a growing area in cyber investigations (for OSINT and digital forensics), and having a dedicated module would highlight its importance.

### Multimedia (Video) Content
While there are classes for images (RasterPicture) and audio (Audio), there is surprisingly no class for video files or streams. Given the prevalence of video evidence (CCTV footage, screen recordings, body-cam video in investigations), adding a Video observable (with a facet for properties like encoding, duration, etc.) would improve completeness. This can be grouped with other content/media observables.

### General Missing Artifacts
Other niche areas that could merit observables include application-specific logs (beyond the generic EventLog), configuration artifacts (the ontology has Windows Registry keys, but perhaps not things like cloud configuration or application config files), and DevOps/CI artifacts (build pipelines, code repositories). These are less universally recognized than the major gaps above, but worth noting for future extension. Overall, the most pressing additions are cloud and ICS domains, since these are explicitly recognized in industry frameworks as separate domains of activity​.

## Proposed Observable Ontology Modules
Below is a breakdown of the proposed modular structure for the UCO Observable ontology. Each module represents a distinct domain of cyber observables, with clear boundaries and relationships to other modules.

### Core Module (observable-core.ttl)
The foundation module containing the base classes that all other modules extend:

1. **DefinedEffectFacet** - The base facet for defining effects of actions on observable objects
2. **ObservableAction** - Actions that can be observed within the digital domain
3. **ObservableObject** - The fundamental base class for all observable objects
4. **ObservablePattern** - Patterns of observable characteristics
5. **ObservableRelationship** - Relationships between observable objects

### Host & System Module (observable-host-system.ttl)
Contains classes related to host systems and operating systems:

1. File System Classes
   - File
   - Directory
   - FileSystem
   - File Permissions
   - Content Data

2. Operating System Classes
   - OperatingSystem
   - Process
   - Thread
   - Memory
   - Volume

3. Windows-specific Classes
   - WindowsRegistryKey
   - WindowsRegistryValue
   - WindowsEvent

4. UNIX-specific Classes
   - UNIXProcess
   - UNIXFilePermissions

### Network Module (observable-network.ttl)
Contains classes related to network operations and artifacts:

1. Address Classes
   - IPAddress (IPv4Address, IPv6Address)
   - MACAddress
   - DigitalAddress

2. Network Connection Classes
   - NetworkConnection
   - NetworkFlow
   - Socket

3. URL and Domain Classes
   - URL
   - DomainName

4. DNS and ARP Cache Classes
   - DNSCache
   - DNSRecord
   - ARPCache

5. Network Interface Classes
   - NetworkInterface
   - NetworkProtocol

## Implementation Guidelines
1. Each module should be self-contained with clear dependencies
2. Use consistent prefix naming across modules
3. Maintain proper import chains between modules
4. Document class relationships and hierarchies
5. Follow UCO best practices for ontology design

## Success Criteria
1. All observable classes properly categorized
2. No broken relationships or dependencies
3. Improved maintainability and readability
4. Successful validation of ontology structure
5. Backward compatibility maintained

## Future Considerations
1. Additional domain-specific modules (Cloud, ICS, etc.)
2. Enhanced documentation and examples
3. Integration with other UCO modules
4. Community feedback and contributions
5. Version management strategy 