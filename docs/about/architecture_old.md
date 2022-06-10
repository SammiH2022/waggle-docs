---
sidebar_position: 3
---

# Architecture
![Figure 1: A high-level overview of the Sage Cyber-infrastructure](./images/SAGE_CI.jpg)

The Sage project will design and build a new kind of national-scale reusable cyber-infrastructure to enable AI at the edge.  The illustration above shows a high-level view of the Sage CI architecture and enumerates the various software services, tools and infrastructure pieces. Below a quick summary of each of the components and their interrelationships is provided.


## Nodes

#### [Sage Node](https://github.com/sagecontinuum/nodes)
Any Edge node part of the Sage project.  This includes new AoT nodes, Wild Sage nodes, and Sage Blades.

#### [Array of Things (AoT) Node](https://arrayofthings.github.io/)
A weatherized Waggle Node designed to be installed on a street pole in the city or mounted on exterior walls.  An AoT node usually includes a sensor pod that includes air quality sensors.  The device is also attractive for an urban setting.

#### [Wild Sage Node](https://github.com/sagecontinuum/nodes)
This identifies Waggle Nodes that are weatherized for remote, outdoor deployment as part of the Sage project.  These nodes are similar to AoT nodes, but since urban aesthetics are not needed, and different cameras and sensors might be used, the Wild Sage Node may look strange.  Wild Sage Nodes look like proper bits of science experiments mounted outside, while AoT nodes look like they deserve an architectural award.

#### [Sage Blade](https://github.com/sagecontinuum/nodes)
This identifies Waggle Nodes that are standard, commercially available blade server or box intended for use in a machine room or climate controlled telecommunications hut.  For the Sage project, the first Sage Blades are Dell XR2 1U servers that have been hardened for increased environmental range. They include a powerful NVIDIA GPU for AI@Edge compute jobs.  As a Waggle Node, they run the complete Waggle software stack, and therefore can run Edge jobs, report data, and be remotely configured.

#### [Waggle Node](https://github.com/waggle-sensor/waggle)
This slang indicates that an AI@Edge computer is running the Waggle software stack.  It is similar to saying “It is a Linux Box”.  The Linux box could be running a web server or a database, but is running the core Linux software stack.  “A Waggle Node” runs the Waggle encrypted and reliable messaging layers, configuration system, resilience components, adheres to the Waggle security model, provides the AI@Edge runtime libraries, and provides the resource management components to schedule and run Edge docker containers from the Edge Code Repository.


## Software infrastructure

#### [Sage Core Services (SCS)](https://github.com/sagecontinuum/bic)
To deliver the Sage Cyberinfrastructure, a set of essential components and tools provide data APIs, authentication, and management services to the entire framework.  This includes: Storage & Storage API, Authorization Service, User Management and Authentication, Sage Continuous Integration, Public Streaming Service, and Sage Web Portal.

#### [Waggle Edge Stack (WES)](https://github.com/waggle-sensor/waggle-edge-stack)
The WES includes the operating system image and Waggle services running on the NC and EP as well as the ML run-time libraries and tools. It also manages cybersecurity, certificate management, and manages system resources, such as power, memory, and cores. It constantly updates its state with the cloud server to fetch and perform any task scheduled from SES.

#### [Sage Edge Scheduler (SES)](https://github.com/sagecontinuum/ses)
All configuration changes, whether they be software updates or new edge computing algorithms are handled by the SES. Users who have edge code already running and deployed on Waggle nodes can use their authentication token to push configuration changes to nodes via the SES. Users can also submit “jobs” that can be scheduled and run on nodes at a later time. The SES makes all configuration and system update decisions, and queues up changes that can be pushed out to nodes when they contact Beehive.

#### [Sage Lambda Triggers (SLT)](https://github.com/sagecontinuum/slt) <small className="muted">(in design)</small>
The SLT provides a framework for two kinds of triggers: From-Edge and To-Edge. A value or message from a Waggle edge node, delivered to Beehive, can be used to trigger a lambda function -- for example, if high wind velocity is detected, a function could be triggered to determine how to reconfigure sensors or launch a computation or send an alert. Similarly, an HPC calculation or cloud-based data analysis could trigger an API call to the SES and send a notification to a Waggle edge node -- for example to request scheduling of new edge computations or reposition mobile assets.

#### [Cloud Training Software Stack (CTSS)](https://github.com/sagecontinuum/ctss) <small className="muted">(in design)</small>
CTSS will provide interfaces (CTSS Training Environment and CTSS API Client) and documentation with end-to-end examples for users to allow them to build and bundle the components necessary to test on a Virtual Waggle and then on a Sage Node. It can be run on the cloud or as a downloadable software.


## Data

#### [Sage Data Repository (SDR)](https://github.com/waggle-sensor/waggle-beehive-v2)
Accessed via the [Sage Data API](docs/tutorials/accessing-data), Sage data is made open for research wherever possible.  Some training data sets may require data-usage agreements to adhere to privacy guidelines or for operational security.  However all sensor data and AI@Edge inference results are intended to be open and immediately shared in near-real time via the SDR. The SDR aggregates all data collected by Sage Nodes and provides web-based tools for extracting (slicing and dicing) relevant data components or viewing the data on map tools (previously known as BDR).

#### [Sage Object Store / Open Storage Network](https://github.com/sagecontinuum/sage)

The Sage Object Store API enables storing of larger objects (files), such as images, audio, and data sets.  When an object is stored via an ECR application, a reference to these files are kept in SDR and can be accessed via the [Object Store API](/docs/tutorials/accessing-data#accessing-large-files-ie-training-data).


## Edge Code Repository

#### [Edge Code Repository (ECR)](https://github.com/sagecontinuum/sage-ecr)
A library of tested and benchmarked AI@Edge codes that can run on the Waggle software stack.  The ECR provides a verified and versioned repository of AI@Edge docker images that can be pushed by the Beehive to Sage Nodes and executed.  [View public apps on portal](https://portal.sagecontinuum.org/apps/explore).


## Utilities

#### [Virtual Waggle (VW)](https://github.com/waggle-sensor/virtual-waggle)
Virtual Waggle is a downloadable software-only programming environment for building and testing edge computing code for the Waggle framework.

#### [Bench-top Waggle Driver (BWD)](https://github.com/sagecontinuum/bwd) <small className="muted">(in design)</small>
The BWD provides a remotely controllable interface to a physical Waggle node. The BWD will control as many physical attributes of the Waggle node as possible, including the serial console.  Ideally, almost everything that can be done physically, while a node sits on a desk, can be done remotely via the BWD.


## Support Infrastructure

#### [Beehive](https://github.com/waggle-sensor/waggle-beehive-v2)

Beehive is a cloud endpoint that offers several services for Waggle nodes and derivatives (AoT, Sage etc.)
including authentication, management, configuration, data aggregation and dissemination. Beehive is hosted
at Argonne National Laboratory.

#### [Beekeeper](https://github.com/sagecontinuum/beekeeper)

Beekeeper is the is an administrative cloud endpoint that all Sage nodes connect to allow Sage administrators to perform actions on the nodes such as gather health metrics, and perform software updates.
