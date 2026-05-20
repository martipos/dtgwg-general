# Decentralized Trust Graph Hybrid Interaction Architecture - Baseline

## Status

> **Version:** Draft baseline v0.1  
> **Date:** 2026-05-20  
> **Scope:** Contributor-facing architecture alignment document    
> **Editor:** [Martina Kolpondinos](https://github.com/martipos)    
> **Authority:** Informative, not a DTG specification   
> **Source basis:** DTG Glossary, DTG Credentials draft, First Person Project White Paper V1.2, DTG presentation deck, Trust Tasks draft, OpenVTC / Verifiable Trust Infrastructure implementation sources, DTG General - GitHub Discussion #8, and the most recent architecture diagram.  
> **Update policy:** Revise as glossary terms, credential specifications, implementation patterns, and governance decisions evolve.


This document is source-grounded, but it is a **working paper** and **not a final specification**.

## Table of Contents

- [Status](#status)
- [Purpose](#purpose)
- [Getting Familiar with the DTG Architecture](#getting-familiar-with-the-dtg-architecture)
  - [Terminology Note: “Layer”](#terminology-note-layer)
  - [Actor / Entity Layer](#actor--entity-layer)
  - [Human Experience / Access Layer](#human-experience--access-layer)
  - [Management Layer](#management-layer)
  - [Community and Network Layer](#community-and-network-layer)
  - [Standards and Protocol Layer](#standards-and-protocol-layer)
  - [Topology Layer](#topology-layer)
  - [Governance Layer](#governance-layer)
  - [Closing the Loop](#closing-the-loop)
- [DTG Architecture Layers: Overview & Status](#dtg-architecture-layers-overview--status)
- [DTG Architecture Core Components: Overview](#dtg-architecture-core-components-overview)
- [Key Interaction Patterns](#key-interaction-patterns)
- [Source Basis and Authority](#source-basis-and-authority)

*** 
*** 

## Purpose of this Content

This document provides a shared architecture baseline for contributors working on the Decentralized Trust Graph (DTG).

It is intended to support:

- DTG architecture work
- DTGWG task force work
- specification discussion
- terminology alignment
- governance discussion
- implementation alignment
- future diagram creation
- non-technical stakeholder onboarding

The goal is not to freeze the architecture. Instead, the goal is to **make current assumptions visible, distinguish stable components from open questions, and reduce confusion between actors, infrastructure, credentials, graph topology, governance, and implementation-specific choices**.



## Getting Familiar with the DTG Architecture

The DTG is not one central database of everyone’s relationships. It builds on decentralized trust infrastructure through which actors can control their own trust relationships and produce verifiable evidence about those relationships, including Proof of Personhood, when needed.
The DTG architecture can be understood through seven architecture layers. These are not protocol-stack layers. They are a way to separate the main parts of the system: who participates, how participants access and manage their DTG presence, what community and network infrastructure is involved, what identifiers, credentials, and protocols are used, how those elements are mapped into graph views, and how governance is applied.

### Core Mental Model

Before going through the seven layers, it helps to keep a simpler mental model in mind. The table below groups the architecture into six questions. These questions do not map one-to-one to the seven layers; they are a shortcut for understanding how the main parts fit together.

| Question | Architecture area |
|---|---|
| Who or what participates? | Actor / entity |
| How does the actor control or administer its DTG presence? | Access and management |
| How does that DTG presence become addressable and interactable? | VTA infrastructure |
| What provides verifiable evidence? | DIDs and credentials |
| How is that evidence mapped into graph form? | DTG topology |
| Who decides whether the evidence counts? | Governance |


### Terminology Note: “Layer”

As noted above, the seven DTG architecture layers are **not protocol-stack layers**.

Here, “layer” means a part of the architecture that is useful to examine separately while still showing how it depends on, or is interpreted through, other layers. For example, the Actor / Entity Layer focuses on who or what participates. The Management Layer shows the VTA infrastructure through which that participation becomes addressable. The Topology Layer then shows how DTG-relevant identifiers, credentials, and infrastructure are mapped into node and edge views.


Only the Standards and Protocol Layer should be read as protocol-oriented.


### Actor / Entity Layer

The first layer contains the real-world or logical participants that may have a DTG presence.

Core actor/entity types include:

- people
- communities
- devices
- AI agents


These actors exist independently of the DTG. 
A `DTG presence` is the actor’s operational presence in the DTG. It is not the actor itself, but the identifiers, VTA infrastructure, credentials, and governance context through which the actor can be addressed, verified, and involved in trust relationships. When such a presence is established, the actor has a corresponding DTG node in the DTG view. 

Relationships and memberships between those presences are evidenced by DTG credentials and may be mapped into the DTG edge view.

The control of a DTG presence can be sovereign, delegated, or custodial. These control modes help the architecture scale beyond people and communities to other actors such as AI agents, IoT devices, robots, sensors, and systems.

- **Sovereign:** the actor defines, controls, and maintains its own DTG presence, including policy decisions.
- **Delegated:** the actor authorizes another actor or agent to act on its behalf within explicitly granted permissions and constraints.
- **Custodial:** another actor operates or maintains the DTG presence, including policy constraints, without necessarily being the origin of identity or authority.


### Human Experience / Access Layer

The second layer is the human-facing or administration-facing access layer. It is where private individuals and community administrators interact with DTG infrastructure, typically through a mobile device, desktop application, browser, or other user-facing tool.

This layer can include:

- `Personal Network Manager (PNM)`
- `Community Network Manager (CNM)`
- `Personal Network Vaults (PNVs)` or wallets
- access devices such as smartphones, laptops, browsers, or admin consoles
- ceremony and consent interfaces

A `Personal Network Manager (PNM)` is used by an individual to manage trust relationships including, memberships, communication, and transactions.


A `Personal Network Manager (PNM)` is used by an individual to manage trust relationships, memberships, communication, transactions, and trust tasks.



A `Community Network Manager (CNM)` is used by people administering a community. For simple use cases, basic community management functions may be included in a person’s PNM to support quick community setup and management. For more advanced use cases, community administrators may use a dedicated CNM application to manage one or more communities.

A `Personal Network Vault (PNV)` is the secure vault, sometimes called a wallet, where a person stores DTG credentials and associated signing keys for the DTG verifiable identifiers associated with those credentials. A PNM may use or interact with a PNV, but the PNV is the vault or wallet component while the PNM is the management agent.

AI agents and other machine actors may not need a human-facing access layer, but they may still require vault, wallet, key-management, or authorization capabilities when they use credentials, sign messages, manage identifiers, or act under delegation. Depending on the implementation, they may interact directly with management-layer infrastructure when authorized.


### Management Layer

The third layer contains `Verifiable Trust Agents (VTAs)` and related management components.

A VTA is the infrastructure component through which a DTG presence can be reached and interacted with. An actor with a DTG presence is associated with a VTA or VTA network. The DTG presence is identified by one or more verifiable identifiers, such as DIDs, through which the relevant VTA endpoint can be discovered so other parties can find, verify, and interact with that presence. Depending on the implementation, the VTA may support routing, credential exchange, trust tasks, access control, and other interaction functions.

Common VTA distinctions include two different dimensions: where the VTA runs, and whose DTG presence it supports.

- `local VTA`: runs on a local or edge device, such as a phone, laptop, or other device close to the actor. It can support direct control, local interaction, and local key or credential handling depending on the implementation.
- `cloud VTA`: runs on network/server infrastructure. It can support availability, routing, queuing, notifications, and interactions that need to work even when a local device is offline.
- `personal VTA (pVTA)`: associated with an individual person’s DTG presence.
- `community VTA (cVTA)`: associated with a Verifiable Trust Community’s DTG presence.

A `VTA network` brings several VTAs together to support a DTG node or DTG presence. For example, a person may use a local VTA on a phone, another local VTA on a laptop, and a cloud VTA for availability. A community may use multiple VTAs to support shared administration or operational resilience. The DTG Glossary distinguishes personal VTA networks and community VTA networks, while the detailed model is still developing.


A PNM may use, control, coordinate with, or provide an interface to personal VTA infrastructure, depending on the implementation.

Together with the relevant identifiers and governance context, a DTG presence can be mapped into the DTG node view. Relationships and memberships between DTG presences are evidenced by credentials and can be mapped into the DTG edge view.

In some implementations, cloud VTAs may provide encrypted storage, backup and recovery, message queuing, routing, or other availability functions. This can be useful when a DTG presence needs high availability or when an authorized agent must act while a local device is offline. Whether wallet or vault functions remain local, are supported by cloud infrastructure, or are split across both is implementation-specific.


### Community and Network Layer

The fourth layer contains the community and network structures that give many DTG relationships their broader context.

The most important components are:

- `Verifiable Trust Community (VTC)`
- `Verifiable Trust Network (VTN)`
- community VTA infrastructure, where applicable
- trust registry infrastructure, where applicable
- `Verifiable Trust Service Provider (VTSP)` infrastructure, where applicable

A `Verifiable Trust Community (VTC)` is a governed community identified with a verifiable identifier. In the DTG architecture, the verifiable identifier for a VTC is a community DID (C-DID). A VTC can be formal or informal, public or private. Examples include organizations, open-source projects, professional communities, local communities, and other groups that define membership and trust policies.

Members of a VTC may include people, devices, AI agents, or other VTCs, depending on the community’s governance.

A VTC may use community VTA infrastructure to make the community’s DTG presence reachable and interactable. The VTA is not the community itself; it is the infrastructure through which the community’s DTG presence can be reached and managed. The community is identified by its C-DID, while the relevant VTA endpoint can be discovered through the DTG verifiable identifier associated with that community.

A `Verifiable Trust Network (VTN)` is a governed trust network whose members are VTCs. At this level, the focus is not only membership in a single community, but recognition across communities. A VTN can define trust anchors, recognition rules, and shared governance requirements.

Trust registry infrastructure may be used to make VTCs, VTN members, or trust anchors discoverable and verifiable. This is especially relevant for VTNs, where trust anchors and member VTCs may need to be checked across community boundaries.

Community and network infrastructure may be operated in different ways depending on the use case. Some communities may be small and lightweight, while others may require dedicated community VTAs, trust registry infrastructure, or support from a `Verifiable Trust Service Provider (VTSP)`.



### Standards and Protocol Layer

The fifth layer contains the technical building blocks that make DTG interactions verifiable and interoperable.

This layer includes:

- `Verifiable Identifiers (VIDs)`
- `Decentralized Identifiers (DIDs)` as one important type of VID
- DID-based identifiers such as R-DID, M-DID, C-DID, and P-DID
- keys, service endpoints, and related identifier metadata
- `DTG credentials`
- `Verifiable data Structures`
- `Trust Tasks`
- communication and trust protocols
- credential formats and cryptographic standards

The DTG specifications currently use DIDs for DTG verifiable identifiers (VIDs). A VID is the broader concept of a verifiable identifier. In the DTG architecture, a DTG VID is used to identify a DTG node. The glossary defines a DTG node as always being identified by at least one DTG VID and lists these four types of DTG DIDs: R-DID, M-DID, C-DID, and P-DID.

| DID / VID type | What it identifies | How it relates to DTG node mapping |
|---|---|---|
| R-DID | One party’s identifier in a specific peer-to-peer relationship context | Used in VRCs; relevant to relationship-specific node or edge mapping depending on the architecture/context |
| M-DID | A member in the context of a VTC | Can identify a member’s context within a VTC |
| C-DID | A Verifiable Trust Community | Most clearly maps to a VTC’s DTG node view |
| P-DID | A persona | Can identify a persona context that may be mapped into the DTG node view depending on the architecture/context |

Not every DID should be read as a standalone DTG node by itself. In this architecture, DIDs are used to identify relevant trust contexts, such as a relationship-specific party context, membership context, community, or persona. These identifiers help make DTG presences and relationships verifiable. The relevant VTA endpoint can be discovered through the DTG VID associated with the entity or context being interacted with.

DTG credentials provide verifiable evidence. The current credential baseline describes four functional categories:

- DTG edge credentials: VRC, VMC
- DTG invitation credentials: VIC
- DTG annotation credentials: VPC, VEC, VWC
- Verifiable Data Structures (VDSs): RCard

These categories are descriptive and help explain how the credential types function. They should not be treated as schema-level credential types unless the specification defines them that way.

`A Relationship Card (RCard)` should be treated as a verifiable data structure used for human-readable relationship data, not as a VRC.

`Trust Tasks` provide reusable interaction patterns for verifiable work between parties. They may coordinate private channel formation, credential issuance, credential presentation, verification, acceptance, rejection, revocation, or other bounded trust interactions.




### Topology Layer

The sixth layer is the graph view of verifiable trust relationships.

This layer includes:

- DTG node view
- DTG edge view
- relationship and membership edges


An actor or entity is not treated here as being mapped into the DTG as a raw real-world object. In this architecture model, the useful intermediate concept is the actor’s `DTG presence`: an identified, reachable, and verifiable presence in the DTG.

A DTG presence is identified by one or more DTG VIDs and made reachable through associated VTA infrastructure. The specific VID/DID and infrastructure pattern may differ by context and actor type.

In this document, `DTG presence`, `DTG node view`, and `DTG edge view` are explanatory architecture terms, not formal glossary terms. They are used to distinguish the real-world actor, the infrastructure through which the actor can be reached, and the graph-level topology interpretation.

A DTG node view is the graph-level view of an identified and reachable DTG presence. It should not be confused with the actor itself or with the VTA infrastructure used to reach that actor.

A DTG edge view is the graph-level view of a verifiable relationship between two DTG node views. Under the current credential baseline, VRC or VMC credential pairs may be mapped into DTG edge views.

Annotation credentials such as VPCs, VECs, and VWCs do not create new graph structure. They attach additional information, persona context, endorsement context, or witness evidence to an existing edge, party, or relationship context.


The topology layer should therefore be described with mapping language:

| Source | Relationship | Target |
|---|---|---|
| actor/entity | has or is associated with | DTG presence |
| DTG presence | identified by | DTG VID / DID appropriate to the trust context |
| DTG presence | reachable through | VTA / VTA network, depending on implementation |
| DTG presence | interpreted as | DTG node view |
| community DTG presence / VTC | identified by | DTG VID / DID, specifically C-DID |
| VTA / VTA network | provides infrastructure for | corresponding DTG presence |
| VRC or VMC credential pair | mapped to | DTG edge view |
| VPC / VEC / VWC | annotates | existing edge, party, or relationship context |



#### Simplified flow

> Actor / Entity  
> → has or is associated with  
> DTG presence  
> → identified by  
> DTG VID / DID  
> → reachable through  
> VTA / VTA network  
> → interpreted as  
> DTG node view

#### Examples

| Actor / Entity | Has or is associated with | Identified by | Reachable through | Interpreted as |
|---|---|---|---|---|
| Person | DTG presence | DTG VID / DID appropriate to the trust context | personal VTA / VTA network | DTG node view |
| Community | Verifiable Trust Community (VTC) / community DTG presence | DTG VID / DID, specifically C-DID | community VTA / community VTA network | DTG node view |
| Device | DTG presence | DTG VID / DID appropriate to the trust context | VTA / VTA network, depending on implementation | DTG node view |
| AI agent | DTG presence | DTG VID / DID appropriate to the trust context | VTA / VTA network, depending on implementation | DTG node view |


----

### Governance Layer

The seventh layer explains how technical trust becomes human trust in a specific community or network. Protocols can verify signatures, identifiers, and credential formats, but they cannot decide by themselves who is allowed to issue a credential, what counts as valid membership, which witnesses are accepted, or which trust anchors are recognized. Those decisions belong to governance.

Communities and networks define membership rules, trust anchors, credential acceptance rules, witness rules, revocation policies, and contextual meaning.

This layer includes:

- governance frameworks
- VTC governance
- VTN governance
- trust registries
- trust anchors
- `Policy Enforcement Points (PEPs)`
- membership policies
- credential acceptance policies
- revocation and status policies

A `Policy Enforcement Point (PEP)` is the policy engine for a VTC. It enforces the community’s policies for issuing and revoking DTG credentials.

Governance is part of the architecture because it determines whether technically valid credentials are accepted and useful in a given community or network.


### *Closing the Loop*

The previous layers describe the main actors, infrastructure, identifiers, credentials, topology, and governance structures of the DTG. What they do not fully capture is the human, social, and cultural context in which these exchanges happen. That is the role of ceremonies.

`Ceremonies` describe the human-meaningful exchange context around DTG credentials and trust tasks. They help explain not only whether something was technically exchanged, but whether the exchange was understood, accepted, witnessed, consented to, or recognized as meaningful within a specific community.

In other words, a DTG credential may be cryptographically valid and a trust task may technically be complete, while the broader ceremony may still be incomplete, socially unresolved, culturally invalid, or contested.

Ceremony concepts are important for usability, consent, witnessing, community participation, relationship meaning, and cultural interpretation. Different communities may attach different meanings, expectations, rituals, or legitimacy conditions to the same technical exchange.

This is why ceremony-specific structures such as ceremony IDs, ceremony profiles, completion receipts, cultural validity rules, and formal witness roles are treated as emerging architecture concepts for the DTG.



----

## DTG Architecture Layers: Overview & Status

Note: Terms such as `DTG presence`, `DTG node view`, and `DTG edge view` are explanatory architecture terms used in this document. They help distinguish real-world actors, operational infrastructure, and graph/topology interpretation. They should not be treated as formal DTG glossary terms unless adopted into the DTG specifications.

| Layer | Name | Purpose | Core Components | Status |
|---:|---|---|---|---|
| 1 | Actor / Entity | Real-world or logical participants | Person, community, device, AI agent | Stable concept; “entity” is stronger source wording; “actor” is useful architecture language |
| 2 | Human Experience / Access | Human or community-facing control surface | PNM, CNM, wallet/PNV, access device, ceremony/consent interface | PNM concept stable but wording needs alignment; CNM useful but needs formal definition; UX patterns are implementation-specific and underdeveloped |
| 3 | Management | Management infrastructure for DTG interactions | VTA, pVTA, cVTA, local VTA, cloud VTA, VTA network; wallet/PNV integration is implementation-specific | Stable at conceptual level; implementation patterns vary |
| 4 | Community and Network | Community and network structures that provide context for DTG relationships | VTC, VTN, VTSP, trust registry infrastructure where applicable | Stable at conceptual level; implementation patterns vary |
| 5 | Standards and Protocols | Technical standards and data structures for verifiable interaction | VID/DID (R-DID, M-DID, C-DID, P-DID), DTG credentials (VRC, VMC, VIC, VPC, VEC, VWC), RCard/VDS, Trust Tasks, TSP, TRQP, DIDComm, VC formats, ZKPs | DIDs and DTG credentials mostly stable drafts; Trust Tasks being developed; protocol integration varies by implementation |
| 6 | Topology | Graph view of verifiable trust relationships | DTG node view, DTG edge view, relationship and membership edges | Stable concept; “node view” and “edge view” are explanatory architecture terms |
| 7 | Governance | Defines what counts and who is trusted | Governance framework, trust registry, trust anchors, PEP, VTC governance, VTN governance | Stable concept; concrete policies vary |


## DTG Architecture Core Components: Overview

| Component | Plain-language explanation | Technical role | Source authority | Status | Notes |
|---|---|---|---|---|---|
| Actor / Entity | A participant in the world or system | Source of control, participation, or authority | Glossary for “entity”; architecture interpretation for “actor” | Stable concept; wording needs alignment | “Entity” is stronger source wording; “actor” is useful and may be more widely understood but is less formal |
| Person | Human actor | Can control DTG presence and credentials | Glossary / deck | Stable | May hold PHCs, VRCs, VMCs, etc. |
| Community | Group or collective context | Can become a VTC when identified and governed | Glossary | Stable | Formal DTG term should usually be VTC once the community has a DTG presence |
| Device | Technical object that may be an actor | May be mapped to DTG node view if it has DTG presence | Glossary / deck | Stable | Separate from access device |
| AI Agent | Software agent that may be an actor, delegate, or tool | May have its own DTG presence, act on behalf of another actor, or assist without independent DTG standing | Glossary / deck | Stable as node type; roles need care | Do not collapse all AI roles |
| DTG node | Source term for an entity participating in DTG trust relationships | Used in topology and relationship reasoning | Glossary | Stable | In this architecture model, treated as the graph-level view of a DTG presence; do not equate it with the actor or VTA |
| DTG edge | Verifiable trust relationship between DTG nodes | Graph-level relationship view supported by relationship or membership credential evidence | Glossary / credentials draft | Stable | Credential pairs may map to edge views under the current credential baseline |
| VTA | Verifiable Trust Agent | Digital agent / infrastructure through which a DTG node or DTG presence can be reached and interacted with | Glossary | Stable | VTA is infrastructure, not the actor itself |
| local VTA | VTA running on local/edge device | Edge-side agent capability | Glossary | Stable | May overlap with local user-facing tools depending on deployment |
| cloud VTA | VTA running on network server | Availability, routing, task handling | Glossary | Stable | May be hosted by VTSP |
| PNM | Personal Network Manager | Individual-facing trust relationship and task manager | Architecture baseline; glossary wording needs correction | Stable concept; wording needs alignment | More than a wallet; do not collapse PNM into VTA |
| CNM | Community Network Manager | Community-facing management/admin interface | Deck / architecture baseline | Supported but less formal | Should be added to glossary/spec if adopted |
| PNV | Personal Network Vault | Secure storage for a person’s DTG credentials and associated signing keys | Glossary | Stable | Sometimes called a wallet; distinct from PNM |
| VTA network | Set of VTAs used by one or more controllers to control a DTG node / DTG presence | Multi-VTA support for one DTG node or presence | Glossary | Stable but details open | Glossary indicates TODO for more detail |
| VTC | Verifiable Trust Community | Governed community identified by VID / C-DID | Glossary | Stable | Not a “container” unless implementation-specific |
| VTN | Verifiable Trust Network | Network of VTCs under governance | Glossary | Stable | Trust anchors often discoverable through trust registry |
| VTSP | Verifiable Trust Service Provider offering trust infrastructure or services | May provision local VTAs, host cloud VTAs, operate trust registries, and support routing, queuing, and notifications | DTG Glossary | Stable | Optional service-provider role; should be shown as external or supporting infrastructure, not as a required DTG component |
| VID / DID | Verifiable identifier / decentralized identifier | Cryptographic identifier and endpoint discovery basis | Glossary / Trust Tasks | Stable | DID is the primary VID type used in DTG sources |
| R-DID | Relationship DID | Pairwise relationship identifier | Glossary / credentials draft | Stable | Used for privacy-preserving relationship context |
| M-DID | Membership DID | Identifier for membership context | Glossary | Stable | Used in VMC and sometimes VRC contexts |
| C-DID | Community DID | Identifier for VTC | Glossary | Stable | Core to VTC/VMC architecture |
| P-DID | Persona DID | Identifier for intentional correlation / persona | Glossary | Stable | Used in persona credentials |
| DTG credential | Verifiable credential used in DTG | Parent credential concept | Glossary / credentials draft | Stable draft | Formal hierarchy controlled by credentials draft |
| DTG edge credential | Credential used to establish graph structure | VRC or VMC | Glossary / credentials draft | Stable draft | Directionality controlled by credentials draft |
| DTG annotation credential | Credential that annotates an existing edge | VPC, VEC, VWC | Glossary / credentials draft | Stable draft | Does not create new graph structure |
| DTG invitation credential | Credential used to bootstrap onboarding | VIC | Glossary / credentials draft | Stable draft | Use “Invitation,” not “Initiation” |
| VRC | Verifiable Relationship Credential | Peer-to-peer relationship evidence | Credentials draft | Stable draft | Current credential draft treats a complete VRC-based edge as bidirectional / paired; glossary also describes a VRC as one half of a bidirectional relationship |
| VMC | Verifiable Membership Credential | Membership evidence | Glossary / credentials draft | Stable draft | PHC can be a VMC use case/profile under governance |
| VWC | Verifiable Witness Credential | Witness assertion about an edge | Glossary / credentials draft | Stable draft; social semantics emerging | Witness roles need more work |
| VPC | Verifiable Persona Credential | Persona linked to relationship context | Glossary / credentials draft | Stable draft | Supports intentional correlation |
| VEC | Verifiable Endorsement Credential | Endorsement / reputation assertion | Glossary / credentials draft | Stable draft | Vocabulary likely community/network-specific |
| PHC | Personhood Credential | Proof-of-personhood use case | Glossary / white paper | Stable concept | In DTG, should be treated as VMC profile/use case unless spec changes |
| R-Card / RCard | Human-readable signed relationship data | Verifiable data structure | Glossary / credentials draft | Stable draft | Not a VRC |
| Trust Task | Reusable verifiable interaction pattern | Transport-agnostic interaction framework | Trust Tasks draft | Draft / emerging | Not yet endorsed by DTGWG as a whole |
| TSP | Trust Spanning Protocol | ToIP spanning layer for authentic/confidential communication | White paper / ToIP | Stable ToIP-level component | External protocol dependency |
| TRQP | Trust Registry Query Protocol | Trust registry query mechanism | White paper / ToIP | Stable ToIP-level component | Used for governance/trust registry checks |
| PEP | Policy Enforcement Point for a Verifiable Trust Community | Enforces the community’s policies for issuing and revoking DTG credentials | DTG Glossary | Stable | Belongs in the governance / ecosystem layer; should be shown near VTC governance, membership policy, credential policy, and revocation/status policy |
| Trust registry | Governed machine-readable list of trusted roles/entities | Authorization and ecosystem discovery | Glossary / white paper | Stable concept | Important governance component |
| Governance framework | Rules defining who can issue, verify, accept, or trust | Policy layer | White paper / glossary | Stable concept | Must not be hidden in technical layer |
| OpenVTC / VTI | Concrete implementation stack | VTA/VTC service implementation | OpenVTC repo | Implementation-specific | Useful example, not normative DTG terminology |

## Key Interaction Patterns

| Pattern | Summary |
|---|---|
| Person controls a DTG presence | A person uses a PNM, wallet/PNV, access device, and VTA infrastructure to manage identifiers, credentials, trust tasks, and verifiable trust relationships. The person is not the DTG node directly; their DTG presence is interpreted in the DTG node view through identifiers, VTA infrastructure, and credential evidence. |
| Community controls a DTG presence | A community becomes a VTC when identified and governed as a DTG presence. A VTC uses governance, a C-DID, community VTA infrastructure, membership policies, and VMC relationships to manage community membership and trust context. A CNM may provide the community-facing administration interface. |
| PNM / CNM / VTA relationship | A PNM or CNM provides the control and administration surface. A VTA or VTA network provides addressable infrastructure for DTG interactions. The access manager controls, uses, or coordinates with the VTA, depending on implementation. |
| Local VTA and cloud VTA coordination | A local VTA may operate at the edge, such as on a smartphone or laptop, while a cloud VTA may provide availability, routing, queuing, or server-side interaction support. Together they may form part of a VTA network for one DTG presence. |
| DTG node view formation | An actor’s DTG presence is interpreted in the DTG node view through VIDs/DIDs, keys, endpoints, VTA infrastructure, and governance context. This mapping should not be described as the actor or VTA “being” the node. |
| DTG edge view formation | A DTG edge view is formed from verifiable relationship or membership evidence between two DTG node views. Under the current credential baseline, a VRC or VMC pair may be mapped into a DTG edge view. |
| VRC exchange | Two parties exchange Verifiable Relationship Credentials, typically one in each direction, to provide verifiable evidence of a peer-to-peer relationship. The resulting credential pair may be mapped into the DTG edge view. |
| VMC exchange | A Verifiable Trust Community issues membership evidence using Verifiable Membership Credentials. VMCs connect a member context with a community context and may support membership, personhood, or other governance-defined claims. Agenthood is shown in explanatory material but should be treated as emerging unless specified. |
| PHC as VMC profile | A Personhood Credential should be shown as a VMC profile or use case under governance, not as a standalone DTG credential type, unless the credential specification changes. Its meaning depends on the VTC governance rules that define uniqueness and eligibility. |
| VWC / witness flow | A Verifiable Witness Credential can annotate an existing DTG edge by providing witness evidence about the authenticity or context of a relationship. The credential type is part of the credential baseline, while the social meaning of witness roles remains an emerging design area. |
| VPC / persona flow | A Verifiable Persona Credential can annotate a relationship with persona information, allowing an actor to manage intentional correlation across contexts. Persona-related identifiers should remain distinct from relationship-specific identifiers. |
| VEC / endorsement flow | A Verifiable Endorsement Credential can annotate an existing relationship with contextual claims, endorsements, or reputation-related assertions. Its meaning depends on the vocabulary and governance context in which the endorsement is interpreted. |
| RCard exchange | A Relationship Card is exchanged as a Verifiable Data Structure to provide human-readable relationship or contact information. It should be shown as a VDS, not as a VRC. |
| Private channel formation | Two parties establish a private channel using pairwise identifiers, keys, endpoints, and agent/VTA-mediated communication, depending on implementation. This private channel can then support trust tasks, credential exchange, RCard exchange, and ongoing secure interaction. |
| Trust Task execution | A trust task defines, or is intended to define, a reusable interaction pattern for verifiable work between parties. It may orchestrate private channel use, credential issuance, credential presentation, verification, acceptance, rejection, or other bounded trust interactions. Status: draft / emerging unless adopted by DTGWG. |
| Trust registry / VTN governance check | A verifier, VTC, or VTN may query a trust registry to determine whether an issuer, VTC, trust anchor, or governance context is recognized. This check helps determine whether a technically valid credential is meaningful in a given ecosystem. |
| AI agent as actor | An AI agent may have its own DTG presence and be mapped into the DTG node view through its identifiers, VTA infrastructure, credentials, and governance context. |
| AI agent as delegate | An AI agent may act on behalf of a person, organization, community, or other actor. In this case, the critical architectural question is what authorization, delegation credential, policy, or relationship evidence constrains the AI agent’s authority. |
| AI agent as tool | An AI agent may assist a person or organization without having independent DTG standing. In this role, it should be treated as part of the application or human experience layer rather than as a separate DTG actor. |
| Device actor participation | A device, robot, sensor, system, or other technical object may participate as a DTG actor if it has its own DTG presence, identifiers, VTA infrastructure, and credential relationships. |
| Access device use | A smartphone, laptop, browser, or desktop may simply serve as an access device for a person, PNM, wallet, or local VTA. It should not automatically be shown as a DTG actor unless it has its own DTG presence. |
| Ceremony-level exchange | Ceremony-level exchange is an emerging socio-technical architecture concept. A broader ceremony may combine private channel formation, credential exchange, witness flow, RCard exchange, consent, community policy, and completion evidence. A ceremony can remain incomplete or socially unresolved even when individual credentials are valid and individual trust tasks technically complete. |

---

## Source Basis and Authority

The source hierarchy used for this baseline is:

1. **DTG Glossary and TF specifications** — strongest authority for terminology and formal claims
2. **First Person Project (FPP) White Paper** — conceptual, strategic, and ecosystem-level context
3. **DTG presentation deck** — explanatory and conceptual; not formal specification unless aligned with glossary/specs
4. **GitHub discussions** — emerging design discussion unless reflected in specifications
5. **OpenVTC / Verifiable Trust Infrastructure** — implementation-specific evidence
6. **Most recent architecture diagram** — current visual representation of synthesized information; not a source of truth

| Source | Type | Authority | Version / Date | Notes |
|---|---|---:|---|---|
| [DTG Glossary](https://lf-toip.atlassian.net/wiki/spaces/HOME/pages/442073089/DTG+Glossary) | Terminology working document | High | 2026-01-24 | Defines DTG, DTG node, DTG edge, VTA, VTC, VTN, PNM, credential terms, DIDs, and related terminology. It is still a draft working document. |
| [DTG Credentials draft](https://github.com/trustoverip/dtgwg-cred-tf/blob/main/dtg.md) | Specification draft | High for credential claims | Early Draft v0.3 | Defines DTG credential categories, VRC/VMC directionality, VIC, VPC, VEC, VWC, and RCard/VDS status. Under ongoing development and review. |
| [FPP White Paper](https://www.firstperson.network/white-paper) | Conceptual / ecosystem paper | Medium-high | 2026-01-23 | __V1.2:__ Explains why PHCs, VRCs, governance, FPN, AI agents, and DTG matter. It explicitly frames the work as a trust layer and a living document. |
| [DTG presentation deck](https://docs.google.com/presentation/d/1jLHl1k7wsmwvEoSi-KLX-aMJEitg0_zFTsH_zW-9EsE/edit?slide=id.g10d40b945bc_2_24#slide=id.g10d40b945bc_2_24) | Explanatory deck | Medium | 2026-05-11 | Useful for the narrative: people, devices, AI agents, VTCs, PNM/CNM, VTAs, VMCs, VRCs, and VTNs. |
| [Trust Tasks draft](https://github.com/martipos/dtgwg-trust-tasks-tf/blob/main/SPEC.md) | Specification draft | Medium-high for Trust Task framework | 2026-05-18, document version 0.1 | Defines Trust Tasks as transport-agnostic descriptions of outcomes between parties; not yet endorsed as a WG deliverable. |
| [OpenVTC / Verifiable Trust Infrastructure](https://github.com/OpenVTC/verifiable-trust-infrastructure) | Implementation repository | Implementation-specific | Current GitHub view, reviewed 2026-05-19 | Rust workspace implementing VTA and VTC service backends, including CLIs, SDKs, and shared crates. It is not DTG terminology authority. |
| [OpenVTC VTC MVP design note](https://github.com/OpenVTC/verifiable-trust-infrastructure/blob/main/docs/05-design-notes/vtc-mvp.md) | Implementation design note | Implementation-specific | Current GitHub view, reviewed 2026-05-19 | Describes VTC setup flows and VTA-driven key authority for that implementation. |
| [GitHub DTGWG General Discussion](https://github.com/trustoverip/dtgwg-general/discussions/8) | Emerging design discussion | medium | Started 2026-04-28 | [Socio-Technical] Architecting socio-technical ceremonies for consensual and reliable multi-part and multi-party credential exchange: Explores ceremony, witness, multi-part credential exchange, and social/technical dimensions. Not settled architecture. |
| [Latest architecture diagram](https://miro.com/app/board/uXjVGoW5EIY=/?share_link_id=64257663661) | Visual artifact | medium-high, depends on TF developments | Uploaded 2026-05-19 | DTG - Layered Component+ Architecture - V1: Support understanding the current architectural landscape. Contains useful structure. Is currently a draft and will be updated to show the latest developments. |

---