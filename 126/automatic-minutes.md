**Session Date/Time:** 24 July 2026 09:00 CEST

# [SCONE](../wg/scone.html)

## Summary
The SCONE Working Group met at IETF 126 to discuss the finalization of the core protocol draft, address feedback on the applicability and manageability considerations draft, and plan the future direction of the working group. The WG agreed to submit the SCONE protocol draft to the IESG, decoupled from the applicability and manageability draft, due to external dependencies (such as 3GPP), while continuing to refine the applicability and manageability draft with a target of initiating a Working Group Last Call (WGLC) in September or October.

---

## Key Discussion Points

### 1. Hackathon and Interoperability Status
* **Marcus Ihlar** reported on recent interop experimentation, including testing SCONE advice over emulated satellite links (addressing concerns raised by **Gorry Fairhurst** regarding highly impaired links). 
* Work is also ongoing with researchers from the University of Aberdeen to enable open-source adaptive bitrate (ABR) clients to utilize SCONE advice.

### 2. SCONE Protocol Completion
* **Martin Thomson** confirmed that the [draft-ietf-scone-protocol](https://datatracker.ietf.org/doc/draft-ietf-scone-protocol/) is stable and contains only minor editorial updates since the previous working group last call.
* There were no objections to submitting the document to the IESG. **Gorry Fairhurst** (AD) advised the chairs to review the mailing list and then submit. The working group agreed to proceed with the publication request rather than coupling it with the manageability document, citing deployment urgency from **Marcus Ihlar**, **Matt Joras**, and **Anoop Prasad** (noting 3GPP and real-world deployment timelines).

### 3. SCONE Applicability & Manageability
**Sanjay Mishra** presented updates on the [SCONE AppMan](https://datatracker.ietf.org/meeting/126/materials/slides-126-scone-scone-appman-02) and [Appman Draft](https://datatracker.ietf.org/meeting/126/materials/slides-126-scone-appman-draft-00) for [draft-ietf-scone-applicability-manageability](https://datatracker.ietf.org/doc/draft-ietf-scone-applicability-manageability/).

* **Version 02 Changes:** The draft underwent a significant rewrite. Key changes include moving "Operational Considerations" to the front of the main body, restructuring the introduction, moving per-flow signaling to Section 3, and revising the ECN and L4S interworking sections (distinguishing proactive vs. reactive signaling).
* **OpsDir Review (Joe Clark):** 
  * **PR 55** (detecting when an endpoint ignores advice) was added to address diagnostic capabilities.
  * **PR 49** (handling non-compliance): **Lars Eggert** objected that the language around misbehaving applications moves away from SCONE's advisory intent, arguing that non-reactive SCONE traffic should be treated the same as other non-SCONE traffic the network already handles, rather than as less than best-effort. **Zaheduzzaman Sarker** agreed, noting the language could be softened. **Gorry Fairhurst** objected specifically to the words "violation" and "conformance": monitoring to protect the network is fine, but the terminology needs to change. **Mirja Kühlewind** noted that enforcement is independent of SCONE — the network enforces its limits regardless of whether an endpoint understands the advice — and characterized the issue as a misunderstanding of the document, to be resolved by clarification rather than by enforcement language. **Christian Huitema** stressed that a flow signal must not change how the network manages traffic ("SCONE is not RSVP"). **Martin Thomson** posted suggested wording to the PR, and the editors agreed to reformulate the language there.
  * **Kazuho Oku** noted that a client such as a browser may emit SCONE signals without knowing whether the specific application using it will actually act on them.
* **Tunnels and MASQUE (PR 37):**
  * **Mirja Kühlewind** noted the text is generic to tunnels but highlights MASQUE as the prominent QUIC-based case.
  * **Martin Thomson** pointed out an error in the proposed text: clients should not blindly take the minimum of two values across tunnels. Instead, each piece of advice strictly applies only to the specific flow on which it was received.
* **L4S & Shapers Motivation:**
  * **Stuart Cheshire** expressed skepticism regarding the necessity of SCONE over existing traffic shapers, policers, or L4S enforcements, questioning the deployment timelines.
  * **Martin Thomson** and **Christian Huitema** emphasized that SCONE provides critical rate transparency to endpoints, which is missing from traditional packet-dropping shapers.
* **Document Reframing:**
  * **Mirja Kühlewind** suggested focusing the document on operator manageability (possibly dropping "applicability" from the title) and volunteered to submit a PR to reframe the text accordingly.

### 4. Future of the Working Group & New Work
The working group discussed several proposals for potential rechartering or post-completion work:

* **SCONE Echo (`draft-duke-scone-echo`):** **Martin Duke** requested feedback on the draft, specifically regarding its privacy properties. He noted that if SCONE closes, the work could potentially move to the QUIC WG, and that his employer would likely implement it regardless.
* **SCONE for TCP:** Mentioned as a potential item for TCPM or SCONE if rechartered.
* **RoCE (RDMA over Converged Ethernet) over UDP:** **Tianji** proposed using SCONE-like signaling for wide-area, cross-datacenter RoCE networks to handle slow congestion convergence over long RTTs.
  * **Lars Eggert** questioned how this would interface with RoCE's highly integrated fabric flow control.
  * **Gorry Fairhurst** suggested that this multilayer transport and network interaction is more suited for TSVWG rather than SCONE.
* **WG Status and New Work:** **Martin Thomson** noted that the working group will likely need to stay open to manage publication of the core documents, with no urgency to close it now. **Brian Trammell** (as chair) stated that proponents of new work (including SCONE TCP, Echo, and RoCE) should have drafts ready for a formal rechartering discussion at IETF 127.
* **Future scenarios and applicability:** **Tianji** noted that a potential 6G architecture could make MASQUE-for-SCONE viable, and that new SCONE work would likely influence the applicability and manageability draft (which currently reflects what is done with QUIC). **Brian Trammell** (as an individual) noted that possible new protocols could address these concerns in their own operational considerations sections, rather than relying on the SCONE appman document to do so.

---

## Next Steps

* The chairs will review any mailing list discussion and then submit [draft-ietf-scone-protocol](https://datatracker.ietf.org/doc/draft-ietf-scone-protocol/) to the AD/IESG for publication on **Monday 27 July 2026**. The working group will not couple the progression of the protocol and manageability drafts; the protocol draft will proceed on its own.
* Following the comment deadline of Tuesday 11 August 2026, editors to resolve the open GitHub PRs and issues for [draft-ietf-scone-applicability-manageability](https://datatracker.ietf.org/doc/draft-ietf-scone-applicability-manageability/) through the remainder of August, targeting a Working Group Last Call (WGLC) for the manageability draft in the September–October timeframe.
* Proponents of new work items to foster discussion on the mailing list ahead of the rechartering evaluation at IETF 127.