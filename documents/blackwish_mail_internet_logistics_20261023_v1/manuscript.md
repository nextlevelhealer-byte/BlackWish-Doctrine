# Blackwish Protocol Mail Internet and Related Delivery Services

Research reference dated 23 October 2026 UTC

NEW RESEARCH / REVIEWED / NOT RATIFIEDREVIEWED means internal source and consistency desk review. It does not mean operational certification, legal approval, empirical validation, canonical adoption or authorization to deploy.

Delivery is a chain of bounded handoffs, not one universal success event. A parcel can reach a building without reaching its resident; an email can reach a mailbox without being read; an API can commit a change while its reply is lost. The central question is what reached which boundary, according to whose evidence, under which service terms.

This reference follows physical mail from preparation through collection, sorting, transport, last mile and exceptions; follows Internet services through infrastructure, naming, routing, transport, security and applications; then compares receipts, retries, custody, access and recovery. It supplies synthetic traces and a reusable evidence record for Blackwish text analysis.

## Scope and navigation

Pages 2-5 explain physical delivery and evidence. Pages 6-10 explain Internet and related services. Pages 11-14 provide examples, a reusable record and operational questions. Pages 15-17 contain three scoped Zen reviews, a bounded Death Knell audit and source-status limits. Pages 18-20 provide the source register.

The postal baseline is United States USPS, with separately qualified international architecture. Digital standards have international use, but operator implementations, terms and legal duties vary. This is not a tariff catalogue, shipment instruction, network configuration, account audit or performance study.

This additive artifact changes no canonical Blackwish text and reports no real shipment, account action, communication, purchase, network change or experiment on people. Proposed revisions remain subject to explicit manual ratification. No deployment or real-world action is authorized by this reference.

# Separate the object from the claim

A shared vocabulary helps compare systems without pretending that mail and packets are the same thing. The distinctions below are analytical conclusions drawn from the service and protocol evidence, not a new universal delivery standard. [P02-P05, I03, I08-I11]

Separate concept | Question to preserve
Address or name | Where is an object or request directed? This is not necessarily a person, current location or permission.
Route and reachability | Which path can the service use now? Does policy, capacity or an outage change it?
Identity and authorization | Who is identified, and what action may that party perform? Authentication alone grants no universal authority.
Custody and storage | Who possesses the physical item, or which service has accepted responsibility for a digital copy?
Delivery and use | Which boundary was reached? Was the object retrieved, processed, displayed, read or acted on?
Ownership and consent | What separate evidence supports ownership or consent? Neither follows simply from delivery.

## Useful analogy and its stopping point

Collection points, sorting centres and relays all aggregate work. Addresses and names help select destinations. Receipts expose selected events, and exception queues prevent one failure from blocking every item. These are useful comparisons at the level of roles and handoffs.

The analogy fails when it hides copying. A letter is ordinarily one physical object; digital services can fragment, copy, cache, retransmit and deliver to several consumers. A packet acknowledgement is not a signature, and a signature is not proof of comprehension. Public tracking is not continuous GPS; DNS is not the physical route. [P02, I03-I05]

Writing rule: replace an unqualified statement such as "it was delivered" with a named object, receiver boundary, event, time and evidence source. Preserve a recipient non-receipt report even when a carrier or server records success. Conflicting observations are evidence to investigate, not permission to erase one side.

# Physical mail from preparation to last mile

Sender preparation determines whether later automation can work. Check mailable contents, packaging, sealing, readable addressing, unit information, weight and size, postage and service eligibility. A return address supports exception handling. Address standardization improves machine usability; it does not independently verify a resident. [P01]

Conceptual stage | Work and handoff
Collection or acceptance | An eligible counter, collection point or pickup brings the item into the operator network. A printed label or tracking number alone is not physical acceptance.
Origin processing | Read addresses and identifiers; separate formats; sort and consolidate into transportable units.
Transport and re sorting | Move through line-haul and intermediate or destination facilities according to the operator network and capacity.
Delivery unit and round | Prepare local sequence, load the round and attempt an eligible final handoff.
Completion or exception | Deliver to an allowed receptacle or receiver, or retain custody while following a notice, hold, redelivery or return process.

This is a teaching model, not a claim that every item visits every stage or follows the shortest geographic path. Barcodes can identify destinations, items, extra services or aggregates. A container movement is therefore not automatically an individually observed scan of every item inside it. [P02]

## The final boundary matters

An apartment mailbox, building mailroom, parcel locker, PO Box and individual receiver are different endpoints. A carrier handoff may be followed by separate household or building distribution. Oversized PO Box items may require counter collection or an available locker. Hours and equipment vary. [P03]

Private-carrier access is not inherent in a PO Box number: participating Street Addressing arrangements have their own terms. A carrier partner handing an item to USPS is a different arrangement. Signature on File is a limited opt-in and excludes specified services, including Registered Mail, Certified Mail, hardcopy Return Receipt and Restricted Delivery. [P03]

# Exceptions returns and international exchange

A failed attempt is not necessarily a lost item. An unavailable required signer, inaccessible receptacle, full locker or lack of a suitable placement can leave the item in carrier custody. Follow the actual notice and service rules; there is no universal attempt count, holding period or redelivery entitlement. [P06]

## Different changes solve different problems

Hold pauses eligible delivery at an existing address. Forwarding reroutes eligible mail and does not update every sender database. Intercept is an eligible, authorized request before relevant cutoffs, not guaranteed recall. Retail USPS Intercept options differ from commercial redirection options. No such request is made here. [P07]

Undeliverable mail may be forwarded, returned or handled under dead-mail rules depending on class, endorsements and circumstances. A missing-mail search, service refund request and insurance claim are different processes. Preserve relevant receipts, value evidence, damaged contents and packaging; deadlines and inspection requirements vary. Neither a search nor a claim guarantees recovery or payment. [P06, P08]

## International delivery adds boundaries

International post can involve origin and destination operators, exchange offices, transit operators, transport providers and customs. UPU guidance distinguishes an item, a receptacle such as a bag, a dispatch between exchange offices, and a consignment assigned to transport. These units need not remain together. UPU coordination does not make one worldwide carrier with identical promises. [P09]

Goods may need customs declarations and electronic advance data. Specific descriptions, admissibility review, assessment and release are separate from final delivery. Document-only correspondence and merchandise need not have the same requirements. Postal and commercial courier clearance are not identical. Actual country and content rules control. [P09, P10]

A tracking gap does not establish customs seizure. CBP cautions that it cannot track packages and that a seller description of "with customs" may be inaccurate. Preserve the distinction between a carrier handling clearance and an authority actually detaining goods. [P10]

# Service promises custody and proof

Choose the control for the question it answers. The following are USPS definitions, not universal meanings for similarly named products elsewhere. Eligibility, exclusions, evidence and deadlines still apply. [P04, P05]

Control | Contribution and limit
Tracking | Selected movement, attempt and delivery events; not continuous location, opening or ownership evidence.
Certified Mail | Mailing receipt and delivery or attempt verification, with a retained signature record. It is not itself insurance or secure Registered handling.
Registered Mail | Enhanced secure handling and a receipt chain, with delivery signature. The service alone does not provide public facility-to-facility en-route tracking; security can slow transit.
Return Receipt | Eligible access to a signature-containing delivery record. Distinct from Certified Mail, insurance and restricted delivery.
Restricted Delivery | An additional addressee or authorized-agent restriction under applicable terms; not implied by an ordinary signature.
Insurance | Potential compensation for covered loss or damage with required evidence. Not prevention of loss or a delivery-time guarantee.
Time commitment | Priority Mail Express has qualifying date-specific money-back terms and exceptions. Route, acceptance and drop-off timing matter; it is not universally overnight.

## The evidentiary ceiling

A signature may belong to an authorized receiving agent. A delivery scan records the operator event, not a complete history of later possession. Neither proves that the addressee opened the package, accepted its assertions, owns its contents or can safely use them. Those conclusions require separate evidence.

A service estimate is planning information; a guarantee is a contractual promise with a defined remedy. A remedy may be compensation rather than successful delivery. Likewise, a digital SLA service credit is not proof of restored data. Do not silently turn either remedy into an assurance that failure cannot happen. [P05, R05]

# Internet infrastructure naming and routing

The Internet is a network of independently operated networks. A typical journey crosses a device and access network, aggregation and backbone links, interconnection and a destination network. Fibre, copper, coaxial cable, terrestrial radio and satellite can participate. Wireless access does not make the whole path wireless. [I01]

Physical logistics remain: power, cooling, buildings, spare equipment, crews, permits and repairs. Submarine cable resilience includes landing sites and repair-vessel availability. Two logical routes may still share a vulnerable physical corridor. Data-centre redundancy is an engineering control, not evidence that every application has independent failure domains. [I01, I02]

## Interconnection is not a single global dispatch desk

Transit buys broader reachability through another network; peering exchanges agreed traffic. Public peering can use an Internet exchange point, while private peering uses dedicated links. An IXP route server helps exchange route information and normally does not carry the user traffic. Peering is not automatically access to every destination. [I02]

Layer or function | What it does and does not do
DNS | A resolver uses cached data or follows delegation to authoritative answers. Records can identify addresses or mail exchangers. DNS lookup is not the subsequent packet path.
IP routing | Reachability and policy determine routes. BGP exchanges prefixes and path information between autonomous systems; best path need not mean shortest distance.
Packet forwarding | Routers apply next-hop information to packets. Outward and return paths can differ; paths can change during faults or policy changes.

DNS cache lifetime is not an IP hop limit. IPv4 TTL is decremented in forwarding and operates principally as a hop limit; IPv6 explicitly has a Hop Limit. These prevent indefinite circulation, not missed wall-clock delivery deadlines. Basic packet service must tolerate drops, reordering and duplication. [I03, I04]

An IP address is not necessarily a person, a permanent physical location or an authorization credential. Reaching an endpoint establishes neither permission to use its data nor the honesty of its operator. [I03]

# Transport security and application meaning

TCP provides a reliable ordered byte stream using sequencing, acknowledgements, retransmission and flow control; congestion control manages network pressure. A transport acknowledgement is not proof that the application committed a change to durable storage. Reliability still depends on a usable connection. [I05]

QUIC provides secure multiplexed streams over UDP with loss recovery and congestion control; connection identifiers support migration between paths. HTTP/3 carries HTTP semantics over QUIC. Transport reliability does not itself make application effects happen exactly once. [I05]

## Name the protected channel endpoints

TLS protects a channel between its endpoints against eavesdropping and undetected modification, with authentication under application identity rules. A CDN or proxy terminating TLS is an endpoint of that channel. This is not proof that no intermediary sees content, that stored copies are end-to-end encrypted, or that the operator is trustworthy. [I06]

Current-status correction: RFC 9846 replaces RFC 8446 as the TLS 1.3 specification. It is a backward-compatible minor revision that retains the version number 1.3, not a new version named TLS 1.4. RFC publication status does not establish what a particular deployed service supports. [I06]

## HTTP adds a separate semantic boundary

HTTP requests and responses describe application operations. A 202 Accepted response does not establish finished processing. Idempotence concerns the intended effect of repeating a request, not identical response bytes. A timeout can occur after a remote effect succeeds, so arbitrary POST requests cannot safely be repeated merely because the client saw no reply. [I07]

The useful evidence ladder is therefore: reachable address, established transport, authenticated channel, accepted request, durable application outcome, and any later human action. Each step needs its own observation. Success lower in the stack cannot silently satisfy a higher step.

This reference describes properties and failure models, not configuration commands, cryptographic parameter selection or deployment instructions. Exact implementation guidance must include relevant updates, errata, application rules and provider support.

# Email is store and forward

Email usually passes from submission through mail transfer agents to a mailbox service. DNS MX records guide receiving-server selection. SMTP envelope recipients and displayed message headers are different information; forwarding and mailing lists can add further handoffs. [I08]

A successful SMTP response after the complete message data transfers responsibility for delivery or appropriate failure reporting. Temporary failures usually mean queuing and retry; permanent failures or exhausted retries may produce a non-delivery report. If the connection fails near final acceptance, uncertainty can lead to duplicates. Acceptance is not proof of mailbox placement, reading or agreement. [I08]

## Receipts answer different questions

Delivery-status notifications concern delivery outcomes. Message-disposition notifications concern later handling and may be suppressed for privacy. Even a displayed disposition does not guarantee that a person read or understood the content. Absence of a bounce or receipt is not decisive evidence of either success or failure. [I08, I09]

Authentication tool | Bounded claim
SPF | Whether a sending host is authorized to use a domain in specified SMTP identities; not the identity or intent of a human author.
DKIM | A signing domain is associated with validated signed message material; signer and purported author need not be the same.
DMARC | SPF or DKIM outcomes are considered with alignment to the author domain and domain handling/reporting preferences. Passing does not certify safe content or guarantee inbox placement.

None of SPF, DKIM or DMARC encrypts message content. Hop-by-hop transport encryption and end-to-end content encryption have different boundaries. A message can authenticate correctly yet contain a scam or an unsafe attachment. [I10, I11]

Current-status correction: RFC 7489 is obsolete. RFC 9989 supplies the current DMARC core, with aggregate reporting in RFC 9990 and failure reporting in RFC 9991. Failure reports can disclose headers or content containing personal data; requesting or generating them requires privacy consideration. [I11]

# Copies queues messaging and notifications

Digital delivery often creates durable or temporary copies. HTTP caches use freshness rules, validators and revalidation, and some conditions permit stale responses. Updating an origin, changing DNS and invalidating a CDN cache are different operations. Private responses need appropriate shared-cache treatment. [I07]

Do not label all cloud storage eventually consistent. S3 documents strong read-after-write consistency for object PUT and DELETE operations, while some configuration changes are eventually consistent. Object consistency, replication, cache freshness, durability and availability are distinct properties; one strong read does not make every downstream consumer current. [R01]

## A queue separates acceptance from completion

A producer, broker and consumer can acknowledge different boundaries. In SQS, an unremoved message can become visible again after a visibility timeout; standard-queue consumers must tolerate duplicates. Removal is not automatically atomic with a downstream side effect. At-least-once delivery therefore requires duplicate-safe processing, not the assumption of exactly-once business action. [R01]

## Provider status names are contracts

Twilio distinguishes queued, sent and delivered. Sent means acceptance by the upstream carrier; delivered reflects confirmation from the carrier and, where available, the handset. Read status belongs to supported channels such as WhatsApp and RCS, not ordinary SMS. A read receipt still does not establish comprehension or consent. [R02]

Firebase states that a returned message ID means acceptance for delivery, not device delivery. Offline devices, expiration and collapse behavior can delay, discard or replace notifications. A push alert should not be the sole authoritative record of a consequential state change. [R02]

Webhooks can arrive repeatedly or out of order. An analytical design recommendation is to authenticate intake, correlate event identifiers, durably record accepted responsibility and reconcile with authoritative state. A request identifier prevents duplicates only when the service defines deduplication semantics for it. Stripe supplies one operator example, not an Internet-wide rule. [R03]

# Failure handling without false certainty

A timeout says the observer did not receive an expected result in time. It does not, by itself, say whether the remote action occurred. A stale tracking page, delayed email notification and lost API reply are different forms of incomplete observation. Model the unknown rather than converting it into failure or success.

Observed condition | Reasonable analytical next question
No acceptance evidence | Was only a label or request prepared, or did a responsible service accept it?
Accepted but delayed | Which queue or custodian owns the next transition, and what timeout or retention rule applies?
Reply missing after action | Can authoritative state establish the outcome before a retry creates a duplicate effect?
Conflicting success and non receipt | Are the boundary, identity, timestamp and evidence source actually the same?
Repeated or unordered events | Is this a repeated observation, redelivery, or genuinely new intended action?
Terminal rejection or expiry | What authorized return, correction, cancellation or disposal path exists?

## Bound retries by meaning

A retry policy needs an owner, a reason, a duplicate-risk assessment and a stopping condition. Backoff and a retry budget can reduce overload, but do not repair an invalid address or grant missing authority. An idempotency record needs a defined operation scope, parameter binding, concurrency behavior and retention covering the intended retry horizon. This is a design consideration, not an implemented guarantee. [I07, R01, R03]

Reconciliation compares event history with the authoritative current result. Recovery may mean finding a parcel, correcting permitted documentation, recovering data, accepting a failed delivery or escalating an unresolved discrepancy. A new shipment or repeated business operation is not automatically the first remedy.

Termination is explicit: delivered to the defined boundary, returned, rejected, expired, canceled, safely disposed under applicable authority, or unresolved with a named owner. "No new update" is an observation, not necessarily a terminal state.

# Synthetic physical delivery traces

These are invented desk-analysis examples, not observed shipments. Times and identifiers are illustrative and carry no delivery promise. The traces exercise the distinctions supported by USPS and UPU guidance. [P02, P06, P09, P10]

## Trace A Apartment access failure

Illustrative event | State and evidentiary limit
Day 1 09 00 Label created | Prepared. No physical acceptance is yet established.
Day 1 15 00 Operator acceptance | Accepted into custody. The correct unit address does not prove final access.
Day 2 Processing and transport | In transit. Selected scans are not a continuous location feed.
Day 3 Delivery attempt | Suitable secure placement is unavailable. Notice and retained custody replace delivery.
Day 4 Authorized collection | Handoff to an eligible receiver. Opening, comprehension and ownership remain unproved.

The repair addresses access, not postcode spelling. If a delivered scan appears but the resident reports non-receipt, preserve both records and investigate the handoff boundary. Do not invent a theft, force success, or erase the resident report. No real pickup or redelivery is requested here.

## Trace B Incomplete merchandise declaration

A fictional international parcel has a valid destination but an insufficient contents description. Origin acceptance and transport consolidation occur. Destination clearance asks for information. The gap does not establish loss, seizure or ownership transfer; the responsible operator and authority must be distinguished.

A possible permitted path is accurate documentation through the authorized process, then release, destination routing and final delivery. Another is rejection and return or other authorized disposition. This example does not promise that every defect is correctable after dispatch or that any authority must release the item.

Counterexample tested: correct address plus acceptance does not entail successful delivery. Access and admissibility remain independent conditions. The text-only correction is to name those conditions, retain unresolved evidence and avoid creating a duplicate replacement before establishing the first item status.

# Synthetic email and API traces

The following traces are fictional. They demonstrate protocol boundaries, not vulnerabilities tested against a live system. No message was sent and no API was invoked. [I07-I09, R03]

## Trace C Accepted email that is never read

At 09:00 a sender submits a message to mira@example.net. The receiving mail server accepts the complete message. Later the mailbox service stores it, but a mailbox rule files it in an unattended folder. Mira never opens it, and no disposition notification is sent.

The sender can establish only the events for which evidence exists: submission, receiving-server acceptance and perhaps mailbox delivery. Neither lack of a bounce nor a transport acknowledgement supplies the missing human-reading event. A displayed receipt, if it existed, would still not prove understanding, agreement or authorized action.

## Trace D Lost response and duplicate effect

Event | What follows
Request A sent | The client asks a fictional inventory API to create a reservation.
Reservation R1 committed | The server effect occurs, but its response is lost.
Client timeout | The client knows its wait expired; it does not know that R1 failed.
Naive retry accepted | Without defined duplicate protection, request B creates R2.
Reconciliation | Two reservations exist for one intended action. Transport correctness did not prevent the business error.

A proposed correction is a stable idempotency key for the intended reservation, bound to its parameters and atomically related to the result. Concurrent repeats must converge within the service-defined scope and retention period. Issuing a fresh key for every retry defeats that purpose. Any later warehouse handoff needs its own transactional or duplicate-safe treatment.

This is not a universal exactly-once proof. A crash between a side effect and its record, expired deduplication history, inconsistent parameters or a downstream service outside the boundary can reintroduce uncertainty. The repair is a bounded design proposal and remains unratified and undeployed.

# Reusable delivery state and evidence record

Use this proposed analytical record for one intended delivery or action. It is a comparison aid, not a replacement for an operator system or legal chain-of-custody requirement. Retain observations separately from inferred state and preserve conflicting reports.

Field group | Record
Identity and scope | Record ID; intended item or action; object version; physical original or digital copy; sender and recipient roles with minimal necessary identifiers.
Authority and contract | Authorized purpose; requester role; applicable operator, jurisdiction, service, specification version and terms-check date.
Boundary and state | Prepared, submitted, accepted, in transit or queued, attempted, delivered to named boundary, processed, or explicit exception/terminal state.
Event evidence | Event ID; event time with zone; observation time; observer; evidence type and location; integrity/authenticity check; confidence and limitations.
Custody and responsibility | Current known custodian or responsible service; handoff source and destination; what responsibility was accepted; unknown intervals.
Failure and recovery | Reason code plus plain meaning; retry or return eligibility; duplicate risk; deadline or expiry; next owner; authorized alternatives; stopping condition.
Privacy and retention | Access restrictions; redacted identifiers; retention rule; necessary content only; separate secrets from diagnostic records.
Disposition | Supported, inferred, hypothetical, disputed or unknown; open questions; proposed text correction; manual ratification status.

## Minimal completed example

SYNTHETIC D-04: intended reservation, one logical action; client timeout observed at 09:02 UTC; server result unknown to that observer; request identifier retained; no retry authorized by this record alone. Next step in the model: reconcile against authoritative application state. Stop when one intended outcome is established or an unresolved exception has a named owner.

Do not make one status field carry every meaning. Delivery-to-mailbox, personal retrieval, display, reading and consent may be separate events with different evidence and retention requirements. A blank field means not established, not automatically false.

# Operations privacy access and service choice

The operational unit is the end-to-end outcome, not merely the fastest link. Capacity depends on people, machinery, transport slots and receptacles for post; and on links, compute, storage, power, cooling and staff for digital systems. Backlogs and repair work consume capacity after the initial incident. [I01, I02, R04]

## Choose a service by the required boundary

State the object, deadline, receiver, proof required, confidentiality needs and acceptable recovery. Then compare service eligibility, exclusions, retention, support and remedy. A carrier guarantee or cloud SLA may offer a conditional refund or credit rather than delivery or data recovery. Avoid transferring one provider contract to another. [P04, P05, R05]

## Observe and recover

Digital monitoring can distinguish access, DNS, connection, application and queue failures. Latency, traffic, errors, saturation, queue age and end-to-end results answer different questions. Named incident ownership and authorized rollback plans help prevent uncoordinated changes from compounding faults. Redundancy is not backup: corruption or deletion may replicate, so restoration evidence matters. [R04]

## Protect people and evidence

Tracking identifiers, signatures, address histories and message metadata can expose personal information. Logs should preserve diagnostic evidence without unnecessarily copying bodies, credentials or secrets. Use independently reached operator channels for suspicious delivery-payment messages rather than unsolicited links. [P12, I11]

Accessibility is a separate completion condition. Reaching a building does not show that a resident can reach a locker; an app alert does not show that its information is perceivable or usable. USPS has a documented physical-hardship request process, assessed rather than automatically granted. Digital access alternatives should be evaluated against actual tasks and user needs, not assumptions about disability. [P11]

## Bridge to sector logistics

The separate Blackwish sector-logistics reference covers inventory and warehouse workflows. Here the bridge is only the handoff: an order or reservation record, a physical package and its carrier label are different objects. Warehouse dispatch, carrier acceptance and customer receipt should not collapse into one status. No sector reference is replaced or canonically synchronized.

# Zen reviews one and two

Three scoped text-only reviews use POINT for the claim, BRIDGE for evidence and authority, PATH for consequences, alternatives and termination, and SHADOW for counterexamples. They concern this reference, not the complete Blackwish canon or real-world validation.

## Review one Evidence and semantic boundaries

POINT: a delivery statement should identify its object, receiving boundary and evidence. Receipt, reading, comprehension, consent and ownership remain distinct.

BRIDGE: USPS tracking and extra-service definitions support bounded physical evidence; SMTP, DSN, MDN and HTTP specify different digital events. The record on page 13 preserves observation, inference and authority separately. No record field confers permission. [P02, P04, I07-I09]

PATH: replace an ambiguous success claim with the strongest supported event. Where evidence is absent, retain unknown or disputed state. Alternatives include a narrower claim or an explicit request for further evidence. Terminate this review when each selected claim has a named boundary and unresolved gaps are preserved.

SHADOW: an authorized building agent signs while the resident is absent; an email is stored in an unattended folder; a notification is displayed without comprehension. Finding: all defeat the universal implication from delivery to personal reading or agreement. Intentional narrative ambiguity may remain if not mislabeled as proof.

## Review two Handoffs failure and recovery

POINT: a coherent delivery model includes exceptions, duplicate risk, responsibility and a terminal disposition rather than assuming that retries always repair failure.

BRIDGE: postal return/intercept rules, HTTP retry semantics and queue visibility examples support distinct recovery paths. Proposed idempotency and reconciliation are analytical designs, not claims about a deployed Blackwish service. [P06-P08, I07, R01, R03]

PATH: follow one accepted object through access failure or a lost reply. Compare wait, reconcile, permitted retry, return and unresolved escalation. Stop after the chosen trace has an explicit outcome or a named unresolved owner; do not retry indefinitely in the model.

SHADOW: a second shipment duplicates an item merely delayed in clearance; a repeated POST duplicates a committed reservation. Finding: uncertainty must be resolved or bounded before a repair can be described as safe or complete. No real repair is executed.

# Zen review three and bounded Death Knell

## Review three Authority access and applicability

POINT: delivery capability does not establish permission, accessibility or universal service eligibility. A source must be current enough for the particular claim and applied within its scope.

BRIDGE: USPS products are jurisdiction-specific; operator documents describe those operators; RFC status records establish publication status, not installed support. The reviewed PO Box and hardship processes demonstrate conditions rather than universal access. [P03, P11, I06, I11]

PATH: ask who may request a change, what receiver can actually access the endpoint, and which source version governs. Alternatives are a narrower service claim, an accessible authorized channel or an unresolved gap. Stop after those limits are explicit; any proposed Blackwish revision remains subject to manual ratification.

SHADOW: a private carrier cannot use an arbitrary PO Box merely because it exists; a valid domain signature can accompany harmful content; a current standard can be unsupported by a particular endpoint. Finding: reachability, authenticity and standards status are insufficient substitutes for authorization, safety or deployment evidence.

## Bounded Death Knell adversarial audit

Target claim: "A delivered or accepted status plus authentication proves that the intended person received safe content and authorized the next action." Scope: the synthetic traces and defined status meanings in this document only.

Counterexample | Result within the bounded model
Parcel signed for by agent | Handoff can succeed without personal receipt or reading by the named addressee.
Authenticated email left unread | Domain authentication and mailbox delivery do not establish safe content, comprehension or consent.
API commit with reply lost | Missing response does not establish failure; a retry can duplicate the intended effect.

Outcome: the target implication fails. Narrow it to a specific evidenced boundary and require independent authority for later actions. This rejects the selected overclaim, not the entire project. No contradiction found in another case would mean only that the bounded search found none.

Stopping condition reached: the selected implication has documented counterexamples and correction options. No universal proof, empirical result, canonical ratification or deployment authorization follows. Final disposition: NEW RESEARCH / REVIEWED / NOT RATIFIED.

# Protocol status and source limits

Status was checked on 23 October 2026 UTC against RFC Editor or IETF records. These are selected base documents, not an exhaustive implementation or security checklist. Updates and errata can matter even when a base RFC is not obsolete.

Area | Selected verified status
DNS and IP | RFC 9499 is Best Current Practice; IPv6 RFC 8200 is Internet Standard with a later update. BGP RFC 4271 and IPv4 router RFC 1812 have later updates.
Transport and HTTP | TCP RFC 9293 and HTTP semantics RFC 9110 are Internet Standards. QUIC RFC 9000 and HTTP/3 RFC 9114 are Proposed Standards.
TLS 1 3 | RFC 9846 is Proposed Standard and obsoletes RFC 8446. It remains TLS version 1.3.
Mail authentication | SPF RFC 7208 and DKIM RFC 6376 have later updates. Current DMARC core RFC 9989 and reporting RFCs 9990/9991 are Proposed Standards; RFC 7489 is obsolete.

The correction from RFC 8446 and RFC 7489 matters for a current reference. It does not show that every provider has updated, that older text has no historical value, or that protocol conformance makes an application safe. Exact deployments require their own evidence. [I03-I11]

## What the evidence can and cannot establish

USPS living pages describe the US baseline at review time. An actual route, content category, country restriction, service interruption or claim needs its own current check. The 2024 UPU transport and customs guides establish architectural distinctions, not all national rules in 2026. The 2016 SRE book supports engineering principles, not current provider promises. [P09, P12, R04]

Operator examples from AWS, Twilio, Firebase and Stripe are deliberately scoped; their semantics must not be generalized to every storage, queue, messaging or payment service. Undated living pages have an access date here, not an invented publication date. No prices, quotas or universal transit times are asserted.

This is public-document research plus synthetic reasoning. It did not inspect facilities, traffic, customer accounts, actual messages, live service configurations or a complete Blackwish canon. Some FAQ variants were unreadable; the CBP package guidance was checked through official search rendering. These access limits do not justify inventing omitted details.

All source-register links were consulted in the research pass on 23 October 2026 UTC. Square-bracket identifiers identify support near claims. The proposed record, review method and cross-domain synthesis are explicitly analytical additions, not quotations from the operators.

# Sources for physical delivery

Primary-source register. Checked 23 October 2026 UTC. Service and operator applicability is qualified in the text. Links are clickable; an access date is not a publication date.

[P01] USPS addressing and package preparation

https://faq.usps.com/articles/Knowledge/Addressing-Mailpieces
https://www.usps.com/ship/packages.htm

[P02] USPS tracking event meanings and barcodes

https://faq.usps.com/articles/Knowledge/Where-is-my-package
https://pe.usps.com/businessmail101?ViewName=Barcodes

[P03] USPS PO Boxes and premium service agreement

https://www.usps.com/manage/po-boxes.htm
https://www.usps.com/pobox/customer-agreement-for-premium-po-box-service-enhancements.pdf

[P04] USPS extra services and Registered Mail

https://pe.usps.com/text/dmm300/503.htm
https://faq.usps.com/articles/Knowledge/Registered-Mail-The-Basics

[P05] USPS Priority Mail Express and insurance services

https://www.usps.com/ship/priority-mail-express.htm
https://www.usps.com/ship/insurance-extra-services.htm

[P06] USPS redelivery and undeliverable mail

https://faq.usps.com/articles/Knowledge/Redelivery-The-Basics
https://pe.usps.com/text/dmm300/507.htm

[P07] USPS hold forwarding and interception

https://www.usps.com/manage/hold-mail.htm
https://www.usps.com/manage/forward.htm
https://www.usps.com/manage/package-intercept.htm

[P08] USPS missing mail and domestic claims

https://www.usps.com/help/missing-mail.htm
https://www.usps.com/help/claims.htm

[P09] UPU transport and customs architecture
2024 guides; architecture, not all current national requirements.
https://www.upu.int/UPU/media/upu/files/postalSolutions/programmesAndServices/postalSupplyChain/Transport/publications/guidePostalTransportEn.pdf
https://www.upu.int/UPU/media/upu/files/postalSolutions/programmesAndServices/postalSupplyChain/customs/guideWcoUPUCustomsEn.pdf

[P10] USPS customs descriptions and CBP package guidance
CBP content checked through official search rendering.
https://www.usps.com/international/customs-forms.htm
https://www.help.cbp.gov/s/article/Article-1174

[P11] USPS physical hardship service request

https://about.usps.com/forms/ps1528.pdf

# Sources for Internet delivery

Primary-source register. Checked 23 October 2026 UTC. Service and operator applicability is qualified in the text. Links are clickable; an access date is not a publication date.

[I01] ITU connectivity and submarine cable resilience
Cable resilience article dated 2 February 2026.
https://www.itu.int/itu-d/sites/cpp/
https://www.itu.int/hub/2026/02/the-world-is-coming-together-to-strengthen-submarine-cable-resilience/

[I02] Interconnection and data centre dependencies
Internet Society brief dated 13 October 2026; AWS is an operator example.
https://www.internetsociety.org/resources/policybriefs/2026/ixps-and-local-interconnection-ecosystems/
https://aws.amazon.com/trust-center/data-center/our-controls/

[I03] DNS terminology and separation from routing

https://www.rfc-editor.org/info/rfc9499/
https://www.icann.org/en/rssac/faq

[I04] BGP and IP forwarding

https://www.rfc-editor.org/info/rfc4271/
https://www.rfc-editor.org/info/rfc1812/
https://www.rfc-editor.org/info/rfc8200/

[I05] TCP QUIC and HTTP 3

https://www.rfc-editor.org/info/rfc9293/
https://www.rfc-editor.org/info/rfc9000/
https://www.rfc-editor.org/info/rfc9114/

[I06] Current TLS 1 3 and predecessor status
RFC 9846 replaces 8446; the protocol remains TLS 1.3.
https://www.rfc-editor.org/info/rfc9846/
https://www.rfc-editor.org/info/rfc8446/

[I07] HTTP semantics and caching

https://www.rfc-editor.org/rfc/rfc9110.html
https://www.rfc-editor.org/info/rfc9111/

[I08] SMTP and delivery status notifications

https://datatracker.ietf.org/doc/rfc5321/
https://www.rfc-editor.org/info/rfc3461/
https://www.rfc-editor.org/rfc/rfc3464.html

[I09] Message disposition notifications

https://datatracker.ietf.org/doc/rfc8098/

[I10] SPF and DKIM

https://www.rfc-editor.org/info/rfc7208/
https://www.rfc-editor.org/info/rfc6376/

# Sources for authentication and related services

Primary-source register. Checked 23 October 2026 UTC. Service and operator applicability is qualified in the text. Links are clickable; an access date is not a publication date.

[P12] Service alerts and postal phishing guidance

https://about.usps.com/newsroom/service-alerts/
https://www.uspis.gov/news/scam-article/smishing-package-tracking-text-scams

[I11] Current DMARC and reporting specifications
RFC 7489 is obsolete; current core and reporting documents are distinct.
https://www.rfc-editor.org/info/rfc9989/
https://www.rfc-editor.org/info/rfc9990/
https://www.rfc-editor.org/info/rfc9991/
https://www.rfc-editor.org/info/rfc7489/

[R01] AWS object consistency and queue visibility

https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html
https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html

[R02] Messaging and push acceptance semantics

https://www.twilio.com/docs/messaging/api/message-resource
https://firebase.google.com/docs/cloud-messaging/customize-messages/setting-message-lifespan

[R03] Idempotency and webhooks as operator examples

https://docs.stripe.com/api/idempotent_requests
https://docs.stripe.com/webhooks

[R04] SRE monitoring incident response and recovery
2016 engineering guidance; not a current service contract.
https://sre.google/sre-book/monitoring-distributed-systems/
https://sre.google/sre-book/managing-incidents/
https://sre.google/sre-book/data-integrity/

[R05] Example service level agreement
S3 SLA page last updated 28 November 2023; provider-specific terms.
https://aws.amazon.com/s3/sla/
