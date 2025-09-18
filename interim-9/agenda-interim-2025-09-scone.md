# SCONE interim meeting, 16 April   {#scone-interim-meeting-16-april}

## TRONE Issue Scrub   {#trone-issue-scrub}

### Issue 15: TRONE with ICE   {#issue-15-trone-with-ice}

No action: let's keep this open, but we're chartered to do QUIC first.
Save for recharter

### Issue 7: TRONE ACK   {#issue-7-trone-ack}

Dan Druta: value of the ack is to make the communication efficient, by
allowing tracking of signal freshness.

Renjie Tang: I proposed this so the network element could switch from a
generic limiter to one that's tuned to the SCONE window. I'm okay with
the element taking SCONE signaling as an implicit indication.

Marcus: I wouldn't trust an ACK more.

Sanjay Mishra: please put your comment in the issue. Explicit ACK can
reduce overshoot by using longer horizon before enforcement.

Marcus: Agree we need a signal to switch to longer window. Still think
the willingness to participate is more trustworthy than an ACK.

Kazuho: +1 Marcus. Return path might go through a different middlebox,
so you don't see an ACK. This behavior is fragile.

Christian: Concerned about the mechanism by which a TRONE packet sets
state in a network element, because the are very easy to forge. The more
state you keep based on one, the more you are vulnerable to such state
attack. I think we're making a stateless protocol. The ACK discussion
makes me think we're considering being stateful, and that makes me
uneasy. We should put advice to this effect in the text.

Marcus: One of the intended use cases is allowing throttling to be
disabled. That's state.

### Issue 20: time window   {#issue-20-time-window}

Ian Swett: Do we have an issue about how often we're supposed to send
these? Signal could be good for a minute, but packets might get lost. We
need to tolerate packet loss.

Marcus: We want to give lightweight advice.

Martin: we're using QUIC, you know the packet was lost.

Ian: oh right. 20 sec is still good.

Anoop: don't think we've had enough discussion to know 20s is correct.
We'll have experiments at the next interim.

### Issue 19: privacy considerations with multiversion   {#issue-19-privacy-considerations-with-multiversion}

Kazuho: there's some complexity here, sender has to send two types,
receiver has to understand both. Could have sender always sent TRONE2,
middlebox can drop to TRONE1 if necessary.

### time check from the chair   {#time-check-from-the-chair}

Brian: Does anyone see any other issues that would affect their decision
to adopt?

(no response)

### PR 23: TRONE indication   {#pr-23-trone-indication}

no comments, merge it

### PR 13: DoS on stateful TRONE   {#pr-13-dos-on-stateful-trone}

Christian: no unauthenticated communication should change state. for
deployment reasons, we can't do auth. Important to have this in the doc
early.

merge it.

### PR 16: congestion control interaction   {#pr-16-congestion-control-interaction}

Marcus: This is a great discussion. It is a long discussion. Important,
these areas are easy to conflate. Not sure it needs a merge before
adoption.

Christian: I was asked to prepare this at Bangkok. We need clarity from
the beginning. General trend in the IETF: "you should use ECN". Should
start that discussion.

Gorry: CC should be quite separate from TRONE. We need text here, I'm
not sure what we need to say beyond this is separate. There are nuances.
You're going to change rate based on what you see.

Christian: The link is loose. It's a fact that the SCONE signal will
make its way into the congestion controller

Resolution: Christian to take the text after the first paragraph to an
issue

### Bike Shed   {#bike-shed}

Calling the merged protocol SCONE would make everyone's life easier.
Need to check with all TRAIN

### Call for Adoption   {#call-for-adoption}

14 yes, 0 no.

Dan Druta: I hope by adopting this that we're rolling missing pieces
back into the protocol.

## draft-mishra-scone-usecase-01   {#draft-mishra-scone-usecase-01}

Marcus: the protocol should allow for changes to policies, which doesn't
necessarily require network-injected packets, but the requirement should
cover timely signaling.

Adopt for applicability/manageability?

Marcus: This is a useful document to track requirements, we should keep
it alive. Requirements probably don't need to be published as an RFC.

Christian: Issues that come from the requirements should be discussed on
the protocol document, and should be tracked as issues there. If these
diverge, we have a problem.

Sanjay: Intent is to have requirements... this document is defining what
the network element is. That's probably still meaningful. Requirements
from the network point of view are still useful to keep around. Wanted
to make sure these were captured.

Christian: What happens when the protocol doesn't match the
requirements. Which do we change?

Sanjay: Three requirements are important here. One led to PR 23, dynamic
update leads to 21. Until there's a balance, we need to track the
requirements.

Dan: Document useful. Combination of requirements and applicability.
Adopting the context and applicability on mobile networks is very
useful.

