# SCONE Minutes IETF 124
*IETF 124 Montreal Tue 4 Nov 2025* 

## Welcome

Chairs reviewed the new note well, kicking the meeting off at 17:00 local time.
Ted Hardie agreed to compete with Gemini as scribe.

The chairs reviewed the working group progress since IETF 123 in Madrid.  There
were 3 interim meetings, working to drive progress.  The base protocol is in
good shape, and we expect a document freeze soon.

## Hackathon, Interop, Demos

## Summary and Actions

- We made good interop progress duing the hackathon Saturday and Sunday.
- The chairs will work with Marcus and Matt to make some form of the demos
  created during the hackathon available.

### Dicsussion

Wesley Eddy reviewed the accomplishments of the hackathon, see
https://datatracker.ietf.org/meeting/124/materials/slides-124-scone-scone-hackathon-summary-00
for details.  A new Slack channel for continuous testing has been set up at
#scone-interop at https://quicdev.slack.com.

The group also saw a demo by Marcus Ihlar, showing playback of video through a
scone network element, comparing scone mode vs. a token bucket policer.
(Looking at this via Meetecho is suboptimal for judging QoE, but the statistics
show that you move from a choppy to a consistent environment.)  The demo is not
yet available, **but the speaker and chairs will work toward a network available
equivalent, and/or video of the demo**.

Matt Joras then shared a recording of a demo that showed scone in the Reels tab
of the Facebook application.  With scone, it uses manifest trimming to keep the
app from buffering.

Jordi asks why their ABR detector is not able to detect the maximum.  The answer
is interaction with user behavior; users swiping away from buffering videos
eventually exhausts the buffer.  Overall, however, improvements to ABR are also
possibile.

Christian notes that there is always a suspicion when you see before and after
videos that folks may not have tried too hard on the "before" conditions.  Matt
confirms that this is the actually Facebook app, and that there has been
significant work.

## Protocol Open Issues

### Summary and Actions

- Martin and Kazuho will make an editing pass on the document, tightening
  vocabulary around SCONE functions and ensuring the text on measurement is
  useful as the semantic definition of the signal.

- The chairs will start WGLC once the revision with these changes is posted.

### Discussion

The group then switched to discussing the protocol document, Marcus Ilhar
reviewing the issues list.  Brian suggests focusing on PR 83 to kick things off.
Zahed and Martin raised the related issue, asking what exactly a network element
is.  Zahed gave a bit more detail, trying to tease out what different functions
the element could exercise.  It knows about flows, can impose policy, and can
enforce.  

Brian showed [these
slides](https://datatracker.ietf.org/meeting/124/materials/slides-124-scone-what-is-a-scone-network-element-scone-00),
pointing out that a minimal SCONE network element just knows how to recognize a
SCONE packet and write a six-bit signal into it, and that all of the rest of the
architecture is optional

He asked the folks discussing the issue to comment specifically about whether or
not he had that wrong.  Gorry said that it seemed on the right track, modulo the
need to have some idea of what to write.  Martin then commented that the slide
showed the right thing, but that the PR did not yet capture that.  Brian asked
if Martin had time to help write up a PR. He said that it touches too much of
the document, as we would have to comb through the document.  There was some
discussion about whether the broader community would or would not understand it
if network element were so redefined.  

Zheng Cai noted that he felt that network element was known as a generic term,
and that there were many different applications which were resource constrains.
Zahed replied to the concern Martin raised, and he and Brian exchanged thoughts
on how these would be referenced by other SDOs (e.g. 3GPP), Sanjay points out
that there are many different network elements in a 3GPP network and this makes
it unclear whose job it is to get this done.  Sanjay noted that you really have
to focus on the idea that this is the element that writes Scone information.
Ted Hardie agreed that the focus should be on the verb (writes) rather than
talking about the noun (network element).  Matt Joras then raised a larger issue
about what is the responsibility fo various things in our overall diagram.
Monitoring is another function, and that might be handled separately. Brian
asked Matt to open a new issue tracking the structural issue about how the
document presents the different functional requirements.

Tianji Jian then discussed the idea these will not stand alone; this is a
function, not a node. There are other things managing provision and enforcement.
Next step, adjust the PR to focus on the functions (verbs) rather than the
elements.

The group reviewed PR #87, which was uncontroversial.  #88 was similarly
uncontroversial and was merged (using "throughput advice"). Zahed agreed that
this looks good.  There is another issue about "sustainable" and "rate-limit"
both being used.  In general it needs a pass to get the terminology to be
consistent. 

Issue #8 was shelved as having been previously discussed and
Christian agreed it could be closed, as there is a section on it now.  Issue 9
was also declared OBE, since the greasing is really at the QUIC layer.

Issue #64 was merged into issue #65. This about policy changes that occur during
a user session; we are looking for guidance here, given that there are potential
issues with immediate enforcement.  Ted suggested that this explain the problem,
but not specify this interval, as there are many different potential resource
interactions there.  Martin noted that you could give assymetric advice; ask
clients to select the lowest throughput which it has been sent, but ask the
enforcement only to use the largest that has been sent.  That would give the
best result.  

Zahed noted that this advice is likely to be unread or be subject to later
deployment experience.  Marcus stated that he wants some level of advice, even
if it was just setting basic expectations.  Zahed notes that folks will code
this and then have to consider when to change it.

Brian said that we needed to do this, to confirm that there was an improtant
exercise in demonstrating that there was an operating window that made sense.
But do we need to have that shipped as a defaut parameter?  Martin says yes.
What we need to ensure is that the semantics of the signal are clear, and how
the monitoring works is part of the semantics.   

Martin and Kazuho will write an update to this, possibly including pseudo-code
for an appendix, showing one way you could do this.  

Issue #75 will be closed after seeing Martin and Kazuho's text is available.  

Brian, as chair, says that it would make sense to have an interim sooner rather
than later, as a forcing function to get this all resolved.  Martin counters
with a proposal that we schedule a working group last call.  Gorry, as an
individual, asks whether or not there is one Scone funciton or two?  Scone
writes are the core function; the monitoring is a requirement of delivering the
semantics of the overall system. 

Zahed notes that in his network there are other ways of monitoring, and that the
monitoring generally speaking does not have to happen on the same network
elements.

## Applicability and Manageability

### Summary and Actions

- The applicability and manageability document is adopted up to section 3; the
  working group will decide in the future what to do with the remaining,
  network-architecture-specific text. 

### Discussion

The group then moved onto the discussion of applicability and manageability.
Sanjay Mishra led the discussion based on [these
slides](https://datatracker.ietf.org/meeting/124/materials/slides-124-scone-applicability-manageability-draft-02).
See slide 5 for the key changes in draft-03, which responded to the discussion
held during the call for adoption.

Lars Eggert asked about the 3GPP references justified on slide 6: can you
clarify who is the audience for this document?  Sanjay replied "the operators"?
Lars, "why"?  Sanjay wants any network operator who wishes to deploy scone on
their network to know that they do not need to write new specs to incorporate
this ; it works on 3GPP networks as a "vanilla" deployment.  Lars notes that
this is still a very 3GPP oriented documents, 5G is written, and the other TBDs
are for other networks.  If this is adopted, the chairs will appoint editors and
make sure that the TBDs are filled in. Lars notes that he would want this
information from 3GPP or Cablelabs if he were an operator.  Can we make this
high level, and leave the details to the ssytem engineering SDOs?

Lars fundamentally believes that we cannot say that it does work on X's network;
that is up to X.  Marcus continues the discussion by saying that we can
certainly discuss what level this advice needs to be, but that he believes we
should adopt the document as we need a document of this sort.  Tianji notes that
not many people are involved in both IETF and 3GPP, and so a liaison would be
more effective if there were a document that could provide background for the
95% that are not that familiar with the IETF side. 

Martin Thomson refined Lar's concern by focusing on section 3.  It is generic,
and that's very appropriate for the work here.  He is less comfortable with 4,
5, and the TBD sections, as those are not appropriate for the IETF to dictate.
An appendix with an example stating what a reasonable deployment architecture
might be would be acceptable, but we need to be careful about straying across
the line into defining other groups' network architectures. Sanjay notes that
where the work is in the document doesn't matter at this point, because this is
an adoption call and we can change all that.  Martin responds that this is a
scoping question.  Right now, it says we are signing up for a scope of work that
might be beyond our competencies.  Zahed stepped in to agree that we should
focus on saying that this is our take on it, but not attempt to declare a
speficic mandatory approach.  We do need to clarify what needs to be implemented
and then how it might be deployed. The tone must remain non-normative. 

Brian points out that there have been several different audiences named for this
document--SDOs, operators, vendors.  That's a lot of text and a lot of work.
For adoption, he asks whether it is appropriate to simply pull that into an
appendix and note that this will be handled in the working group process.  Brian
says that he really doesn't want to specify documents in some other SDOs'
processes; he is a zero appeals chair, and he want to keep it that way.

Mirja says that the right direction is to ask 3GPP what advice they need.  Zahed
replies we probably not focus on the liaison aspect, but on writing what we need
to write. Mirja notes that the discussion is ongoing at 3GPP and that they don't
need our our input at this time.

Gorry as AD.  We have a chartered milestone for this and we have some things in
the protocol spec that need to move here, and so we should probably adopting
section 3.  You could write a totally separate document for the other sorts of
networks.  It's not in the charter, but it fits in it. 

Sri Gundavelli said that he would be willing to provide text on Wi-Fi, and that
he generally supports the approach of a new document with no normative language.

Brian put forward a poll.  "Do you support adoption of -03 as the basis of a
working group -00 for the applicabilitya and manageability milestone, to section
3 only?"

**21 yes responses, 1 no response, 5 no opinion responses.**

Brian believes that represents rought consensus, and he wishes the editors to move forward on that basis. 

The chairs reviewed the discussion and discussed planning for an interim meeting in early 2026, focused on interoperability testing. 

There being no other business, the meeting adjourned at 18:47.