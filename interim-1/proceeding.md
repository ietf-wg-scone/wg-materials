SCONE Interim -- 12 December 2024

**\*\* Consolidation of SCONE and TRAIN (Marcus Ihlar) \*\***

See slides.

**\*\* Signal Format \*\***

Jonathan: TRAIN has the information at a specific offset, which might be
easier for routers? I think that was an important motivation, but don't
know if it's a real constraint.

Marcus: This is an infrequent signal, maybe not a big deal.

Ian: Internally, 6 bits is probably enough. More information = more
risk. We need strong suggestions about how often to send these. More
bits could provide frequency guidance.

Hang Shi: Does SCONE put it in an encrypted QUIC payload?

Marcus: Not really, just obfuscated like a QUIC Initial. MASQUE is what
gives you confidentiality.

Abishek: Too early for payload decisions. There is wide variety of
expressions of throughput out there. We could write an I-D about it.

Brian: Can you publish before a future interim?

Abishek: Yes, not January, but before Bangkok.

Brian: If you have data about this, please go see Abishek.

Ted: In the train protocol, the server creates the space for the signal,
but a different network element sets it. So we may want to define
sending the signal in some way that doesn't require a channel between
the shaper and the server (e.g. RTTs or time). For the payload, it seems
like we are mostly asking folks to reduce their user experience to lower
the required network resources. If we are always saying "go down a bit",
the the signal may be simpler, since the number of choices to make (e.g.
with ABR video or similar) is not infinite at the actual application.
"Reduce your QoE just a bit, please" may be a sufficient signal, if we
can vary the "just a bit" in strength.

Marcus: There are many operator policies out there. We should collect
more requirements.

**\*\* Packetization \*\***

Ian: I prefer not creating more packets. Prepending is better. Fate
sharing also helps with loss detection -- If I got ACK for the QUIC
packet, the TRAIN packet probably made it.

Marcus: That doesn't tell us if any element inserted information.

Matt J: I agree it's good to couple the packets. SCONE precursors did
this, it's technically feasible. The spoofing rationale isn't
convincing. There's no way to authenticate that the TRAIN packet origin
is from the QUIC endpoint.

**\*\* Signalling Frequency \*\***

Sanjay: Changes in policy come from the network side, so that's a more
natural origin for the decision to send advice.

Ian: In SCONE, elements are doing more packet inspection, which is sad.

Nick: I'm not convinced the network can inject packets with the correct
connection ID. If there's migration, you don't even know what the
connection ID length is.

Marcus: The endpoint generates a SCONE packet that tells the element
what the CIDs are. The endpoint would have to resend SCONE on
tuple-change.

Martin: To me, the signal format is almost orthoganal to the core issue;
the other properties are more important. I prefer Train, barring its
signal timing issue, but I think we can tackle that with a TTL and some
sender heuristics. That gives us the fate-sharing and authentication
properties ofr Train that I prefer.

Ted: In WebRTC we baked off various proposals and merged them. The
product got more edits to be unrecognizable. If the current authors can
work together, then picking either is fine. I prefer TRAIN as a basis
for the same reasons as Martin.

Brian (hat on): Many good questions, we understand the tradeoffs. +1 to
Ted; pick one and get started. Can we nominate a subset of authors to
elect an editor? A concrete proposal would be better than a pointless
binary vote on picking one.

Marcus and Matt are both willing to help, but TRAIN authors are not
here.

**\*\* Throughput Advice Object (Med) \*\***

(see slides)

Med presents slides on their effort to create a reusable blob. Their
second goal was to know what information was available on the network
side. The third goal was to identify the subset of the information
available that was useful to the application. He presents a simplified
reference architecture (see slide 3). He wants to define an architecture
that sends data to the host and the content emitter. The authors use
CDDL to defined a generic blob structure, that is then mapped to the
encoding specific to the channel.

Marcus: This is maximalist approach, which includes a lot of policer
configuration. What can an application do with all this?

Gorry: (Re: Is PHB/Class ID something to add?) The packet has a DSCP. Is
that not the scope of the response, or will there be a map of all the
PHBs?

Med: Jason would have to answer that.

Marcus: Do we need more granular traffic categories?

**\*\* SCONE Experiments (Abishek) \*\***

(see slides)

Marcus: We should do tests on what signal is useful to the application.
Operators will have to share data to make some of this work.

Lucas: How can I describe SCONE to product managers? Having a QoE
improvement number would help to pitch it. Constraints are fine.
Openness is great but private testbed results are also welcome.

Sanjay: Performance measurement will drive deployment.

Brian: I will get a hackathon table in BKK. What do you think about
that? What's the first thing we could do by then?

Abhishek: We should be able to do something given the enthusiasm, not
sure what.

**\*\* Wrapup \*\***

Brian: next interim scheduling will go to the list. We will not use
Zcal, and will find a way to include the TRAIN authors. One or two
meetings before BKK.

Ian: Renjie Tang wrote a short draft about conforming to sent signals.
Not using the policer has improved QoE a lot.
https://datatracker.ietf.org/doc/html/draft-rjt-scone-conformance-signal-00

