# VR rigging vector graphics and mesh research

A production and evidence guide for Blackwish

Research checked 22 October 2026

## Findings and scope

**The practical conclusion:** a convincing virtual scene is not evidence that its geometry, animation, tracking, permissions, collision or performance are correct. Treat these as separate claims with separate evidence. VR is not one interchangeable device or runtime, and a file that opens successfully has not necessarily preserved the behavior of its authoring project.

This guide connects current VR platforms to the underlying asset pipeline: vector and raster artwork, mesh geometry, rigs, skinning, animation, interchange, runtime rendering and interaction. It then describes comfort, accessibility, privacy, multiplayer and review requirements. It supports research and text-only Blackwish analysis, not a purchasing decision or an implementation certification.

The hardware and standards snapshot is dated. An announcement, an available document, a purchase invitation, a supported API and a shipped product are different statuses. Where a shipment date or release status was not established, the uncertainty remains visible. This is a broad orientation and production guide, not an exhaustive inventory of every headset, SDK, extension, research paper or jurisdiction.

**Blackwish applications in this guide are proposals.** They do not amend canonical text, implement a renderer, authorize sensors, approve a human experiment or ratify deployment. Research, review, manual ratification and implementation remain separate. Compatibility statements concern the selected text-first instructions available for this task, not an inspection of the entire Blackwish canon.

### Reading route

Start with the capability distinctions and platform snapshot. Read the graphics chapters to understand what is being built and exported. Use the pipeline and review chapters to turn vague ambitions into inspectable records. The final source register preserves direct primary sources; dates identify the research check unless a publication date is stated explicitly.

### Evidence labels

**Documented** means a primary source supports the described feature or limitation. **Announced** means future availability was described, not verified shipment. **Unverified** means this review did not establish the fact. **Proposed** means a suggested Blackwish application, not current behavior. **Measured** should be reserved for an actual named test with method and results; no headset, asset pipeline or participant test was performed for this guide.

## What VR systems actually contain

VR usually replaces the visible environment with a virtual scene. AR adds digital material to a view of the physical world. MR commonly refers to spatially registered digital content interacting with surroundings, but vendors use the label differently. XR is the umbrella term. Define actual capabilities rather than relying on these labels alone. [S01]

Video passthrough shows camera-derived imagery of the room; it is not direct optical sight. Standalone describes where computation happens, not whether the experience is VR or MR. A standalone headset may also stream a scene rendered by another computer. An optical display, camera passthrough, opaque VR and a flat window inside a headset pose different rendering and interaction requirements.

A useful system model separates five layers:

- **Presentation:** optics, display, refresh, stereo views, passthrough and compositing.
- **Sensing and input:** head and controller poses, hands, eyes, voice, environment and optional body devices.
- **Runtime:** device abstraction, permissions, reference spaces, input actions and frame submission.
- **Application:** world state, interaction rules, simulation, content and network behavior.
- **Assets:** geometry, textures, materials, animation, sound, metadata and provenance.

OpenXR addresses the application-to-runtime interface. It does not supply the game engine, asset format, store or guarantee that every optional feature exists. WebXR provides a browser-oriented interface; it is not a synonym for OpenXR. glTF and USD describe assets or scenes rather than headset frame submission. [S18-S21, S40-S41]

**Proposed Blackwish distinction:** record display mode, computation location, required input and environmental access independently. “Supports XR” is too ambiguous to review. A mystery room can be a seated flat-screen scene, opaque VR, or room-scale MR; the narrative may be similar while permissions, comfort and physical risks differ substantially.

## Platform snapshot as of 22 October 2026

This is a representative status snapshot, not a ranking or shopping recommendation. Host, operating system, runtime and accessory combinations matter as much as product names.

**Meta Quest 3 and Quest 3S:** current Meta Horizon OS all-in-one devices in the device comparison documentation. They support controller and hand-oriented interaction but do not contain eye-tracking hardware. A software proposal requiring gaze tracking cannot silently treat these models as equivalent to eye-equipped devices. [S02, S12]

**Meta VR Glasses:** announced with Spring 2027 availability. The documented design combines approximately 100 g eyewear with a tethered compute and battery puck, and eyes, hands and voice as input. It belongs in an announced/future-target column, not a shipped-device baseline. [S03]

**Apple Vision Pro with M5:** announced 15 October 2025 with availability from 22 October 2025. It uses a separate battery and supports hands, eyes, voice and spatial accessory interactions. Hardware eye tracking does not mean applications receive raw eye movements. [S04, S16]

**Samsung Galaxy XR:** Samsung's release dated 22 October 2025 says it was available then. It uses Android XR, head, hand and eye tracking, and camera passthrough. Check application-level API and permission support separately from the sensor list. [S05]

**Valve Steam Frame:** official Steamworks documentation describes a streaming-first standalone SteamOS device, including PC streaming and standalone execution paths. September 2026 purchase invitation or limited-drop material does not establish the exact physical shipment date; that date remains unverified here. Compatibility with a PC title does not prove adequate standalone performance. [S06-S07]

**PlayStation VR2:** supported uses on PS5 and Windows PC have different features. Sony lists absent PC features including HDR, eye tracking, headset feedback, adaptive triggers and advanced Sense haptics; basic controller vibration remains. PC does not automatically activate see-through view when the user leaves the play area. [S23]

**Windows Mixed Reality:** removed beginning with Windows 11 version 24H2. Microsoft's conditional legacy statement says existing devices continue with Steam through November 2026 on Windows 11 version 23H2. Treat this as a constrained legacy-support case, not an indefinite supported growth platform. [S08]

## Displays and performance numbers without false equivalence

Resolution is not a single quality measure. Distinguish physical panel pixels, render resolution, visible angular detail, optical clarity, field of view, refresh rate, new application frames and reprojection. A 90 Hz display does not establish that an application renders 90 new frames each second.

Quest 3's published resolution is 2064 by 2208 pixels per eye with pancake optics; combined “4K+” marketing should not become “4K per eye.” [S09] Apple's M5 Vision Pro specifications list 23 million display pixels and 90, 96, 100 and 120 Hz operation. Its R1 12 ms photon-to-photon figure is a vendor subsystem metric, not a measured total latency for an arbitrary application interaction. [S10]

Samsung documents Galaxy XR's 3552 by 3840 display resolution, 27 million pixels and micro-OLED panels. Its stated refresh modes are 60 Hz, 72 Hz default and up to 90 Hz upon service request; it should not be summarized as always running at 90 Hz. The listed field of view is 109 degrees horizontal by 100 degrees vertical. [S05]

For the announced Meta VR Glasses, documentation distinguishes nominal straight-ahead field of view, 70 by 66 degrees, from a 74 by 68 degree render extent. Fit, eye position and gaze affect the visible result. A render extent is not a guarantee of what every wearer sees. [S11]

**Proposed measurement record:** name the device, host, OS, runtime, application build, quality settings, scene, refresh mode, test duration and method. Report CPU and GPU timing separately, and note thermal state, missed frames, reprojection and tracking loss. A simple reciprocal frame-time budget is about 13.9 ms at 72 Hz, 11.1 ms at 90 Hz and 8.3 ms at 120 Hz; those arithmetic totals are not promises of the usable budget after runtime overhead.

No universal polygon ceiling or single “VR-ready” badge establishes success. Shaders, overdraw, stereo rendering, texture bandwidth, lighting, animation, physics and networking can move the bottleneck. Candidate optimizations must be profiled in the actual target configuration. [S42-S43]

## Tracking is not the same as full body measurement

Six degrees of freedom describe three rotational and three positional components. Three-degree tracking describes orientation without equivalent positional tracking. Specify this separately for the headset, controllers and other tracked objects. [S24]

A rendered avatar can contain more joints than the tracking system directly observes. Meta documentation explicitly distinguishes estimated lower-body poses; tracking fidelity can also change with thermal pressure. Hand tracking may lose observations when hands are occluded or outside camera coverage. A smooth animation can conceal missing evidence rather than demonstrate measurement accuracy. [S12-S13]

Use a signal chain: **sensor observation → estimated pose → filtered or predicted pose → retargeted skeleton → artistic correction → rendered avatar.** These stages are conceptually distinct even when an SDK bundles them. Store provenance at the boundary where a claim is made. Do not label an inferred knee position as a directly measured knee position.

A useful proposed state vocabulary is tracked, estimated, stale, unavailable and permission denied. Add timestamps and reference spaces where relevant. A stale pose should not silently become a fresh observation. Loss of a controller should not trigger an unintended action merely because the last pose remains visually plausible.

Hand tracking is not force feedback. A virtual hand entering a wall does not create physical resistance. IK can align a hand with a virtual target but cannot prove the real hand is in the same location, the posture is comfortable or the user has room to move.

**Genre-neutral examples:** a science-fiction robot can intentionally have nonhuman proportions; a documentary reconstruction must distinguish measured motion from illustrative animation; a historical character's coat needs deformation review; a comedy character's squash may be intentional rather than a defect. The intended claim controls what evidence is required.

## Environmental access and privacy boundaries

Separate the user's composited passthrough view from application access to raw camera images. Also distinguish scene planes or labels, room geometry, depth, spatial anchors, persistence and screen capture or casting. Permission for one is not blanket permission for the others. [S01, S14]

Meta's Camera API documentation checked for this review distinguishes front-camera access from MediaProjection or casting. Camera textures do not cover the full passthrough view, and supported resolutions differ by software/device context. The documented API has device-user-data permission requirements and is not supported in XR Simulator. A simulator result therefore cannot be substituted for a camera-path validation. [S14]

Apple states that normal eye input is not shared with apps, websites or Apple. Applications can receive the resulting interaction without receiving raw eye movements. Android XR documentation likewise treats hand and eye information as privacy-sensitive and describes required permissions. [S16-S17]

**Proposed Blackwish data record:** for camera, room mesh, depth, gaze, voice and body data, record the purpose, source, permission, processing location, retention, access, export behavior and deletion expectations separately. Raw data and derived inferences may have different risks; a reduced representation is not automatically anonymous.

A room mesh can reveal layout and private surroundings. Passthrough availability does not authorize recording or uploading someone's home. Environmental reconstruction is not a physical safety certificate: obstacles may move, tracking may drift, camera coverage is limited and geometry may be incomplete.

For a text-only scenario review, use fictional or explicitly supplied room descriptions. No new environmental capture, participant sensing or live experiment is necessary to reason about a missing-permission counterexample. Actual collection or deployment must follow its own authorization and review gate.

## Vector graphics and raster artwork

Raster artwork stores sampled pixels. Enlarging it does not recover absent detail. Vector artwork represents paths and shapes that can be rendered at different scales, but it still becomes samples on a display. SVG paths can include straight segments, quadratic and cubic Bézier curves, arcs and subpaths. Curve control points guide a curve; they are not necessarily points the curve traverses. [S25]

Fill paints an interior according to a fill rule. Stroke follows a path with properties such as width, caps, joins and dashes. Open and closed paths can produce different results. Coordinate transforms, the viewport and the viewBox need to be understood together; a shape's authored coordinates are not identical to its final displayed size. [S26-S27]

A runtime may tessellate curves into triangles or render them into textures. Tighter tessellation tolerance can increase geometry; texture conversion makes texture resolution and sampling important. Unity's vector-graphics package documentation illustrates the trade-off, but the reviewed package is explicitly experimental 2.0.0-preview.25 and not recommended there for production. This guide does not recommend that preview as a current production dependency. [S28]

Useful applications include science-fiction instrument panels, documentary diagrams, historical maps, mystery clues, interface icons and 2D character layers. Select vector or raster by the content and delivery path, not a blanket belief that one is always superior. Photographic detail is naturally raster; editable geometric diagrams benefit from vector structure.

**Review questions:** Is lettering readable at the intended apparent size and depth? Do thin strokes survive antialiasing? Does a converted texture blur at close inspection? Are transparency and layering correct? Does an icon remain understandable without color alone? A vector source preserves editability but does not establish readability, performance or semantic accuracy.

## Mesh geometry and surface appearance

Vertices define points, edges connect them and faces form surface elements. Topology is the connectivity pattern, not simply the polygon count. Authoring quads may become triangles in a runtime. Two assets with equal face counts can deform, shade and render very differently. [S29]

A runtime vertex record can contain position, normal, tangent, UV coordinates and joint influence data. Normals guide lighting; tangents provide a basis used by normal mapping; UV coordinates map surface positions to texture coordinates. UV seams or shading boundaries can require separate runtime vertex records at the same geometric position, so exported vertex counts may differ from what an artist expects. [S30]

Mesh density is not visual quality by itself. A densely subdivided flat plane may look plain, while a low-polygon surface can appear detailed through textures and lighting. Ordinary normal maps alter shading rather than the base silhouette or collision shape. Close stereo inspection can expose this difference, particularly at an edge. [S31]

Keep the following representations separate:

- **Render mesh:** the surface drawn by the renderer.
- **Deformation representation:** joints, weights, shape changes or other motion controls.
- **Collider:** geometry and rules used for physical contact or queries.
- **Visibility representation:** what is rendered, clipped, culled or hidden.

Geometric intersection, camera clipping, backface culling, occlusion and occlusion culling are different phenomena. Occlusion culling itself consumes computation and memory; it is not an automatic speed-up. [S45]

A simplified collider can be appropriate for performance, but its mismatch with the visible surface should be intentional and reviewed. An invisible collider can block an apparently open doorway. A deforming render mesh does not establish a matching deforming collider. [S38]

**Proposed asset acceptance:** record intended silhouette, scale, topology needs, UV/material assumptions, deformation range, collider approximation and expected inspection distance. Avoid calling an asset “correct” when only its still image has been checked.

## Rigs FK IK skinning and shape correction

A skeleton is a hierarchy of joints or bones; parent transforms affect descendants. A broader rig can include animator controls, constraints, deformers and procedural logic. The control system used by an artist is not always the same representation exported to a runtime.

Forward kinematics controls joints directly through the hierarchy and can support deliberate motion arcs. Inverse kinematics solves joint poses toward a target and is useful for contact, such as keeping a hand near a handle. Switching or blending between FK and IK needs an intentional matching strategy. Neither method guarantees balance, anatomical plausibility, collision avoidance or comfortable real-world posture. [S32]

Skinning binds surface points to joint influences. Weights control their contributions. Poor weights can pull a sleeve toward the wrong bone or collapse an elbow. Linear skinning can lose volume under twisting; alternative skinning approaches or corrective shapes can help, but availability and export support must be checked in the chosen pipeline. [S33-S34]

Morph targets describe alternative shape differences blended by weights. They can support expressions, eyelids, speech shapes and corrective deformation. They are distinct from joints, even when driven by joint motion or animator controls. [S35]

Constraints and limits describe selected relationships, not the entire intended anatomy or artistic purpose. A technically valid rig may allow an unwanted extreme pose or prevent intentional cartoon squash. Specify the intended motion range and the acceptable exceptions. [S36]

**Proposed rig review:** inspect representative bends, twists, contact poses, expression combinations and transitions, including deliberately difficult counterexamples. Check the art-direction requirement separately from technical validity. A robot's rigid wrist casing should not collapse like skin unless that behavior is intentional; a comedy character should not be rejected merely for nonhuman deformation.

## Retargeting coordinates and animation evidence

Retargeting transfers motion between different character structures. Joint names alone do not establish equivalent movement. Mapping, reference poses, proportions, chain definitions and contact behavior matter. Epic's IK retargeting documentation supports transfers across different bone counts, names, orientations and proportions, with optional IK contact preservation. This is capability documentation, not proof that any arbitrary pair will retarget without review. [S37]

**Counterexample:** a tall actor reaches a table. Copying rotations to a shorter character can leave the hand short of the surface. Preserving hand contact may require different shoulder and torso motion. Changed leg length may create foot sliding. The desired invariant might be trajectory, contact, timing or expressive intent; it cannot be assumed to be all of them simultaneously.

Coordinate spaces also matter. Local coordinates are relative to an object or parent; world coordinates are relative to the scene; view coordinates are relative to a camera. Stereo rendering has a distinct view for each eye. Units, axis orientation, handedness, origin, parent hierarchy and scale must survive export intentionally.

Nonuniform scale applies different scale factors on different axes. In a hierarchy it can produce shear-like effects when combined with rotations. Unity documents cases where mesh and collider behavior can disagree, and warns about zero scale. A scene can look plausible while its physical dimensions or collision relationships are wrong. [S39]

**Proposed provenance chain:** distinguish original capture, estimated motion, cleanup, retargeting, artistic changes and final export. Preserve the native source and record which stages are reversible. A documentary animation should not imply measured evidence for manually reconstructed movement. A fictional animation can use inference freely while still documenting its technical dependencies.

## Interchange formats and standards

**glTF 2.0** is delivery-oriented. It represents meshes, materials, scene hierarchy, skinning, morph targets and animation, but does not promise arbitrary authoring-rig controls or constraints. Core animation targets node translation, rotation, scale and morph weights. A successful import does not prove preservation of every DCC behavior. [S40]

Two important source corrections follow the normative specification rather than an overgeneralized tutorial. glTF permits JOINTS_n and WEIGHTS_n sets beyond the first four joint influences, although an implementation may support only the first set. Animation channels sample node properties; they are not inherently bind-pose-relative deltas. Export and runtime limits must be stated as implementation limits rather than misattributed to the format. [S40]

**OpenUSD** supports scene assembly, references, layers, variants and non-destructive overrides. Its own introduction says it is not a rigging system. The ability to encode custom data does not guarantee that another application understands the same behavior. The reviewed /release page displayed a 26.11 label; this review does not infer general availability from that label. [S41]

**OpenXR** is the native application-runtime interface. The official changelog records version 1.1.65 on 16 October 2026, including spatial/data-flow work and a standardized detailed-hand permission string. A registered extension is not automatically a ratified extension or universally implemented feature. Android XR documents OpenXR 1.1 with selected extensions; applications must check the actual runtime. [S18-S20]

**WebXR** was a W3C Candidate Recommendation Draft dated 9 June 2026 when checked. It was not a final W3C Recommendation. Browser, device and feature availability still require verification. [S21]

**Proposed export manifest:** native source; export format/version; exporter and importer versions; required extensions; units and axes; baked versus editable behavior; unsupported features; licensing/provenance; validation results. File extension alone is not a compatibility guarantee.

## A production pipeline with explicit evidence gates

The following is a proposed workflow, not a claim that Blackwish already implements it.

**1 Define intent.** State medium, genre, audience, interaction, presentation mode, target capabilities and what the scene is supposed to establish. Separate fictional imagery from measured reconstruction.

**2 Block out.** Establish scale, layout, viewing distances and interaction reach before polishing details. A text-only plan can expose contradictory dimensions without building a live scene.

**3 Build representations.** Create or select artwork, geometry, UVs, textures, materials, skeletons, weights and corrective shapes. Preserve source licenses and native originals. Define colliders separately from visual surfaces.

**4 Animate and review.** Check motion range, contacts, retargeting, expression combinations and intended stylization. Review both ordinary poses and counterexamples. Do not rely on a single attractive still.

**5 Export deliberately.** Record units, axes, extensions and features that were baked, approximated or lost. Preserve an editable source alongside purpose-specific exports.

**6 Integrate only under authority.** Runtime shaders, inputs, reference spaces, anchors, colliders, LODs and network behavior need their own validation. Text review does not authorize a live integration.

**7 Measure the actual target.** Candidate optimizations include appropriate LOD, fewer costly material changes, texture compression, controlled transparency and supported stereo/foveation paths. None is an unconditional improvement. Evaluate deformation-aware LOD: a vertex removed in a harmless rest pose may be essential to an expression or bend. [S42-S44]

**8 Separate release gates.** Source verification, design review, user ratification, implementation approval and release evidence remain distinct. Retain failed checks and unresolved limits rather than rewriting them as successful completion.

A small evidence-complete scene is more informative than a large scene with unexamined assumptions. The next useful text-only Blackwish step is to define one capability record and test its claims against hypothetical failures, not to declare a universal VR implementation complete.

## Comfort accessibility and cinematic attention

Locomotion and accessibility should be considered before final art, not added after a scene's layout makes alternatives difficult. Separate tracked head movement from artificial camera movement. Define seated, stationary and room-scale modes, floor origin, scale, recenter behavior and what happens when tracking is lost.

Meta's comfort guidance recommends distance interactions, adjustment for posture and head position, and avoiding repeated extreme head movements or large camera-fixed content that obscures passthrough. Its locomotion guidance discusses selectable movement options and limiting artificial acceleration or direction changes. Teleportation, snap turning and optional smooth movement are design choices, not guarantees against discomfort. [S46-S47]

For an immersive film, the viewer can look away from a scripted event. Spatial sound, light and motion can guide attention, but the production cannot assume the fixed camera viewpoint of an ordinary film. Essential narrative information may need another opportunity to be perceived. Avoid converting an attention cue into forced or unexpected camera motion.

The W3C XR Accessibility User Requirements document is a Working Group Note dated 25 August 2021, not baseline conformance requirements or a certification. It supplies useful needs to consider: alternative input, accessible movement and reach, captions, configurable presentation, and a dependable way to pause or escape. [S48]

**Proposed acceptance questions:** Can essential actions work seated, with one hand, with either hand or through an alternative supported input? Do they require continuous raised arms, precise pinching or standing height? Can users adjust timing, movement speed, target size and caption presentation? Are essential cues available without relying solely on color, sound direction or gesture? Is pause or exit reachable when the preferred input fails?

These are review questions, not completed accessibility tests. An option existing in a menu does not prove every critical path respects it. A documentary subtitle may be legible in a screenshot yet fall outside the user's comfortable view during movement. A mystery clue should not require an inaccessible gesture simply because that gesture suits the fiction.

## Runtime timing optimization and validation

OpenXR's frame loop separates waiting for a frame, beginning it and submitting it. Predicted display time helps coordinate poses and views; it is not certainty about the future or a replacement for ordinary time semantics. The current frame-submission guide supports this conceptual account; this review did not audit every part of the full specification. [S49]

Inspect CPU simulation, render submission and GPU work separately. A favorable mean frame rate can conceal repeated missed deadlines. Sustained operation, scene changes and thermal behavior matter. Use a named target and reproducible settings before claiming that an optimization improved performance.

Stereo rendering can expose assumptions hidden in a flat-screen preview. Screen-space effects may not behave correctly for both eyes. Epic's performance guidance emphasizes profiling during production, but some examples retain legacy engine context; verify commands and settings against the actual engine version rather than copying them blindly. [S50]

Fixed foveation and gaze-driven foveation reduce rendering detail in selected regions by different mechanisms. Their support and permission requirements vary. They do not solve every CPU, tracking, networking or latency problem. Reprojection can help presentation but should not be used to disguise failure to meet the intended new-frame target. [S51-S52]

**Proposed validation matrix:** device and host; OS and runtime or browser; engine, SDK and plugins; graphics settings; required and optional capabilities; denied or revoked permissions; controller disconnection; tracking loss; recenter; pause/resume; room changes; scene transitions; sustained load; network delay and rejoin. Record the outcome of each check as not run, passed, failed or inconclusive, with evidence and scope.

Before an authorized physical test, the test plan also needs an appropriate environment, participant permissions and stop procedure. Manufacturer safety guidance stresses attention to surroundings and stopping when unwell; it does not certify a particular application's safety. No individual medical assessment or sickness-prevention guarantee is offered here. [S58]

## Multiplayer visibility authority and physical safety

Four boundaries must remain independent: what is rendered, what is replicated over the network, who can change shared state, and what is physically safe. Hiding an avatar does not remove the real person. Hiding a network object does not necessarily eliminate every route to act on it. A valid ownership transfer does not establish collision safety.

Unity Netcode for GameObjects distinguishes client-server and distributed-authority ownership behavior. Transfer permissions and locks govern particular state operations; they are not general-purpose user authorization or physical-safety policies. Its network visibility documentation concerns which clients receive objects and updates, not camera occlusion. The cited ownership and visibility pages are from different documented versions and are not represented as one tested configuration. [S53-S54]

**Proposed shared-state record:** authenticated actor; authorized operation; object owner; transfer rule; conflict policy; replication recipients; late-join behavior; disconnect recovery; retention and audit evidence. Review authority checks independently from avatar appearance or apparent proximity.

Meta's shared-spatial-anchor guidance warns that colocated multiplayer adds physical collision risks, restricted peripheral visibility and potential avatar-to-person desynchronization. Passthrough warnings can mitigate some issues but cannot guarantee safety. A shared virtual coordinate frame is not proof that every device has the same current physical understanding. [S55]

Avatar design also needs personal-space, mute, block and escape controls. Inferred limbs or synthetic gaze must not be treated as reliable evidence of intention. A participant looking toward an object is not thereby consenting to a recording, transaction or interaction. [S56]

**Counterexample:** a cooperative science-fiction repair scene hides another player's avatar behind a virtual wall. The second player remains physically present and may step into the first player's space. A rendering rule, network visibility rule or fictional door lock cannot solve the physical problem by itself.

## A text first Blackwish capability record

The following is a proposed review record. It contains requirements and unknowns, not claims of implemented capabilities.

**Experience identity:** title, version, genre, purpose, intended audience and claim type. Distinguish fiction, illustration, reconstruction and measured representation.

**Platform contract:** device, host, OS, runtime or browser, engine and SDK versions; local or streamed computation; immersive or passthrough presentation; seated, stationary or room-scale mode.

**Input and inference:** required and optional head, controller, hand, eye, voice and body capabilities; fallback for each; tracked versus estimated data; timestamps, tracking loss and stale-state behavior.

**Asset contract:** native source, licensing and provenance; mesh and material assumptions; rig and animation range; collider approximation; units, axes and scale; export formats and extensions; baked and editable features.

**Data contract:** each data type, purpose, permission, processing location, recipient, retention and deletion behavior. Microphone permission is not recording consent; participation in gameplay is not blanket consent to share a room. Prefer necessary interaction results over unnecessary raw sensor collection. [S21, S57]

**Interaction and access:** locomotion options, reach assumptions, alternative inputs, captions and other redundant cues, reduced-motion behavior, pause and exit. State what remains unavailable rather than masking missing capability.

**Shared-state contract:** actor authorization, ownership, transfer, conflict, replication, disconnect and rejoin rules. Keep rendering and physical safety separate.

**Evidence and status:** source, source date if known, check date, documented limit, test method, result and unresolved uncertainty. Keep not-run checks visible. Attach source verification, design review, ratification and implementation decisions as separate records.

This record is useful now because it can be evaluated using hypothetical examples without modifying a live application. The next authorized text-only step is to populate it for a named proposed scene and challenge its consistency. Actual implementation and human evaluation remain separate gates.

## Review one Zen on representations and evidence

For these reviews, POINT identifies the objective or claim; BRIDGE examines evidence and authority; PATH considers consequences, alternatives and termination; SHADOW exposes assumptions and counterexamples. These are operational review labels for this dossier, not a claim to restate every canonical definition of Zen.

**POINT:** determine whether the guide distinguishes artwork, geometry, motion, contact and observation well enough to support honest Blackwish claims.

**BRIDGE:** the source register grounds each representation in primary documentation. Normative standards take precedence over simplified tutorials. Source versions and unsupported release inferences remain visible.

**PATH:** require explicit representation and provenance fields before saying an asset is compatible or an avatar is measured. Where evidence is missing, narrow the claim or leave the field unknown. Preserve native originals and purpose-specific exports rather than overwriting the source with a reduced runtime representation.

**SHADOW:** a detailed mesh can have a crude collider; a complete skeleton can contain inferred joints; a successful glTF import can omit authoring constraints; a vector icon can be unreadable in-headset. Each defeats a different shortcut from appearance to correctness.

**Review result:** the conceptual distinctions are suitable for text-only scenario analysis. They do not establish toolchain compatibility or measured fidelity for any unnamed asset. Remaining gate: identify the actual assets and intended claims before an implementation-level judgment.

## Review two Zen on people permissions and failure

**POINT:** determine whether the proposed review process avoids treating technical capability as consent, comfort, accessibility or safety.

**BRIDGE:** platform documentation separates permissions and available data. W3C XAUR supplies user needs but is not a conformance certificate. Manufacturer comfort and safety guidance supports design precautions rather than a guarantee. Shared-anchor guidance explicitly identifies physical and synchronization hazards.

**PATH:** specify alternatives before finalizing interaction; distinguish capability unavailable from permission denied; keep an accessible pause/exit; minimize unnecessary data; record review outcomes separately from participant or device tests. If a necessary permission or accessible path is absent, stop the dependent feature rather than manufacturing a success state.

**SHADOW:** ordinary eye-based interaction can work without raw gaze access. Room sharing can expose private surroundings. A hidden avatar is still a physical person. A menu's seated option can coexist with an essential unreachable control. A smooth motion style can remain uncomfortable for a particular user.

**Review result:** the guide supports cautious requirements and counterexample review, not medical advice or a declaration of universal comfort. No people were experimented on, no environment was scanned and no device safety was certified. Actual validation needs its own authorization, methods and appropriate stop conditions.

## Review three Zen on portability production and governance

**POINT:** determine whether the dossier offers a usable production path without promoting research into implementation or canonical doctrine.

**BRIDGE:** OpenXR, WebXR, glTF and USD address different layers. Host-specific PS VR2 limitations demonstrate why product-name equivalence fails. Documented future hardware and legacy support windows are explicitly status-labeled. The proposed capability record preserves source, version, test status and uncertainty.

**PATH:** choose a bounded target matrix, preserve originals, validate export losses, profile actual scenes and keep review, manual ratification and deployment separate. Use a small scene with explicit acceptance criteria before generalizing. Pending approval on a deployment does not prevent unrelated text-only research or consistency analysis.

**SHADOW:** registered extensions may not be implemented; a documentation label may not prove shipment; an invitation to buy is not a shipment date; a low-polygon scene may remain GPU-bound; a local success says nothing about a different browser or host. No single “VR-ready” label resolves these gaps.

**Review result:** the dossier can inform next-step document preparation and text-only comparisons across science fiction, historical drama, documentary, mystery and comedy as well as fantasy. It neither requires a new visual engine nor claims that Blackwish already contains one. Proposed applications remain unratified.

## Bounded Death Knell challenge and remaining gates

This final challenge asks whether a small set of serious counterexamples defeats the dossier's main conclusion or proposed workflow. It is a bounded adversarial review, not exhaustive proof, a scientific certification or a deployment approval.

**Challenge 1:** an announced product is mistakenly used as the current baseline. The status record rejects that inference; future Meta VR Glasses remain announced, and Steam Frame's exact shipment date remains unknown here.

**Challenge 2:** sensor permission is mistaken for informed recording consent. The data contract separates permission, purpose, recipient and retention; recording and room-sharing need their own applicable authority.

**Challenge 3:** visual realism is mistaken for physical or measurement fidelity. Separate render, collider, rig and tracking-provenance records expose the gap. No amount of visual polish closes it by itself.

**Challenge 4:** an accessible option or optimization is assumed to work everywhere. The target matrix and not-run status prevent a menu option, preview or mean frame rate from becoming universal evidence.

**Challenge 5:** completing research is treated as permission to change canonical text or deploy. The review explicitly preserves research, ratification and implementation as different decisions.

**Outcome:** none of these challenges requires abandoning the capability-based approach; each requires preserving a boundary the guide already names. Unresolved implementation facts remain unresolved. A stronger test could still reveal new failures once actual assets, devices and user requirements are supplied.

**Useful next document:** one proposed scene capability sheet, an export-loss checklist and a failure-case review using fictional examples. **Not yet established:** actual exporter/importer equivalence, sustained target-device performance, accessibility outcomes, physical safety, complete canon compatibility or any live implementation. No pending implementation ratification blocks the proposed text-only analysis.

## Research limitations and source conflict handling

The review used official standards, platform, engine and authoring-tool documentation. Some sources describe stable concepts through older versioned pages; others display newer version labels whose release availability was not independently established. Checked on 22 October 2026 does not mean published on that date.

The interchange chapter resolves two tutorial oversimplifications against the normative specification. Unity's experimental vector package is an explanatory example, not a production recommendation. The full OpenXR specification exceeded the browsing tool's direct size limit; relevant indexed material and the smaller official frame-submission guide were used, not a full-specification audit. Some Blender manual fetches failed, so accessible primary alternatives were used rather than claiming those Blender pages were read.

No engine was installed, no assets were imported or exported, no headset was tested, no sensors were enabled and no participant study was conducted. The source register supports the stated research; it does not substitute for the unperformed validation steps.
## Primary source register

All sources below were checked for this research on 22 October 2026. A documentation version or page label is not, by itself, proof of a product's general availability. Links identify the particular source used; statements remain subject to the scope and limitations discussed in the guide.

### Platforms displays tracking and permissions

[S01] Meta, Mixed Reality introduction. Capability categories including passthrough, scene understanding, anchors and depth. [Source](https://developers.meta.com/vr/discover/mixed-reality-intro/)

[S02] Meta, Compare devices. Current device capability comparison; page dated 30 September 2026 in the reviewed documentation. [Source](https://developers.meta.com/vr/resources/compare-devices/)

[S03] Meta, Meta VR Glasses. Announced design and Spring 2027 availability, not evidence of shipment. [Source](https://developers.meta.com/vr/discover/meta-vr-glasses/)

[S04] Apple Newsroom, Apple Vision Pro upgraded with the M5 chip and Dual Knit Band, 15 October 2025. [Source](https://www.apple.com/newsroom/2025/10/apple-vision-pro-upgraded-with-the-m5-chip-and-dual-knit-band/)

[S05] Samsung Mobile Press, Galaxy XR Opening New Worlds, 22 October 2025. Availability and vendor specifications. [Source](https://www.samsungmobilepress.com/articles/galaxy-xr-opening-new-worlds)

[S06] Valve Steamworks, Steam Frame documentation. Architecture and execution paths. [Source](https://partner.steamgames.com/doc/steamhardware/steamframe?language=english)

[S07] Valve, Steam Frame hardware and reservation material. Exact physical shipment date remains unverified; purchase invitations are not shipment evidence. [Hardware](https://store.steampowered.com/hardware/steamframe?cc=gb) and [FAQ](https://help.steampowered.com/en/faqs/view/0AC8-A264-CC02-14F0)

[S08] Microsoft Learn, Features and functionality removed in Windows client. Windows Mixed Reality removal and conditional legacy period. [Source](https://learn.microsoft.com/en-us/windows/whats-new/removed-features)

[S09] Meta, Introducing Meta Quest 3S, September 2024. Quest 3 comparison and resolution context. [Source](https://about.fb.com/news/2024/09/meta-quest-3s-our-most-affordable-mixed-reality-headset/)

[S10] Apple Support, Apple Vision Pro technical specifications, M5 generation. Vendor display and R1 figures. [Source](https://support.apple.com/en-gb/125436)

[S11] Meta, Field of view. Nominal visible field versus render extent. [Source](https://developers.meta.com/vr/essentials/field-of-view/)

[S12] Meta, Horizon OS immersive features. Eye hardware, inferred body tracking and fidelity limitations. [Source](https://developers.meta.com/vr/essentials/horizon-os-immersive-features/)

[S13] Meta, Hand tracking limitations and mitigations. Occlusion and field-of-view limits. [Source](https://developers.meta.com/vr/design/hands-limitations-mitigations/)

[S14] Meta, Passthrough Camera API native overview, reviewed page dated 7 October 2026. Camera versus casting, permissions and simulator limitations. [Source](https://developers.meta.com/vr/documentation/native/android/pca-native-overview/)

[S16] Apple, Eyes and Hands and Privacy. Ordinary eye-input privacy model. [Source](https://www.apple.com/legal/privacy/data/en/eyes-hands/)

[S17] Android Developers, Get started with OpenXR. Sensitive tracking permissions and setup. [Source](https://developer.android.com/develop/xr/openxr/get-started?authuser=9)

[S18] Khronos, OpenXR overview. Native application-runtime interface. [Source](https://www.khronos.org/openxr/)

[S19] Khronos OpenXR documentation changelog. Version 1.1.65 entry dated 16 October 2026. [Source](https://github.com/KhronosGroup/OpenXR-Docs/blob/main/CHANGELOG.Docs.md)

[S20] Android Developers, OpenXR for Android XR. Supported API and extension context. [Source](https://developer.android.com/develop/xr/openxr)

[S21] W3C, WebXR Device API, Candidate Recommendation Draft dated 9 June 2026. Draft status does not imply universal browser support. [Source](https://www.w3.org/TR/webxr/)


[S23] PlayStation Support, Differences between PS VR2 on PS5 and PC. Host-specific feature and safety differences. [Source](https://www.playstation.com/en-us/support/hardware/ps-vr2-console-pc-difference/)

[S24] Google VR, Degrees of freedom. Stable conceptual definition; not a recommendation to adopt a legacy SDK. [Source](https://developers.google.com/vr/discover/degrees-of-freedom)

### Artwork geometry animation and interchange

[S25] W3C SVG 2, Paths. Path commands and curve concepts. [Source](https://www.w3.org/TR/SVG2/paths.html)

[S26] W3C SVG 2, Painting. Fill and stroke behavior. [Source](https://www.w3.org/TR/SVG2/painting.html)

[S27] W3C SVG 2, Coordinate systems transformations and units. [Source](https://www.w3.org/TR/SVG2/coords.html)

[S28] Unity Vector Graphics package 2.0 manual, displayed as 2.0.0-preview.25. Experimental example only, not a production dependency recommendation. [Source](https://docs.unity3d.com/Packages/com.unity.vectorgraphics@2.0/manual/index.html)

[S29] Unity 6000.0 manual, Mesh topology data. Stable mesh concepts. [Source](https://docs.unity3d.com/6000.0/Documentation/Manual/mesh-topology-data.html)

[S30] Unity 6000.0 manual, Mesh vertex data. Attributes and runtime vertex representation. [Source](https://docs.unity3d.com/6000.0/Documentation/Manual/mesh-vertex-data.html)

[S31] Unity normal-map documentation under the observed 6000.7 path. Shading rather than silhouette; version label not independently established as a shipped release. [Source](https://docs.unity.com/en-us/engine/6000.7/manual/materials-and-shaders/built-in/shader-built-in-configure-properties/standard-shader-texture-maps/material-parameter-normal-map/map)

[S32] Autodesk Maya character animation documentation, 2023 path. FK and IK concepts. [Source](https://help.autodesk.com/cloudhelp/2023/ENU/Maya-CharacterAnimation/files/GUID-360A07B4-9C74-4996-92EC-3BF4E9045DA3.htm)

[S33] Autodesk Maya character animation documentation, 2020 path. Skinning and weights. [Source](https://help.autodesk.com/cloudhelp/2020/ENU/Maya-CharacterAnimation/files/GUID-59BB9F41-8B3E-446F-83D3-9EE6810D17D1.htm)

[S34] Autodesk Maya character animation documentation under the observed 2027 path. Skinning methods; release availability not established from the label. [Source](https://help.autodesk.com/cloudhelp/2027/ENU/Maya-CharacterAnimation/files/GUID-CF2C698A-44BB-4CA0-BCB9-DB36500DA812.htm)

[S35] Khronos glTF Tutorials, A Simple Morph Target. Explanatory example, subordinate to the normative specification. [Source](https://github.com/KhronosGroup/glTF-Tutorials/blob/main/gltfTutorial/gltfTutorial_017_SimpleMorphTarget.md)

[S36] Autodesk Maya character animation documentation under the observed 2027 path. Constraints and limits; release availability not independently established. [Source](https://help.autodesk.com/cloudhelp/2027/ENU/Maya-CharacterAnimation/files/GUID-7665A291-FAA7-44C0-BDEB-A6C83482116C.htm)

[S37] Epic Games, IK Rig Animation Retargeting. Observed documentation version label is not a release certification. [Source](https://dev.epicgames.com/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine)

[S38] Unity 6000.0 manual, Meshes introduction. Render meshes and collision representations. [Source](https://docs.unity3d.com/6000.0/Documentation/Manual/mesh-introduction.html)

[S39] Unity 6000.0 manual, Transform component. Hierarchies and nonuniform-scale limitations. [Source](https://docs.unity3d.com/6000.0/Documentation/Manual/class-Transform.html)

[S40] Khronos, glTF 2.0 normative specification. Header identifies 2.0.1, 11 October 2021; current mutable content checked on the research date. Takes precedence over tutorial simplifications. [Source](https://registry.khronos.org/glTF/specs/2.0/glTF-2.0.html)

[S41] OpenUSD introduction, /release page. Scene composition and explicit non-rigging scope; observed 26.11 label is not independently verified release availability. [Source](https://openusd.org/release/intro.html)

[S42] Unity XR graphics documentation under observed 7000.0 path. Rendering optimization candidates, not a verified release recommendation. [Source](https://docs.unity.com/en-us/engine/7000.0/manual/xr/graphics)

[S43] Android Developers, GPU rendering for Unity XR. Target-dependent performance considerations. [Source](https://developer.android.com/develop/xr/unity/performance/gpu-rendering)

[S44] Unity mesh LOD troubleshooting under observed 7000.0 path. Deformation-aware LOD limitations; release label not independently verified. [Source](https://docs.unity.com/en-us/engine/7000.0/manual/analysis/graphics-performance-profiling/lod/mesh-lod/mesh-lod-troubleshooting)

[S45] Unity 6000.0 manual, Occlusion culling. Visibility optimization has its own computation and memory costs. [Source](https://docs.unity3d.com/6000.0/Documentation/Manual/OcclusionCulling.html)

### Production comfort accessibility and multiplayer

[S46] Meta, Comfort, updated 17 December 2025. Posture, distance interaction and view obstruction guidance. [Source](https://developers.meta.com/vr/design/comfort/)

[S47] Meta, Locomotion best practices, updated 17 December 2025. Movement choices and artificial-motion considerations. [Source](https://developers.meta.com/vr/design/locomotion-best-practices/)

[S48] W3C, XR Accessibility User Requirements, Working Group Note, 25 August 2021. User needs, explicitly not a conformance baseline or certification. [Source](https://www.w3.org/TR/xaur/)

[S49] Khronos OpenXR Guide, Frame Submission. Accessible conceptual guide; not a claim that the complete specification was audited. [Source](https://github.com/KhronosGroup/OpenXR-Guide/blob/main/chapters/frame_submission.md)

[S50] Epic Games, VR Performance Testing. Current page includes legacy engine examples; commands need version-specific checking. [Source](https://dev.epicgames.com/documentation/en-us/unreal-engine/vr-performance-testing-in-unreal-engine)

[S51] Unity 6000.0 documentation, Foveated rendering. Fixed and gaze-driven approaches and support considerations. [Source](https://docs.unity.com/en-us/engine/6000.0/manual/xr/graphics/foveated-rendering)

[S52] Unity 6000.0 documentation, VR frame timing. No absolute publication date inferred from relative update wording. [Source](https://docs.unity.com/en-us/engine/6000.0/manual/xr/graphics/vrframe-timing)

[S53] Unity Netcode for GameObjects 2.13, NetworkObject ownership. Authority model and ownership-transfer rules. [Source](https://docs.unity3d.com/Packages/com.unity.netcode.gameobjects@2.13/manual/components/core/networkobject-ownership.html)

[S54] Unity Netcode for GameObjects 2.7, Object visibility. Network replication visibility, not renderer occlusion; not a latest-version claim. [Source](https://docs.unity3d.com/Packages/com.unity.netcode.gameobjects@2.7/manual/basics/object-visibility.html)

[S55] Meta, Health and safety for shared spatial anchors, updated 4 September 2026. Colocated multiplayer risks and limitations. [Source](https://developers.meta.com/vr/design/mr-health-ssa/)

[S56] Meta, Avatar best practices. Gaze and personal-boundary considerations; publication date not established. [Source](https://developers.meta.com/vr/documentation/unity/meta-avatars-best-practices/)

[S57] Apple Developer, Adopting best practices for privacy in visionOS. Interaction results versus sensitive raw data and permission boundaries. [Source](https://developer.apple.com/documentation/visionOS/adopting-best-practices-for-privacy)

[S58] Apple Support, Safely use your Apple Vision Pro. Manufacturer safety guidance, not certification of an application or individual medical advice. [Source](https://support.apple.com/guide/apple-vision-pro/safely-use-your-apple-vision-pro-tanad808c142/visionos)
