# Blackwish congestion research reference

## Queueing AI inference and physical traffic

**Prepared for Blackwish review on 23 October 2026.** This reference explains how congestion forms, what different controls actually change, and how to assess a candidate improvement without mistaking a local gain for an end-to-end benefit. A separate language appendix covers catchphrases, scalloping and optional character mantras. Those editorial ideas are not traffic evidence.

**The central conclusion is to optimize useful completed outcomes within an explicit boundary, not admissions, utilization or visible queue length alone.** Local improvements can coexist with worse overall service.

### How to read this reference

Read the shared queueing models first, then the inference and physical-traffic applications. Transfer questions between domains, not equations or performance percentages without justification.

Each research area ends with **three distinct Point Bridge Path Shadow review passes**. Point states the proposition under review. Bridge connects it to evidence and scope. Path traces a bounded hypothetical case. Shadow records the nearby counterexample, protected loss or authority boundary. These are textual checks, not empirical trials or claims about a religious tradition.

### Evidence and decision status

- **Exact accounting identities** hold by their definitions when counts and boundaries are consistent.
- **Conditional models and approximations** require their stated assumptions; they are not universal predictions.
- **Published studies and operator documentation** support mechanisms and context-specific findings. Their results do not establish a measured benefit for Blackwish.
- **Hypothetical examples and architectural deductions** explain a claim or propose a candidate. They are not experimental results.
- **Language resources** distinguish exact source wording, owner meaning, original drafts and modified adaptations.

There is **no zero-wait promise**. Some buffering and batching may be useful; stability alone does not establish acceptable delay. The relevant questions are whose work finishes, when it finishes, what is rejected or displaced, and whether quality, fairness, safety and agency remain protected.

### Authorization boundary

This document contains educational research and bounded text analysis. It does not implement a generator, alter a live system, conduct experiments on people, or authorize deployment. Candidate policy, code, traffic-control or wording revisions remain subject to the user's explicit manual ratification. Accepting a phrase version is not blanket approval for every use of it.


<!-- pagebreak -->

## Queueing foundations and congestion controls

**Core conclusion:** A queue can absorb a temporary mismatch between arrivals and service, but it cannot create sustained processing capacity. Low waiting time requires a combination of spare capacity, less variability, less unnecessary work, and explicit overload policy - not simply bigger queues.

### Establish the accounting boundary first

Record separately:

- **Offered demand:** original requests/jobs attempted.
- **Admitted demand:** work accepted into this particular system.
- **Attempts:** originals plus retries.
- **Successful completions:** useful outcomes, not merely dequeued messages.
- **Other exits:** rejection, abandonment, expiration, cancellation, failure.

**Accounting identity, not a stochastic assumption:**  
= N(t) = N(0) + A_admitted(t) - D_all_exits(t)

N is the number of jobs present, A_admitted counts cumulative admissions, and D_all_exits counts cumulative exits of every kind. A smaller internal queue can reflect rejection or migration of waiting elsewhere rather than genuinely better service. Preserve end-to-end measurements, including the upstream waiting room.

For suitable long-run averages, **Little’s law** is

= L = λ_eff W        and        L_q = λ_eff W_q

Here λ_eff is the long-run flow rate for the chosen population. Use the same population, boundary, units and averaging regime throughout. L includes service; L_q excludes it. W is total time within the boundary; W_q is waiting before service. No Poisson/exponential assumption is required. The familiar steady-state interpretation requires a stable regime and appropriate finite averages; naive multiplication of short-window arrival rate by completed-job latency can fail during accumulation, drain-down or censoring. [MIT queueing lecture](https://web.mit.edu/1.041/www/lectures/L8-queuing-models-2026sp.pdf)

### Why utilization and variability create long waits

Here λ is the arrival rate, μ is the service rate, S is service time, and ρ is utilization. For a stable **M/M/1** queue - Poisson arrivals, independent exponential service, one server - with ρ = λ/μ < 1:

= E[W_q] = [ρ / (1 - ρ)] E[S]        and        E[W] = 1 / (μ - λ)

For a conventional independent-renewal, single-server FCFS **GI/GI/1** model with finite variances, the useful Kingman-style approximation is

= E[W_q] ≈ [(c_a² + c_s²) / 2] × [ρ / (1 - ρ)] × E[S]

where c_a and c_s are coefficients of variation of interarrival and service times. This is a mean-wait approximation, especially motivated by heavy traffic - not an exact formula for arbitrary correlated, batched, multi-server traffic or latency percentiles. The MIT notes explicitly assume utilization below one and an unbounded waiting room. [MIT queueing notes, pp. 2-4](https://ocw.mit.edu/courses/15-763j-manufacturing-system-and-supply-chain-design-spring-2005/22f4805864deb06eee85acc1601463ba_queueing_note.pdf)

**Calculated illustration, not a measured benchmark:** Under M/M/1, increasing utilization from 50% to 80%, 90% and 95% changes mean queue wait from 1 to 4, 9 and 19 mean-service-time units. This does **not** establish a universal recommended utilization percentage.

**Important counterexample:** Perfectly spaced deterministic arrivals with deterministic service shorter than the interarrival interval can have zero waiting at high utilization. Therefore “high utilization always causes long waits” is false without variability/model qualifications.

### Capacity and backlog recovery

**Derived fluid approximation:** If backlog is B jobs, arrivals remain λ, and effective completion capacity is C > λ,

= T_drain ≈ B / (C - λ)

This assumes comparable job costs and roughly constant rates. With heterogeneous work, express backlog and rates in service-work units instead. If C ≤ λ, the backlog cannot drain while those conditions persist.

Likewise, for stage i, a useful first-pass workload measure is

= ρ_i = λ_0 v_i E[S_i] / m_i

where λ_0 is the original-job arrival rate, v_i is expected visits per original job and m_i is equivalent parallel capacity. This is a screening calculation, not a sufficient stability theorem for arbitrary queueing networks. Locks, shared dependencies, scheduling, blocking and rework can invalidate simple independent-stage assumptions.

**Bounded counterexample:** Adding front-end workers does not improve a fixed-capacity database bottleneck. It may instead increase outstanding database work. A queue-length cap bounds occupancy, not necessarily waiting time: a stalled dependency can hold the oldest item indefinitely.

### Packet network congestion a related but distinct layer

For network queues, **active queue management (AQM)** signals congestion through drops or ECN marks before buffers stay full. It complements endpoint congestion control and fair scheduling. Larger buffers can absorb bursts but also add persistent delay; deleting buffers altogether sacrifices burst absorption. RFC 7567 recommends AQM without prescribing one universally correct algorithm, and distinguishes queue management from scheduling fairness. Do not assume application queue controls replace transport/network controls. [IETF RFC 7567](https://www.rfc-editor.org/rfc/rfc7567.html)




### Controls and their actual effects

| Mechanism | Useful effect | Failure mode or qualification |
|---|---|---|
| Admission or concurrency limits | Prevent excessive work entering the constrained resource | Move waiting upstream; count refused demand |
| Backpressure | Make upstream producers respond to downstream capacity | Nonresponsive producers merely overflow another buffer |
| Load shedding | Preserve useful service during overload | Reduces admitted demand, not offered demand; requires explicit service policy |
| Isolation/fair scheduling | Protect tenants or classes from noisy neighbors | Reservations can strand capacity; priorities can injure low-priority service |
| Deadline propagation | Avoid spending resources after results cease to be useful | Client timeout alone does not guarantee server work stops |
| Bounded retries with jitter | Recover transient faults without synchronized retry bursts | Cannot remedy sustained insufficient capacity |
| Caching/coalescing | Avoid repeated expensive work | Cold caches, stale results and simultaneous misses can reverse the benefit |
| Scaling | Adds effective service capacity where scalable | Startup delay, shared dependencies and contention may limit gain |

**Operational evidence - Google:** Request counts are a poor capacity proxy when request costs differ. Google’s overload guidance describes resource-aware controls, degraded responses, quick rejection and client-side throttling. Rejection itself consumes resources; protecting the server may require stopping work before it reaches that server. Fleet-wide overload is different from one overloaded replica: retrying elsewhere only helps if spare capacity actually exists. [Google SRE: Handling Overload](https://sre.google/sre-book/handling-overload/)

**Operational evidence - AWS:** Asynchronous acceptance latency can look healthy while useful processing is far behind. AWS recommends observing message age and distinguishing first-attempt age from retry effects. Tenant isolation and separate queues can prevent one workload monopolizing resources. Prioritizing fresh work or expiring stale work is appropriate only where application semantics permit; mandatory work cannot simply disappear. [AWS: Avoiding insurmountable queue backlogs](https://d1.awsstatic.com/builderslibrary/pdfs/avoiding-insurmountable-queue-backlogs.pdf)

**Retries:** Apply bounded attempts, a retry budget, backoff and jitter, and retry only safe/idempotent operations. A timeout does not prove the original side effect failed. Retries at multiple call-stack layers multiply work: with three attempts at each of five nested layers, the worst-case leaf amplification is 3⁵ = 243, a conditional combinatorial example rather than a typical observed rate. [AWS: Timeouts, retries, and backoff with jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/)

**Deadlines:** Propagate the remaining time budget rather than granting every dependency a fresh full timeout. gRPC documents that application code must stop its spawned work after noticing cancellation; deadline expiry is not magical cleanup of arbitrary computation. [gRPC deadlines](https://grpc.io/docs/guides/deadlines/)

**Caching:** Evaluate downstream misses, not just headline hit rate. Request coalescing can prevent many identical misses from launching duplicate work. Cold starts and fleet-wide cache loss require a separate overload plan. Freshness and privacy constraints remain binding. [AWS: Caching challenges and strategies](https://aws.amazon.com/builders-library/caching-challenges-and-strategies/)



### Diagnosis before recommending a change

**Proposed analysis protocol, not deployment authorization:**

1. Map each handoff, queue, pool, dependency and retry path.
2. Measure latency, traffic, errors and saturation; distinguish successful-request latency from fast failures. Look at distributions rather than averages alone. [Google SRE monitoring](https://sre.google/sre-book/monitoring-distributed-systems/)
3. Add queue wait/service decomposition, oldest-item age, work-weighted backlog, retry amplification, rejection/expiry counts and per-class results.
4. Plot arrivals and service demand across multiple timescales. Daily averages conceal bursts; identical request rates can carry different work.
5. Identify whether delay comes from excessive demand, slow service, uneven routing, contention, synchronized arrivals or obsolete work.
6. Compare candidate changes using an offline model or existing traces, preserving correlations and job-size mix where possible. Treat results as model-dependent, not proof of production benefit.
7. Evaluate useful completions within deadline, tail latency, errors and fairness together. Do not celebrate low latency achieved solely by rejecting difficult work.
8. Prepare a manually ratifiable proposal with assumptions, expected trade-offs, rollback conditions and unresolved evidence.

Google’s cascade analysis provides the mechanism to watch for: overload causes replicas to fail or requests to retry, which pushes more work onto surviving capacity. Extra concurrency can therefore decrease useful throughput rather than rescue it. [Google SRE: Addressing Cascading Failures](https://sre.google/sre-book/addressing-cascading-failures/)




## Three queueing review passes

### Pass One Evidence and model scope

**Point.** High utilization is a risk factor for waiting in variable workloads, not a universal proof of delay.

**Bridge.** M/M/1 and the Kingman approximation expose how spare capacity and variability interact under specified assumptions. Little's law instead relates consistent averages; it neither chooses a scheduling policy nor predicts a latency percentile by itself.

**Path.** Consider a hypothetical single server whose mean service time is one unit. Under M/M/1, moving from 50 percent to 90 percent utilization changes the calculated mean wait from one to nine service-time units. This example explains nonlinear sensitivity. It does not identify Blackwish's arrival distribution or justify a universal utilization target.

**Shadow.** Perfectly regular arrivals spaced just beyond a fixed service duration can produce zero queueing at high utilization. Conversely, a stable queue can still be too slow, and some heavy-tailed settings have unbounded mean wait despite load below one. The bounded conclusion is to measure variability, service mix and tails before transferring a model. Zero waiting remains a special case, not a promise.

### Pass Two End to end outcomes and protected loss

**Point.** A smaller visible queue is not necessarily a better system.

**Bridge.** Reconcile offered demand, admitted work, attempts, all exits and useful completions across the same boundary. Preserve unsuccessful requests and excluded classes in the evaluation rather than measuring only fast successes.

**Path.** In a hypothetical overloaded service, a new admission cap makes the internal queue shorter. Some requests now wait at a gateway and others are refused. The text-level comparison asks whether useful on-time completions increased, whether total waiting decreased, and whether a previously served class lost access. Without those counts, the internal-queue chart is inconclusive.

**Shadow.** Admission control may still be valuable when it prevents collapse and preserves service for admitted work. It need not reduce every person's wait to be useful. Its costs must remain visible: rejected mandatory work needs a defined disposition, and a policy that protects one class can harm another. Fairness is a stated objective, not an inference from a low average. Size-aware scheduling also does not necessarily harm all large jobs; the result depends on workload and policy. [SRPT fairness analysis](https://www.cs.cmu.edu/~harchol/Papers/jss.pdf).

### Pass Three Authority reversibility and recovery

**Point.** A plausible congestion mechanism is not authority to change a live system.

**Bridge.** A candidate should name the constrained resource, assumptions, intended effect, failure signals, owner, rollback path and work that must not disappear. Separate retry safety from retry quantity; a timeout alone does not establish that a side effect failed.

**Path.** A proposed retry budget is checked on paper against a nested call chain. Three total attempts at each of five layers permit a worst-case 3⁵ = 243 leaf attempts. Centralizing the retry policy could reduce amplification, but the proposal must also account for recoverable transient failures and operations whose effects are not safely repeatable.

**Shadow.** Turning retries off indiscriminately may sacrifice useful recovery. A queue cap does not impose a time limit on a stalled dependency. A cancellation signal does not automatically stop every child operation. These conditions belong in a manually ratifiable design; the present review authorizes neither implementation nor a live trial.


<!-- pagebreak -->

## AI inference traffic and serving

Optimize **useful, correct requests completed within latency objectives (“goodput”)**, not requests admitted, peak tokens/s, GPU utilization, or cache-hit rate independently. Congestion may sit in admission, prefill, decoding, KV memory, networking, retrieval, or CPU orchestration; speeding the wrong stage merely moves the queue.

**Scope:** literature and official documentation reviewed October 23, 2026. No live changes or tests. Hardware, model, engine version, traffic distribution, and latency targets are unknown; recommendations below are conditional, not deployment instructions.

LLM means large language model; KV is the key-value attention state retained for generation. GPU refers to the accelerator, SLO to a service-level objective, and QPS to requests per second.

### What makes inference traffic unusual

- **Arrival rate is insufficient.** Ten short chats and ten long-document reasoning requests impose very different compute, memory, and residence time.
- **Prefill and decode compete differently.** Prefill processes input tokens in parallel; autoregressive decoding repeatedly advances active sequences. “Prefill compute-bound/decode memory-bound” is a useful starting approximation, not a universal classification for every model, batch, context length, and accelerator.
- **Output length is unknown at admission.** Requests accumulate KV state as they generate; admitting a batch that initially fits does not mean it will remain comfortably within memory limits.
- **Bursts and correlated arrivals matter.** Agent fan-out, synchronized background tasks, retries, and users arriving after a release can create very different queues from constant or independent synthetic arrivals.
- **Request populations differ.** Interactive chat, long-context extraction, code generation, multimodal inputs, and background summarization should not be assumed to share one service-time distribution.

The primary **BurstGPT** dataset contains 5.29 million traces over 121 days and documents burstiness, request/response-length relationships, failures, and workload-dependent optimization performance. It supports realistic trace-based evaluation rather than assuming one benchmark transfers everywhere. [BurstGPT](https://arxiv.org/abs/2401.17644)

### Measure the right delay

Instrument request arrival, admission, prefill start/end, first visible token, stream gaps, completion, cancellation, and rejection.

| Measure | What it reveals - and does not |
|---|---|
| Queue time | Time waiting before engine service; distinguish gateway, router, and engine queues |
| Time to first token (TTFT) | User’s initial wait, including relevant preprocessing, queueing, prefill, and delivery |
| Inter-token latency (ITL) | Streaming stalls; inspect tail gaps, not only averages |
| Time per output token (TPOT) | Average generation pace; may hide individual long pauses |
| End-to-end completion | Whether the actual task finished promptly; sensitive to output length |
| Goodput | Completion rate satisfying explicitly defined latency and correctness requirements |

Report p50/p95/p99 by workload class and prompt/output-length bucket, plus rejection, timeout, and cancellation rates. Otherwise a “faster” system may simply reject difficult requests or exclude failures from its chart. Current vLLM exposes queue, prefill, decode, end-to-end, TTFT, ITL, and TPOT metrics. [vLLM production metrics](https://docs.vllm.ai/en/latest/usage/metrics/)



### Bottleneck diagnosis

These are diagnostic hypotheses, not proofs from symptoms alone.

| Observation | Check first | Candidate remedy |
|---|---|---|
| TTFT rises while existing streams remain smooth | Admission and prefill queues; uncached prompt volume | Reduce redundant prefill; reserve interactive capacity; constrain background admissions |
| Streams pause when long prompts arrive | Prefill/decode interference | Chunked prefill; evaluate separate prefill/decode resources |
| Preemption or recomputation rises | Active sequence lengths and KV occupancy | Lower simultaneous admissions; budget KV growth; reduce needless context |
| GPU is lightly busy but requests wait | CPU/tokenization, retrieval, remote KV, synchronization, network | Optimize or bypass the measured upstream/I/O constraint |
| One replica is overloaded while others are free | Cache affinity and length-blind routing | Balance estimated remaining work against cache benefit |
| Queue grows during scale-out | Model loading/warm-up lag and burst duration | Warm capacity and demand-aware admission; scaling alone may arrive too late |
| Timeouts cause even more traffic | Retried attempts still running | Propagate cancellation and use bounded retry budgets |



### Remedies and their failure cases

**Continuous/in-flight batching.** Refill batch slots when sequences finish rather than waiting for the longest sequence. This helps mixed-length traffic, but larger batches do not automatically improve per-user latency. NVIDIA explicitly distinguishes aggressive utilization from conservative no-eviction scheduling: aggressive admission can force pause/resume when KV capacity is exhausted. [TensorRT-LLM scheduling](https://github.com/NVIDIA/TensorRT-LLM/blob/main/docs/source/legacy/performance/performance-tuning-guide/useful-runtime-flags.md)

**Chunked prefill.** Break large prompt processing into pieces so it does not monopolize execution between decode steps. Current vLLM documentation says smaller token budgets favor ITL; larger budgets can favor TTFT. It also documents KV-pressure preemption and recomputation, and warns additional parallelism can introduce synchronization or latency costs. Avoid copying numeric tuning defaults across hardware. [vLLM optimization](https://docs.vllm.ai/en/latest/configuration/optimization/)

**Prefill/decode disaggregation.** Separate pools permit different resource allocations and reduce phase interference, but add KV-transfer work and require balanced capacity between stages. DistServe established strong measured benefits under its workloads and SLOs; its speedups are not general guarantees. [DistServe, OSDI 2024](https://arxiv.org/abs/2401.09670)

The later TaiChi paper specifically argues that aggregation versus disaggregation depends on the relative TTFT and TPOT constraints; neither wins universally. This is research evidence against treating disaggregation as an unconditional upgrade. [TaiChi, 2025](https://arxiv.org/abs/2508.01989)

**Prefix caching.** Reuse genuinely identical prompt prefixes to avoid repeated prefill. It does not eliminate generation of new output. Keep stable material before variable material where semantically appropriate; do not distort prompt correctness merely to chase hits. [vLLM automatic prefix caching](https://docs.vllm.ai/en/latest/features/automatic_prefix_caching/)

**Cache-aware routing.** Choose between saved prefill and extra queueing: the highest-hit worker may not finish first. NVIDIA’s router considers both reusable KV state and projected active load. [Dynamo router](https://docs.nvidia.com/dynamo/dev/knowledge-base/modular-components/router/overview)

A useful August 2026 **preprint**, CacheRoute, reports improved SLO throughput in its main setup but explicitly documents two workloads where affinity’s residual imbalance reduced or erased the benefit. [CacheRoute](https://arxiv.org/abs/2608.19677)

**Remote KV caching is not free.** An October 15, 2026 **preprint** reports an especially instructive counterexample: on one GLM-5.3/8×B300/LMCache-Valkey configuration, a remote cache hit took 0.88 seconds versus 0.31 seconds to recompute; synchronous loading produced long queues despite low GPU activity. The general lesson is to compare transfer-plus-access overhead against saved compute - not to reuse its numerical threshold elsewhere. [When the KV Cache Is Slower Than the GPU](https://arxiv.org/abs/2610.21500)

**Speculative decoding.** A draft mechanism proposes tokens that the target verifies. Its payoff depends on acceptance, verification overhead, model, sampling, hardware, and load. Current vLLM particularly describes the medium-to-low-QPS, memory-bound latency case and warns that real gains are workload-dependent. Exactness guarantees must be checked for the selected method; not every variant is lossless. [vLLM speculative decoding](https://docs.vllm.ai/en/latest/features/speculative_decoding/)

**Fair admission and cancellation.** Meter estimated input/output work and memory, not request count alone. Reserve an interactive share, give background work bounded service rather than starvation, and age waiting jobs. VTC provides a research basis for token-cost fairness under continuous batching. [Fairness in Serving LLMs](https://arxiv.org/abs/2401.00588)

Ensure cancellation reaches the engine rather than merely stopping UI display. vLLM documents explicit abort operations. [vLLM abort API](https://docs.vllm.ai/en/latest/serving/online_serving/token_in_token_out/)

**Autoscaling.** Use queued prompt work, KV pressure, and latency objectives with startup lag and capacity ceilings. Inspect actual scale-down behavior: current NVIDIA **development documentation** warns its planner can terminate workers without draining in-flight work. This is version-specific, but illustrates why “autoscaling enabled” is not enough. [Dynamo planner tuning](https://docs.dynamo.nvidia.com/dynamo/dev/kubernetes/auto-deployment/dynamo-planner)



### Candidate Blackwish architecture implications

These are architectural deductions, not claims about an inspected Blackwish implementation:

1. **Do not route static reference lookup through an LLM.** Deterministic indexed lookup can return canonical text, IDs, versions, and citations directly. Reserve generation for interpretation or synthesis.
2. **Separate interactive and background work.** A requested answer should not sit behind bulk indexing, exhaustive consistency exploration, or speculative agent fan-out.
3. **Preserve provenance and stale context explicitly.** Store source version, retrieval time, content hash, and applicable authority. Cached text or a fast answer is not evidence that the underlying fact is current.
4. **Bound generated work.** Use task budgets, cancellation, duplicate suppression, and limits on concurrent branches; do not convert every ambiguity into simultaneous model calls.
5. **Prepare an offline comparison, not an automatic rollout.** Compare candidate scheduling policies against representative trace mixes, including bursts, long outputs, poor cache locality, and memory pressure. Report fairness, failures, and quality alongside latency. Deployment remains subject to manual ratification.


## Three inference review passes

### Pass One Evidence and model scope

**Point.** Reducing repeated prefill can help, but a cache hit is not a completion-time guarantee.

**Bridge.** Prefix caching avoids work only for genuinely reusable prefixes. Saved compute must be compared with lookup, transfer, synchronization and the selected worker's queue. Deployment-specific papers and current engine documentation do not supply universal thresholds.

**Path.** Consider two hypothetical replicas. One has the prefix cached but a long queue; the other would recompute it immediately. A cache-only router selects the first. A completion-aware comparison includes both waiting and remaining work, so the second could finish sooner. No numerical speedup is asserted.

**Shadow.** For a long reusable prefix and a lightly loaded nearby cache, affinity can be valuable. The lesson is not to disable caching; it is to test the scope of the benefit. The remote-cache preprint's timings describe one configuration and must not be recast as a hardware-independent law.

### Pass Two End to end outcomes and protected loss

**Point.** Higher tokens per second can coexist with worse user service.

**Bridge.** Define goodput using explicit correctness and latency requirements. Keep TTFT, streaming gaps and completion time distinct, and include rejected, expired and cancelled requests. Compare workload classes rather than collapsing long and short tasks into one average.

**Path.** A hypothetical batch policy admits more long requests. Aggregate GPU utilization rises, but interactive streams pause and memory pressure forces recomputation. A second policy admits fewer simultaneous requests and preserves interactive response. Neither policy can be declared superior without its workload, quality constraints, background service bounds and rejected-demand counts.

**Shadow.** Background work is not worthless because it is noninteractive. Strict interactive priority can starve it; unlimited fairness reservations can strand capacity. Useful review asks which class is protected, which delay is tolerated, and whether each class has a visible service commitment. A fast first token is not proof that the actual task finished.

### Pass Three Authority reversibility and recovery

**Point.** Serving optimizations are candidates until the relevant engine behavior and authority are established.

**Bridge.** The same name can conceal different version-specific behavior. Batching, speculative decoding, worker scale-down and cancellation require attention to memory growth, output correctness, unfinished work and rollback.

**Path.** A paper design separates interactive generation from background indexing and sets a bounded concurrency budget. Its review asks what happens when the user cancels, when a worker drains, when a cache is cold, and when output exceeds the estimated length. An offline trace comparison could later test the candidate if authorized; this report does not claim to have run one.

**Shadow.** Partitioning capacity can waste resources, and a scale-down action may terminate useful in-flight work if the engine does not drain it. Speculation is not automatically lossless across methods. Static reference lookup may avoid unnecessary inference, but generated interpretation still needs provenance. Manual ratification must specify the exact revision and allowed environment before implementation or deployment.


<!-- pagebreak -->

## Physical traffic and network congestion

Research completed 23 October 2026. Primary-source web research using FHWA, FTA, USDOT, original research, and an original-paper translator's academic site. This section concerns road traffic, transit, freight, and people/goods movement - not criminal trafficking. Findings and hypothetical analyses do not authorize traffic-control changes or experiments on people.

### Main finding

Alleviate congestion by controlling where and when demand meets effective receiving capacity, not by maximizing local speed, admissions, or occupied space. A faster upstream stage can worsen the whole network if its output blocks downstream intersections, ramps, loading bays, or shared resources.

### Physical structure and assumptions

With consistent aggregation, q = k × v_s: traffic flow equals density times space-mean speed. This does not imply maximizing either density or speed independently. Flow can decline at excessive density. Fundamental diagrams are model families rather than universal fixed curves; critical density and capacity depend on conditions such as merging, vehicle composition, geometry, weather, and incidents. [FHWA freeway-flow discussion](https://ops.fhwa.dot.gov/freewaymgmt/publications/frwy_mgmt_handbook/chapter1_02.htm); [FHWA alternative fundamental diagrams](https://ops.fhwa.dot.gov/publications/weatherempirical/sect3.htm).

Distinguish:

- Demand from observed throughput: low discharge can indicate severe congestion rather than low demand.
- Storage from discharge capacity: more queuing space may prevent spillback without increasing completions per hour.
- Visible queue from binding bottleneck: FHWA describes an active bottleneck as one whose discharge is not constrained by a downstream queue. [FHWA bottleneck classification](https://ops.fhwa.dot.gov/bn/bnchart.htm).

Capacity drop means lower discharge following breakdown relative to pre-breakdown capacity. Measure it rather than assuming a universal percentage. A research model explicitly incorporating capacity drop finds consequences for ramp-meter optimization, conditional on its assumptions. [Capacity-drop modeling paper](https://arxiv.org/abs/2106.10347).

Transfer to workflows/inference: measure completed work and downstream blocking, not only starts or busy workers. Boundary: physical vehicles occupy space and obey safety/headway constraints; digital systems do not inherit road-flow equations simply because both have queues.



### Interventions and limits

#### Protect receiving capacity

Ramp metering spaces entering vehicles and regulates entrance demand to reduce disruptive merging and breakdown. Evaluation must include ramp waiting rather than only mainline speed. Environmental estimates depend on actual ramp operations and modeling assumptions. [FHWA ramp-metering mechanism and evaluation](https://ops.fhwa.dot.gov/publications/fhwahop14020/sec1.htm).

The queue must have a safe place to wait. Short ramps, inadequate acceleration length, restricted sight distance, and spillback onto streets can make control unsuitable. Distributional effects differ for those already on the freeway and those entering later. [FHWA ramp-metering challenges](https://ops.fhwa.dot.gov/publications/fhwahop14020/sec2.htm).

Transfer: bounded admission/backpressure can protect productive operation. Counterexample: a limiter that simply moves identical waiting outside the measured boundary has not demonstrated end-to-end improvement.

#### Coordinate signals compare against a competent baseline

Check detector health, timing adequacy, turning movements, and downstream storage first. Adaptive control depends on reliable detection. FHWA notes that some comparisons find no significant improvement over well-tuned conventional timing; variable conditions are a more plausible source of additional value. Do not transplant improvement percentages from a poor baseline to another corridor. [FHWA adaptive-control guidance](https://ops.fhwa.dot.gov/publications/fhwahop08024/chapter9.htm).

A local controller should not discharge traffic into a blocked downstream link. Include cross streets, pedestrians, transit, and queue tails in evaluation. A more recent program-level reference is the [FHWA Traffic Signal Program Handbook](https://ops.fhwa.dot.gov/publications/fhwahop23041/fhwahop23041.pdf).

#### Recover from incidents

Roadway clearance (all lanes available), incident clearance (last responder leaves), and return to normal flow are separate endpoints. [FHWA incident timeline](https://ops.fhwa.dot.gov/publications/fhwahop15007/chapter1.htm).

Hypothetical - not an empirical estimate: after reopening, a 600-vehicle queue with discharge of 1,800 vehicles/hour and arrivals of 1,600/hour drains at 200/hour and takes approximately three hours to clear, assuming constant rates and no additional restrictions. If arrivals equal discharge, the existing queue does not drain.

Prioritize safe coordinated response and secondary-crash prevention, not pressure to meet an isolated clearance-time target. [FHWA Traffic Incident Management](https://ops.fhwa.dot.gov/tim/).

#### Manage demand and choice

Time-shifting, pricing, alternatives to driving, and freight scheduling can change demand at constrained times/places. Examine who can actually change schedule, route, or mode; pricing without usable alternatives can burden access. Revenue use and distributional effects belong in the intervention design. [USDOT road-pricing overview](https://www.transportation.gov/sites/dot.gov/files/2025-01/Road%20Pricing.pdf).

Duranton and Turner found vehicle-kilometers traveled rose approximately proportionately with interstate highways across U.S. cities. This challenges treating road expansion as a durable congestion cure; it does not prove every project has zero benefit, or that transit lacks accessibility value. Their transit/VKT finding concerns the studied aggregate outcome and setting. [The Fundamental Law of Road Congestion](https://www.nber.org/papers/w15376).



### Two different network effects

Induced demand: supply changes travel choices and eventually activity/location patterns.

Braess's paradox: even at fixed demand, adding a route can worsen user-equilibrium travel time when independently chosen routes have flow-dependent costs. Not every added road causes this effect. [Original-paper translation/background from its co-translator](https://supernet.isenberg.umass.edu/braess/braess-new.html).

Toy example, not observed road data: 4,000 travelers choose two routes, each containing one link costing x/100 minutes at flow x and one constant 45-minute link. An even split costs 20 + 45 = 65 minutes. A zero-time connector between the congestion-sensitive links can induce equilibrium with everyone traversing both, costing 40 + 40 = 80 minutes.

Bound: with unchanged demand/constraints and a central optimizer allowed to leave the new link unused, the added optional link cannot worsen the best attainable solution. Harm comes from the equilibrium/control situation.

### People and freight use the right success metric

An apparently empty bus lane can carry more people than a full car lane. Person throughput, door-to-door time, reliability, access, and passenger waiting often matter more than vehicles/hour. Benefits depend on passenger loads, stops, loading activity, and turning conflicts. [FTA bus-lane guidance](https://www.transit.dot.gov/research-innovation/bus-lanes).

Priority can be conditional on lateness rather than indiscriminate, favoring adherence and passenger waiting rather than solely running time. [FTA signal-priority guidance](https://www.transit.dot.gov/research-innovation/signal-priority).

Freight requires end-to-end diagnosis: road arrival, gate processing, yard movement, dock service, unloading, receiver availability, departure. Candidate measures include loading-zone management, off-hour delivery, reservations, modal shift, and consolidation. Off-hour delivery can introduce receiver-staffing, noise, security, and worker-condition constraints. [FHWA urban-freight primer](https://ops.fhwa.dot.gov/Publications/fhwahop18020/index.htm); [FHWA curb/freight benefits](https://ops-dr.fhwa.dot.gov/publications/fhwahop18020/benefits.htm).

Evidence-quality caution: the USDOT virtual-gate headline describing a 20% drayage turn-time reduction comes from feasibility analysis of candidate solutions under representative scenarios, not a universally observed deployment effect. [USDOT methodology](https://www.itskrs.its.dot.gov/2024-b01820).



### Physical traffic diagnosis by mechanism

This diagnostic guide is analytical synthesis, not a deployment specification.

#### Merge breakdown
**Measure first.** Upstream/downstream flow, speed, occupancy, discharge before/after breakdown, ramp arrivals. **Candidate treatment.** Metering, merge/geometry treatment, smoothing. **Failure check.** Mainline improvement but worse total delay or unsafe ramp spillback.

#### Downstream spillback
**Measure first.** Queue-tail location, storage occupancy, blocked movements, receiving capacity. **Candidate treatment.** Coordinated release; protect intersections; treat downstream bottleneck. **Failure check.** Congestion merely moved beyond sensors.

#### Signal mismatch
**Measure first.** Turning counts, phase failures, detection health, pedestrian/transit delay. **Candidate treatment.** Repair detection; retime; assess adaptive control. **Failure check.** Gain absent against tuned baseline or excluded users harmed.

#### Incident unreliability
**Measure first.** Detection, response, road/incident clearance, full recovery, secondary crashes. **Candidate treatment.** Coordinated incident management. **Failure check.** Faster nominal clearance without safer response or network recovery.

#### Persistent overload
**Measure first.** Origin/destination and time-of-day demand, affordability, alternatives, access. **Candidate treatment.** Demand shift; equitable pricing; transit/service alternatives. **Failure check.** Counted trips fall through exclusion or displacement.

#### Transit delay
**Measure first.** Loads, headways, bunching, waiting, transfers, door-to-door time. **Candidate treatment.** Priority; lane protection; stop/boarding changes. **Failure check.** Vehicle throughput improves while passenger access/time worsens.

#### Terminal and warehouse queue
**Measure first.** Arrival profile, service variability, appointment adherence, dock/yard occupancy, total driver time. **Candidate treatment.** Appointment smoothing; pre-processing; staffing; staging. **Failure check.** Gate waits move off-site or become unpaid driver time.

#### Last mile blockage
**Measure first.** Loading dwell, curb occupancy, double parking, walking/cycling conflicts, receiver windows. **Candidate treatment.** Loading zones; reservations; consolidation; suitable windows. **Failure check.** Delivery speed imposes unsafe conflicts, noise, or access burdens.


Declare network boundary and observation period covering queue buildup and drainage. Track median/tail travel time, completed trips/person movements, total waiting, safety, accessibility, and distribution across groups. [FHWA adaptive-control validation guidance](https://ops.fhwa.dot.gov/publications/fhwahop13031/index.htm) includes percentile travel times and reliability measures.



## Three physical traffic review passes

### Pass One Evidence and model scope

**Point.** Adding a route can worsen travel time in some networks, but not in every network or under every controller.

**Bridge.** Braess's paradox concerns route choice with flow-dependent costs. Induced demand is a different mechanism in which added supply changes travel choices and, over time, activity or location patterns. Neither can be inferred merely from observing a busy new road.

**Path.** The earlier 4,000-traveler example holds demand fixed. A connector changes individually attractive route choices and produces an equilibrium of 80 minutes rather than 65. This is a toy mathematical case, not an observation about an actual road or a prediction for Blackwish.

**Shadow.** If a central optimizer may leave the new optional link unused and all other constraints are unchanged, the best attainable outcome cannot be worse simply because the link exists. Likewise, the cited induced-demand study does not show that every road project has zero value or that transit lacks accessibility benefits. Identify the decision model and the measured outcome before transferring either result.

### Pass Two End to end outcomes and protected loss

**Point.** To move more through a bottleneck, it can help to admit less at that moment.

**Bridge.** Ramp metering may protect mainline discharge by limiting disruptive merges and breakdown. The evaluation boundary must include ramp queues, connecting streets, total journey time, safe storage and people who cannot easily change routes or schedules.

**Path.** A hypothetical ramp meter improves freeway speed but stores a longer queue on a short ramp. If that queue blocks a local street, the apparently successful mainline metric hides a new constraint. A complete comparison includes both queue locations, safety exposure and distribution of delay; no mainline gain alone establishes success.

**Shadow.** Below saturation, needless metering may simply add delay. Conversely, some additional ramp waiting may be justified by a larger network benefit if safety and distribution are explicitly addressed. Passenger throughput can also contradict appearances: a sparse-looking bus lane may carry more people than a crowded car lane, but reservation alone does not create passenger demand.

### Pass Three Authority reversibility and recovery

**Point.** Restoring a lane or changing a signal is not the same as restoring safe network flow.

**Bridge.** Roadway clearance, incident clearance and full traffic recovery are different milestones. A candidate intervention must account for downstream receiving capacity, pedestrian and transit movements, emergency access, sensor reliability and a competent baseline.

**Path.** In the hypothetical incident example, a 600-vehicle queue with 1,800 vehicles per hour of discharge and 1,600 arrivals per hour needs about three hours to drain. Opening the lane does not erase accumulated vehicles. The calculation assumes constant rates and no new restriction; it is not a response-time target.

**Shadow.** Evacuation is not ordinary congestion minimization. Changing hazards, safe destinations, people needing assistance and emergency access require specialized authorized planning. Simulated improvement does not justify a live traffic-control change. This document offers text analysis only; any implementation or operational experiment needs explicit manual ratification and appropriate real-world authority.


## Cross domain conclusions and candidate decisions

The shared structure is a mismatch between arriving work and usable capacity, magnified by variability, blocking, repeated work or incentives. The physical meaning differs. Jobs can be cancelled or deduplicated; vehicles occupy space and cannot be treated as disposable messages. Tokens consume phase-specific compute and memory; completed trips concern people, access and safety. An analogy is useful only while these differences remain explicit.

### A common comparison frame

| Question | Evidence to preserve |
|---|---|
| What enters | Offered demand, admission decisions and repeated attempts |
| Where it waits | Every relevant queue, upstream waiting and downstream blocking |
| What consumes capacity | Service-work mix, memory or storage occupancy and shared dependencies |
| What finishes | Useful, correct completions within the defined objective |
| What leaves otherwise | Rejection, cancellation, expiration, abandonment and failure |
| Who loses | Per-class delay, access, safety, fairness and other protected outcomes |
| What changes over time | Buildup, scale or response lag, drainage, warm-up and recovery |

### What the research supports proposing

**Avoid unnecessary work before accelerating it.** Candidates include deterministic retrieval of canonical text, duplicate suppression, safe request coalescing and removal of expired work where the task permits. This is conditional: mandatory work cannot be discarded solely to improve a metric, and cached answers still require correctness and freshness controls.

**Control admission near the actual constraint.** Concurrency limits, ramp meters and bounded batches can preserve useful operation. Their evaluation must count displaced waiting and unmet demand. The point is not to minimize admissions universally; it is to keep the constrained stage from losing productive capacity while making the burden visible.

**Protect different service needs explicitly.** Interactive and background tasks, long and short jobs, buses and cars, freight and pedestrians can require different measures. Isolation can improve reliability and can also strand capacity. Fairness, accessibility and safety cannot be inferred from a single throughput total.

### Manual ratification checklist

Before approving any candidate, identify its exact version and intended environment; the source evidence and model assumptions; its measurement boundary and comparison baseline; the expected mechanism rather than an unsupported promised percentage; and the outcomes that must not worsen unnoticed. Specify what would trigger rollback, how unfinished work is handled, and who has the authority to make the change.

A ratification record should distinguish permission to refine a paper design, permission to run an offline evaluation, permission to change code, and permission to deploy. None is silently implied by another. The present report supplies a reference for those decisions, not a record that they were made.


<!-- pagebreak -->

## Separate appendix on catchphrases and scalloping

This appendix is a text-only candidate specification, independent of congestion claims. It does not describe implemented generator code or a live integration.

### Owner requirement and provenance

The owner requirement is preserved verbatim:

> I want catch phrases to go in a separate bucket for filtering into idioms, mantras, and proverbs. Saying something repeatedly means it was worth remembering or taught something valuable, but it can be "scalloped" (personally means refining a word/phrase with better depth and usability).

**Scalloped** is the user's personal project meaning: refining a word or phrase for better depth and usability. This report does not assert that meaning as a dictionary definition. The user's interpretation of repetition is preserved as owner meaning; observed frequency, attributed personal value, and factual evidence remain separate.

### Classification

Keep catchphrases together for discovery and filter with overlapping tags. A phrase can remain unclassified.

- **Idiom:** an expression whose conventional meaning is not simply the sum of its words. Mark a new metaphor as an idiom candidate, not an established expression. Source: [Cambridge Dictionary: idiom](https://dictionary.cambridge.org/dictionary/english/idiom).
- **Mantra:** here, a phrase intentionally repeated to express or reinforce an orientation. This is the ordinary nonmedical sense; religious uses also exist. Source: [Cambridge Dictionary: mantra](https://dictionary.cambridge.org/dictionary/english/mantra?topic=sentences-and-expressions).
- **Proverb:** a concise saying conveying advice or a commonly recognized observation. A new project saying may be proverb-like without a claim of traditional origin. Source: [Cambridge Dictionary: proverb](https://dictionary.cambridge.org/dictionary/english/proverb).

A phrase can function as a mantra while offering proverb-like advice. Classification concerns how it works, not whether its content is true. No claims about cognitive recall or illusory truth are needed for this design.



### Candidate phrase record

- **phrase_id.** Stable identifier
- **root_text.** Immutable exact string; no spelling or spacing cleanup
- **provenance.** Source locator, author/speaker if known, date if known, exact-quote/paraphrase/original-example status
- **owner_meaning.** Owner explanation, its source, and directly-stated versus interpreted status
- **tags.** Set of idiom/mantra/proverb labels, each with established/candidate/proverb-like status, rationale, reviewer
- **occurrences.** Observed uses with source and context; deduplicate copied captures
- **repetition_count.** Derived count of documented occurrences; unknown if coverage unknown
- **value.** Owner-stated reason to remember, lesson, intended use; unknown allowed
- **claim_status.** Not-a-factual-claim/unassessed/supported/disputed, with independent evidence references when applicable
- **context.** Audience, situation, fictional/real-world scope, literal/figurative reading
- **conditions.** When useful, when not applicable, bounded counterexamples
- **variants.** Append-only versions: text, parent version, editor, rationale, intended gain, meaning-change note
- **ratification.** Proposed/accepted/rejected; exact version, user decision reference, separately authorized use

### Invariants

1. Repetition, personal value, provenance, and factual support are distinct.
2. The user's interpretation of repetition remains owner meaning. A count alone cannot manufacture an attributed lesson, universal value, or truth.
3. Repeated quotations are not independent corroboration.
4. A refinement that changes the lesson is labeled a meaning change, not disguised as polishing.
5. Accepted wording does not constitute blanket deployment authorization.
6. Role assignments describe who voices or uses a phrase. They do not populate knowledge/evidence fields. Fictional character beliefs remain distinguishable from world facts.
7. Missing evidence stays missing. Do not invent repetition counts or user quotations.
8. Preserve the exact root and append linked refinements; never silently overwrite.



## Three phrase review passes

The pass names Listen, Turn and Shape describe proposed editorial work, not a religious tradition. The demonstration phrases below are original examples for this review, not user quotations or attested traditional sayings.

### Pass One Listen for exact root and provenance

**Point.** Preserve what was actually said before improving how it reads.

**Bridge.** Bind immutable root text to a source, context and owner explanation. Keep directly stated meaning separate from an editor's interpretation. Observed recurrence, attributed value and factual support are distinct fields.

**Path.** The original demonstration “Leave room for the next idea” could invite openness in brainstorming or literal blank space on a page. The record preserves both possible readings unless the owner identifies one. A later refinement can clarify the intended reading without pretending the initial ambiguity never existed.

**Shadow.** Repetition alone does not establish that a phrase was valuable to every speaker, nor that its claim is true. Copied quotations are not independent corroboration. The user's interpretation of repetition remains owner meaning; a missing usage history stays unknown rather than becoming an invented count.

### Pass Two Turn toward semantic boundaries

**Point.** A useful lesson need not be an unconditional law.

**Bridge.** Classification describes a phrase's function. A line can be a deliberately repeated mantra and proverb-like advice without being an established proverb or a factual finding. A new metaphor is not automatically an established idiom.

**Path.** The original demonstration “A second look finds the missing piece” encourages checking. Its nearby counterexample is that the piece was never in the box. A bounded reading says another look may reveal an omission; it does not guarantee that a missing object or answer can be found.

**Shadow.** Flattening every expression into a literal proposition can destroy its useful figurative role. Keeping figurative value, however, does not authorize presenting a character's belief as a world fact, an evidence source or a user belief. Role and speech-marker assignments remain separate from knowledge fields.

### Pass Three Shape with versioned refinement

**Point.** Scalloping can change meaning and must preserve its lineage.

**Bridge.** In the owner's usage, scalloping refines a word or phrase for better depth and usability. It is a personal project meaning, not a claimed dictionary definition. Append variants with the editor, parent version, intended gain, lost nuance and ratification state.

**Path.** The original demonstration “Keep every door open” becomes the proposed variant “Keep useful options open until a choice is needed.” It gains a decision boundary but loses some vividness and removes an absolute. A simple craft project supplies a counterexample: preserving every option can prevent finishing. The change is substantive narrowing, not cosmetic polishing.

**Shadow.** A gentler or clearer version can still misrepresent the owner. Preserve the root, allow rejection and retain the option to choose neither. Acceptance of this wording does not authorize deployment in a generator, public interface or character profile without the separately approved use.

### Existing source boundary

A read-only inspection of the recovered local project snapshot found catchphrase-related tropes and adjacent speech markers, but no dedicated phrase registry in that snapshot. This is not a claim about the entire project. A proposed separate registry should reference roles or speech markers rather than silently migrating or overwriting them. No inspected source was executed or changed in that review.

Dictionary descriptions are linked in the classification section. Some direct pages denied access; the definitions were checked through search-index results. No cognitive-recall or illusory-truth claim is needed to justify this record design.


<!-- pagebreak -->

## Separate appendix on optional character mantras

### Holy Fear and selection boundaries

In this candidate resource, **Holy Fear means self-preservation agency**, not panic, an inferred frightened state, obedience or a claim that danger exists. A character may choose a mnemonic about boundaries, rest, preparation, courage, help, discernment or flexibility. Selection does not establish the user's beliefs, a world truth, objective moral law, a hidden personality diagnosis or authority to override anyone's choice.

Historical excerpts, new project adaptations and original drafts are different kinds of text. The examples below retain that distinction. The historical wording was matched against primary-work transcriptions with whitespace normalized; that is not independent collation against a scan, proof of earliest origin or evidence of popularity. The Franklin source is the 1810 edition of *The Way to Wealth*, in which Father Abraham quotes Poor Richard. The Analects wording is James Legge's historical English translation, not original English speech by Confucius.

### Directing work without becoming its instrument

**Exact historical excerpt.** “Drive thy business, let not that drive thee;” [Benjamin Franklin, The Way to Wealth (1810 edition); Father Abraham quoting Poor Richard; I; printed pp. 11-12](https://www.gutenberg.org/cache/epub/43855/pg43855-images.html).

**Scalloped project adaptation, not a historical quotation.** “Choose the work; do not let the work choose all of you.” Adds explicit personal boundaries; the source concerns industrious management, not a modern work-rest doctrine.

**Bounded scene.** A character sets a stopping time and delegates a task. **Limit.** Urgent care may temporarily require responding rather than directing; control is not absolute.

### Pausing before an attractive offer

**Exact historical excerpt.** “At a great pennyworth pause a while:” [Benjamin Franklin, The Way to Wealth (1810 edition); Father Abraham quoting Poor Richard; III; printed p. 24](https://www.gutenberg.org/cache/epub/43855/pg43855-images.html).

**Scalloped project adaptation, not a historical quotation.** “A bargain can wait for a clear yes.” Modernizes pennyworth and adds consent language absent from the source.

**Bounded scene.** A character pauses before accepting a glittering offer. **Limit.** A truly time-limited harmless opportunity may reasonably be accepted quickly.

### Correcting without surrendering identity

**Exact historical excerpt.** “When you have faults, do not fear to abandon them.” [Analects, Book I, chapter VIII, section 4; James Legge translation; attributed in the text to the Master](https://www.gutenberg.org/cache/epub/3330/pg3330-images.html).

**Scalloped project adaptation, not a historical quotation.** “I can leave a mistake without leaving myself behind.” Adds continuity of identity; source concerns abandoning faults, not abandoning personhood.

**Bounded scene.** A character corrects a mistaken promise after learning its effects. **Limit.** Someone calling a trait a fault does not make it one; shame must not authorize another person’s control.

### Being more than a single use

**Exact historical excerpt.** “The accomplished scholar is not a utensil.” [Analects, Book II, chapter XII; James Legge translation; attributed in the text to the Master](https://www.gutenberg.org/cache/epub/3330/pg3330-images.html).

**Scalloped project adaptation, not a historical quotation.** “I am more than the use others make of me.” Broadens scholar’s non-instrumentality into a personal boundary; modern project interpretation, not literal equivalence.

**Bounded scene.** A character declines being defined solely by a useful talent. **Limit.** Specialization and freely chosen service remain valid; being useful is not automatically exploitation.

### Accepting help without losing agency

**Original project draft, not a historical quotation or user-authored canon.** “Help can widen my choices without taking them away.”

**Bounded scene.** A character asks a companion for options while retaining the final decision. **Limit.** Some offered help is conditional; inspect the conditions rather than assuming all help expands agency.

Selection should offer the source, theme, exact or adapted form, an option to choose neither, and custom wording. Do not silently rank candidates by unmeasured popularity or inferred beliefs. The wider source resource contains additional candidates and held attributions; a held claim is not a selectable verified quotation. Familiar wording is not a substitute for passage-level provenance.



## Three mantra review passes

### Pass One Provenance and exactness

**Point.** A memorable line can be useful without proving its attribution or its truth.

**Bridge.** Bind an exact excerpt to a work, edition, represented speaker, translator when applicable and passage locator. Appearance in Franklin's text does not establish that Franklin originated every proverb. The Analects preserves collected sayings and dialogues; the translation's wording is translator-specific.

**Path.** A source-backed excerpt and a modern project adaptation appear side by side. The source field belongs to the exact excerpt, while the new wording carries its own authorship and meaning-change note. Two attractive but unverified attributions in the candidate resource remain held rather than being silently assigned to Franklin or Confucius.

**Shadow.** A transcription match is not scan collation, proof of historical utterance or a popularity measurement. Absence from the bounded material inspected does not conclusively prove a quotation false. The careful state is unverified, not confidently attributed or confidently disproved.

### Pass Two Holy Fear and character depth

**Point.** Self-preservation agency can support character depth without becoming a compulsory behavior rule.

**Bridge.** Connect a chosen line to a concrete scene and a nearby counterexample. Preserve choice, revision, refusal and differences between characters. A maxim can reveal what a character values without making that value a universal law.

**Path.** A character uses the original draft about help to ask a companion for options while retaining the final decision. Another character notices that the offered help comes with controlling conditions and declines it. The phrase has a useful range, not a guaranteed effect on every interaction.

**Shadow.** Courage cannot force exposure, rest need not be justified by productivity, and kindness is not a requirement for a valid boundary. Self-preservation cannot be converted into a blanket ban on freely chosen costly care. Characters may misunderstand, reject or outgrow a maxim; no diagnosis of the user follows from their fictional choices.

### Pass Three Scalloped refinement and reversibility

**Point.** Refining a quotation can materially change its ethical emphasis.

**Bridge.** Keep the exact source intact and label adaptations separately. A new consent, capacity or boundary clause may be valuable precisely because it adds something absent from the historical text; that gain must not be disguised as faithful quotation.

**Path.** The Franklin line about pausing at a bargain becomes a draft about waiting for a clear yes. The adaptation modernizes the idiom and adds consent language. Its record states that change and leaves both versions available, along with neither. The user can ratify a precise variant for a precise use without endorsing every surrounding historical view.

**Shadow.** Gentle wording can still distort a source or pressure a character to comply. A child-suitable excerpt does not establish that the surrounding historical work is uniformly child-suitable. All candidates remain inert until the appropriate manual ratification; this appendix is not evidence that a selector or generator was implemented.


<!-- pagebreak -->

## Source register and evidence limits

Sources below were checked in the research pass dated 23 October 2026. Links also appear beside the claims they support. Primary academic work, standards, government guidance and first-party operator documentation are distinguished by their role; a citation is not a claim that Blackwish has reproduced its result. Living engine documentation may change, so a future implementation proposal should record the exact release or commit it uses.

### Queueing and distributed systems

Mathematical teaching sources explain conditional models; operator sources describe engineering experience; RFC 7567 is a standards recommendation; the SRPT paper analyzes fairness in specified settings.

- [MIT queueing lecture](https://web.mit.edu/1.041/www/lectures/L8-queuing-models-2026sp.pdf).
- [MIT queueing notes, pp. 2-4](https://ocw.mit.edu/courses/15-763j-manufacturing-system-and-supply-chain-design-spring-2005/22f4805864deb06eee85acc1601463ba_queueing_note.pdf).
- [IETF RFC 7567](https://www.rfc-editor.org/rfc/rfc7567.html).
- [Google SRE: Handling Overload](https://sre.google/sre-book/handling-overload/).
- [AWS: Avoiding insurmountable queue backlogs](https://d1.awsstatic.com/builderslibrary/pdfs/avoiding-insurmountable-queue-backlogs.pdf).
- [AWS: Timeouts, retries, and backoff with jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/).
- [gRPC deadlines](https://grpc.io/docs/guides/deadlines/).
- [AWS: Caching challenges and strategies](https://aws.amazon.com/builders-library/caching-challenges-and-strategies/).
- [Google SRE monitoring](https://sre.google/sre-book/monitoring-distributed-systems/).
- [Google SRE: Addressing Cascading Failures](https://sre.google/sre-book/addressing-cascading-failures/).

- [Harchol Balter and colleagues SRPT fairness analysis](https://www.cs.cmu.edu/~harchol/Papers/jss.pdf).

### AI inference

Primary papers and first-party serving documentation. Treat configuration advice as version-specific. The 2026 CacheRoute and remote-KV sources are preprints; their workload-specific results are not universal performance rankings.

- [BurstGPT](https://arxiv.org/abs/2401.17644).
- [vLLM production metrics](https://docs.vllm.ai/en/latest/usage/metrics/).
- [TensorRT-LLM scheduling](https://github.com/NVIDIA/TensorRT-LLM/blob/main/docs/source/legacy/performance/performance-tuning-guide/useful-runtime-flags.md).
- [vLLM optimization](https://docs.vllm.ai/en/latest/configuration/optimization/).
- [DistServe, OSDI 2024](https://arxiv.org/abs/2401.09670).
- [TaiChi, 2025](https://arxiv.org/abs/2508.01989).
- [vLLM automatic prefix caching](https://docs.vllm.ai/en/latest/features/automatic_prefix_caching/).
- [Dynamo router](https://docs.nvidia.com/dynamo/dev/knowledge-base/modular-components/router/overview).
- [CacheRoute](https://arxiv.org/abs/2608.19677).
- [When the KV Cache Is Slower Than the GPU](https://arxiv.org/abs/2610.21500).
- [vLLM speculative decoding](https://docs.vllm.ai/en/latest/features/speculative_decoding/).
- [Fairness in Serving LLMs](https://arxiv.org/abs/2401.00588).
- [vLLM abort API](https://docs.vllm.ai/en/latest/serving/online_serving/token_in_token_out/).
- [Dynamo planner tuning](https://docs.dynamo.nvidia.com/dynamo/dev/kubernetes/auto-deployment/dynamo-planner).

### Physical traffic

Government mechanisms and evaluation guidance, primary transport research and the original Braess paper translation/background. Local road-control decisions require authorized traffic expertise and safety review.

- [FHWA freeway-flow discussion](https://ops.fhwa.dot.gov/freewaymgmt/publications/frwy_mgmt_handbook/chapter1_02.htm).
- [FHWA alternative fundamental diagrams](https://ops.fhwa.dot.gov/publications/weatherempirical/sect3.htm).
- [FHWA bottleneck classification](https://ops.fhwa.dot.gov/bn/bnchart.htm).
- [Capacity-drop modeling paper](https://arxiv.org/abs/2106.10347).
- [FHWA ramp-metering mechanism and evaluation](https://ops.fhwa.dot.gov/publications/fhwahop14020/sec1.htm).
- [FHWA ramp-metering challenges](https://ops.fhwa.dot.gov/publications/fhwahop14020/sec2.htm).
- [FHWA adaptive-control guidance](https://ops.fhwa.dot.gov/publications/fhwahop08024/chapter9.htm).
- [FHWA Traffic Signal Program Handbook](https://ops.fhwa.dot.gov/publications/fhwahop23041/fhwahop23041.pdf).
- [FHWA incident timeline](https://ops.fhwa.dot.gov/publications/fhwahop15007/chapter1.htm).
- [FHWA Traffic Incident Management](https://ops.fhwa.dot.gov/tim/).
- [USDOT road-pricing overview](https://www.transportation.gov/sites/dot.gov/files/2025-01/Road%20Pricing.pdf).
- [The Fundamental Law of Road Congestion](https://www.nber.org/papers/w15376).
- [Original-paper translation/background from its co-translator](https://supernet.isenberg.umass.edu/braess/braess-new.html).
- [FTA bus-lane guidance](https://www.transit.dot.gov/research-innovation/bus-lanes).
- [FTA signal-priority guidance](https://www.transit.dot.gov/research-innovation/signal-priority).
- [FHWA urban-freight primer](https://ops.fhwa.dot.gov/Publications/fhwahop18020/index.htm).
- [FHWA curb/freight benefits](https://ops-dr.fhwa.dot.gov/publications/fhwahop18020/benefits.htm).
- [USDOT methodology](https://www.itskrs.its.dot.gov/2024-b01820).
- [FHWA adaptive-control validation guidance](https://ops.fhwa.dot.gov/publications/fhwahop13031/index.htm).

### Language and historical wording

Dictionary references support ordinary category usage, not the owner-defined meaning of scalloping. The historical works supply passage-level wording, not popularity claims or proof of universal advice.

- [Cambridge Dictionary: idiom](https://dictionary.cambridge.org/dictionary/english/idiom).
- [Cambridge Dictionary: mantra](https://dictionary.cambridge.org/dictionary/english/mantra?topic=sentences-and-expressions).
- [Cambridge Dictionary: proverb](https://dictionary.cambridge.org/dictionary/english/proverb).

- [Benjamin Franklin The Way to Wealth 1810 edition](https://www.gutenberg.org/cache/epub/43855/pg43855-images.html). Father Abraham and Poor Richard are the literary framing; verified appearance is not proof of proverb origin.
- [The Analects James Legge translation](https://www.gutenberg.org/cache/epub/3330/pg3330-images.html). Book and chapter labels follow this transcription; numbering can differ in modern editions.

### What remains unestablished

No Blackwish traffic trace, production benchmark, live serving configuration or controlled human experiment is reported here. The cited research cannot establish an actual Blackwish bottleneck without relevant observations. Numerical toy examples are explicitly conditional calculations. The reference identifies candidate mechanisms and review questions; it does not certify a performance target, validate a deployment or ratify a wording change.
