# SCONE Interim - February 2025   {#scone-interim---february-2025}

*   notes: Marcus Ihlar, Ted Hardie, Brian Trammell

## Intro   {#intro}

*   experimentation: please discuss on the mailing list

## Merged Protocol Discussion (TRONE)   {#merged-protocol-discussion-trone}

summary: Marcus reviews the need to use the communication model from
TRAIN (TRONE packets bound to QUIC packets, negotiated with a transport
parameter). Adopt the ability from SCONE to have a network element
generate a new TRONE packet. The slides indicate that this may be
limited to times when the introduction of TRONE does not cause the
datagram to exceed the MTU; discussion from Mirja and Christian on this
point challenges the likelihood, given that this is negotiated by QUIC
but not visible to the network element.

Brian, as chair, suggested that we consider this as a requirement, but
leave the mechanism to WG discussion.

Marcus then reviewed the encoding of throughput advice, which has been a
point of contention on the list. In addition to the question of signal
complexity, there is a question of where the signal is in the packet
(particularly whether it is in a fixed location or not) since that
contributes to the complexity of implementation and pain of deployment.

Ted: I agree with Christian on the importance of using a fixed place in
the packet for simplifying hardware development. I also want to remind
folks that we want applications to consume this. If you have policy
delivered to the application that is composed from multiple parties, it
may have difficulty in adjusting its behavior. A mechanism that allows
later nodes to simply update to more restrictive policies would be
simpler (as TRAIN works now).

Mirja: For lower rates, just replace the TRONE packet.

Abhishek: I see the point about simplicitly, want to challenge... the
majority of this problem arises in mobile network architectures, there
is usually one capable node (UPFN) that has access to subscriber info.
That's the thing that will insert rate information. So this architecture
limits how many talkers of this protocol.

Martin: Rich vs sparse info on throughput. Will have to do some
experiments. Would be good for the initial draft to just stick an x-bit
blob in the protocol, and we can decide on encoding after
experimentation

Matt plus ones Martin's point. He also wants to ground our discussion of
policy composition in deployments. At the moment there is one element
that is imposing policies like this in most networks.

Mirja: This is not a per-packet signal like ECN. It's a per-flow signal.
It's about shaping, which also needs per-flow state. Because of where
this is going to be in the network, per-flow state is not a hige deal

Media space is moving quickly. Don't want to make guesses about what
happens tomorrow. So we will need flexibility.

Christian: Need to make sure that bits are reserved so modification in
place can happen.

Marcus: No expansion of packets, that is a strong requirement.

Dan: Update frequency is important. We should explore push notifications

Christian: Understand that desire; injection of information is a
security problem. If this is a design feature, we cannot tell on-path
from off-path injection in the absence of authentication, which we don't
have. Nothing prevents injection of a TRAIN packet except endpoint
policy not to accept TRAIN-only packets. That check will be there
because it is necessary for security.

Marcus: TRAIN packets are unidirectional. If we could signal desire for
a reverse TRAIN packet, that might work to meet the frequency
requirement.

Christian: TRAIN/TRONE is not in isolation, it's part of a wider
feedback mechanism in the network. For per packet signaling, we also
have ECN. Bandwidth limited by TRAIN is also subject to per-packet ECN
signaling. We have to understand the dynamic between these reactive
mechanisms and TRONE, which is less reactive but slower. How does a
sender compose these? Maybe we suggest that ECN is also a signal to poll
again for TRONE.

Marcus: That sounds nice. TRONE is about setting an upper bound. ECN
shows dynamic conditions. Channel conditions might allow less than
policy. ECN might not always indicate a policy environment change.

Mirja: SCONE won't always be at the congested link.

Brian: Need to understand update frequency

Mirja: Frequency is the wrong way to think about it... timeliness is a
better way to think about it. (Chrisitan: the word you're looking for is
timescale)

Mirja: We should optimize for one shaper in the access network. because
that is (by far) the most common case. (broad agreement in the chat)

Christian: I'm hearing there is tension around timescale. One timescale:
wifi hotspot change. Another timescale: move to a completely different
network (border crossing). Move to a different cell (same network) --
this might happen very fast.

Mirja: Cell change is more a CC issue

Christian: The joined draft needs to be very clear about this. What is
TRONE, what is congestion control.

Abhishek: We need to look at this practically to answer the timescale
question. Look at policy change timescales. Look at changing network
technologies. Look at plan exhaustion timescales. These are on the
minutes-to-hours scale.

Discussion in the group about how to get a document for discussion in
Bangkok resulted in the authors of the two documents going off to
generate a merged document, with the agreement that if that did not work
by Bangkok that an external editor would be selected.

## Leveraging the user plane function for network-side advisory signal   {#leveraging-the-user-plane-function-for-network-side-advisory-signal}

Goal of this presentation: introduce the network element that can
acually do SCONE, the UPF.

Kevin Smith notes that the UPF is the easiest place to implement SCONE
in a mobile network, but asks if the information available to the UPF is
as fresh as it needs to be, compared for instance to the information
available to a base station.

## Video Session Data Rate for SCONE protocol   {#video-session-data-rate-for-scone-protocol}

draft-scone-video-session-data-rate

Marcus: thanks for the draft, will review. many network elements that
want to do this, with the expectation that we remove shaping, need to
measure this. Need to be careful that we're working to optimize network
utilization.

## Next Steps   {#next-steps}

