SCONE working group meeting IETF 122 Bangkok  
March 21, 2025  
9:30 am to 11:30 am

Chairs: Brian Trammell, Qin Wu

Notes: Martin Duke, Abhishek Tiwari

## Introduction (Chairs)   {#introduction-chairs}

Chairs emphasized the need to make progress on experimentation

## Work Item 1: Protocol Framing   {#work-item-1-protocol-framing}

Merged Protocol Proposal:TRONE protocol (Marcus Ihlar/Martin Thomson)

Antoine: Is b\_min, b\_max negotiable?

Marcus: Each QUIC version would indicate b\_min, with 2 versions in the
draft. b\_max is calculated from b\_min and exponent.

Abhishek: how do you encode the unit (e.g. kbps)?

Marcus: It is in the protocol spec

Antoine: This reminds me of negotiation of codecs in multimedia
communications. Can we provide very dynamic encoding of the range of
interest?

Marcus: That gets complicated, maybe overkill for this use case.

Martin: Does it return 63 if anywhere outside the range?

Marcus: No. If below the range, returns 0. If above the range, returns
63. Endpoint uses the min of the two values.

Abhishek: How do we specify the method of measurement (time interval
etc)

Marcus: We'll provide guidance in draft about what it means and how to
measure it, and what to do with it.

Abhishek: What's with the range overlap?

Marcus: Exclusive ranges might lead to fingerprinting indicating region
of interest. The overlapping region also provides high granularity in an
important region.

Luis Contreras: Take the lowest, so you'd always use the lower range
encoding?

Marcus: No, 63 means infinity.

Marten: How many new versions will you need?

Marcus: Not very often. 12.5 Gbps is big. Maybe if we need more
granularity in some range?

MT: Version A should cover most video use cases. Version B is
anticipating future needs.

Harald: Noting that in audio calling we can have rates below 100kbps. In
avtcore yesterday it was presented that uncompressed video at 2.5Gbps

Mirja: The low ranges are not interesting because there won't be a rate
limit there. Extensibility is good because it is hard to predict the
future. New versions are a rough extensibility model because of
ossification.

Marcus: Not sure it will ossify.

Dan Druta: Want to make sure that the bitrate is more than an average
bitrate. It's an aggregate for the 4tuple.

Christian: Love the design. There are other ways to control bitrate. It
puts guardrails around congestion control, ECN, etc, not the whole
story.

Renjie: Just one piece of information?

Marcus: Yep, new version and new standard for a new payload.

MT: SCONE used to be a 2D expression (bitrate and time window of
measurement). Harder for a network element to figure if the amount is
lower and should therefore be updated.

Mirja: Timing window is useful info, always take the lowest rate.

Gorry: (individual) clarity on limit and ceiling? This is throughput
advice? Does not constrain sender?

Marcus: Yes

Martin Duke: Agree with Mirja. Not hard to update tput if that's lowest,
expiration if that's lowest, but maybe you have a better way to handle
updates, so I'll defer judgment.

Zahed: You said if the client is not compliying with the thrughput
advice then the newtwork can send another advice, but in trone the
network is not generating any packet, so how they will do that i.e. they
need to wait for any trone packet passing through. so When can
throughput advice be generated and send?

Marcus: When new information is available the network element will send
a new TRONE throughput guidance.

MT: This is not "persistent congestion". Send when the endpoint
experiences consistently below-target bitrate.

DKG: This could leak an address migration to the network.

Marcus: Probably not a part of prep for address migration, it happens
after. Can choose not to send. But have to be careful.

Brian Trammell: +1 we need to be careful about linkability. Guidance
about signal rate? Current guidance is to have no guidance about network
element injection? Could pad to MTU to deter.

Marcus: There is no defense against injection, just requires more
protocol.

Mirja: Endpoint does not control signal. challenge is network makes
decision, does not control the rate. Network element knows the best when
a rate advice needs to be sent.

Martin Duke: Elements injecting TRONE is scary; need to think carefully,
not too much protocol needed to deter elements from doing this.

Jonathan Lennox: Two endpoihts here. We are being sloppy about who is
deciding what, need to clarify.

Christian: +1, TRONE Injection from network is scary.

Mirja: Network elements already maintain per flow state, not a big deal.

Zahed: If network is in bad situation, it wants to send a message. How
does it send that? Probably congestion signals. Maybe a way to ask for
TRONE?

Sanjay: The problem today: client gets manifest, picks a bit rate, sends
a request. A rate report would be helpful. What if the user device
changes network (e.g. 5G to 4G)?

Marcus: 5G to 4G: no visible change at client. Should the network tell
you? Easy enough to just send TRONE a lot. Need to study the trade offs
here.

Gorry: We're going to revisit this. OK to have options now.

Marcus: Right now the networks decrypt the QUIC initial and detect SNI
and thus classify the flow.

Martin: Are we proposing DPI? That can't work - server TPs are not
readable.

Marcus: No, append a TRONE hint to client Initial. It allows
classification based on the first packet.

MT: This might not be useful, without server confirmation. But it's
harmless.

Zahed: TRONE hint seems like an optimization.

Matt Joras: This hint would allow elements to stop DPI. Deployment of
ECH is complicated because of the existence of DPI in the network
elements.

Antoine: This reminds me of some UDP options applications.

Marcus: Skeptical; UDP opt is E2E, wrong layer, but we can look at it.

Marten: Post-quantum: there is no padding happening. sending non-v1 is
not allowed?

Many people: yes it is, Firefox does.

Abhishek: (re: 20s time window) Some downloads are chunked together and
there may be idle periods > 20 sec. This needs experimentation

Martin: Is a fixed value of time window conflict with shallow queues?

(Many people disagree)

Mirja: Throttle might differ from the reported value; maybe this isn't
useful.

Tianji: With delay budget, we might not fully utilize the link. This may
not be a good tool for many policies

Marcus: that's a different layer.

Christian: We need some text about congestion control. Martin Duke's
objection is solved with congestion control.

Gorry: we need to think about damaging non-participant flows. Guidance
to network elements is maybe out of scope?

Brian: We clearly understand the proposal, based on the discussion.
Can't do an adoption call because there is no document, but we'll do it
on the list.

### Poll: Do you support the proposal under discussion as a basis for a WG protocol specification?   {#poll-do-you-support-the-proposal-under-discussion-as-a-basis-for-a-wg-protocol-specification}

Yes: 41 No: 3 No Opinion: 7 (90 attendees)

Brian: Objectors want to say anything?

Luis: Not satisfied with security considerations. Is this a DoS vector
against operators?

Marcus: So bad we can't adopt it?

Luis: Would like to understand before adopting.

Brian: Will do adoption call on list once a draft exists. Every draft
submitted to IESG will have security considerations.

## Work Item 2: Applicability and Managability   {#work-item-2-applicability-and-managability}

### SCONE Mobile Network Use Case (Sanjay Mishra)   {#scone-mobile-network-use-case-sanjay-mishra}

Martin Duke: does TRONE meet your requirements? Sounds like the third
one doesn't.

Sanjay: Maybe not all. Does not seem far, can be worked out in the
working group discussions.

Mirja: Third requirement doesn't sound useful.

### Throttle policies Taxonomy and impact (Kyriakos Zarifis)   {#throttle-policies-taxonomy-and-impact-kyriakos-zarifis}

Magnus: I would have expected subscriber-based throttling.

Kyriakos: Agreed. It was there in the slides. May be I did not phrase it
properly

## Conclusion (Chairs)   {#conclusion-chairs}

Brian: We'd like to make a lot of progress before Madrid. Aggressive
virtual interim schedule, every third Wednesday with distributed
timezone pain. 4/9, 4/30, 5/21, 6/11, 7/2

Will discuss Hackathon goals, Brian will be there.

Mirja: Can we have 1-2 editors on TRONE?

Brian: yep

Dan Druta: Do you expect TRONE to be the only document? I think it
misses some requirements and desired semantics. Would like richer
feedback.

