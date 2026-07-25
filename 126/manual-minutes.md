SCONE@126
=====

Marcus reported on activity during the Hackathon
Chairs reported on document status

The future of the WG
-----

Scone Protocol Completion
-----
Martin reports that there is nothing new to report, except for small editorial updates. 
Brian asks if editors are ok to push the button (progress to IESG). Martin would like that.
Gorry AD: Have a look at the list and then click the button. 

Applicability and manageability
-----
Sanjay presents 01 to 02 changes, a substantial rewrite of the document.
Goes through open issues and corresponding PRs

Issue 49: Lars Eggert talks about introducing language around misbehaving applications, it is moving away from the original intent of this work of being advisory and helpful.

48/55: Qin: is Joe from OPSDIR happy with the changes? a: yes

Zahed: agree with Lars. This is a result of questions about "what happens if detection doesn't happen...". It anseers the question about what the operators can and should do.

Lars: just because you got a review, doesn't mean you need to follow it. What do you do with other traffic that isn't SCONE. If you treat SCONE traffic that doesn't react as expected as less-than-BE, that might be a problem. 

Zahed: This is a class of BE, perhaps. But we can soften this language.

Lars: There' a lot of non-SCONE traffic. You already need to do something for that. Nonreactive SCONE traffic should be treated the same way.

Zahed: that's fine... 

Gorry: I don't like a lot of the words here. Monitoring is okay. I don't like violation. I don't like conformance. You might want to protect the network. I like the paragraph. Need to choose different words.

Marcus: Reactive scone packets might get different treatment... But the main point is that a reviewer picked up these kinds of concerns and suggestions, which might suggest we need to check the rest of the document.

Mirja: I think the issue is wrong. This is more about misunderstanding the document, this should be clarification. Either the network wants to enforce or not.

Gorry: When I look at SCONE, I turn the SLA enforcer off.

Mirja: Three options here: endpoint above enforcement, ndpoint below enforcement, optimization. Independent of scone.

Christian: SCONE is not RSVP. In appman, it's not about giving privilege to any particular flow. The point for me, a flow signal shall not change the management. 

Brian comes up with words that are more likeable. Reactive or non-reactive instead of compliance.

Christian: NO! It doesn't matter to the network. 

Martin put some suggestions on the PR while people arguing, claims that we all violently agree. Gorry states that we almost violently agree.

Brian, let's capture this on the PR.

Kazuho certain applications like browsers may signal scone but not know whether specific applications actually use the SCONE signals. 

Issue 20/PR 37: MASQUE and SCONE. 
Mirja: the text is reasonably fine. Also, this should be more general tunnel considerations and not just MASQUE. Text looks fine

Marcus: Either drop this or put some general tunneling considerations. 

Lars: there is an intarea tunnels doc from Joe Touch. Don't know where it's going. We could just use/reference that.

gorry: I don't want a dependency on the document, though it is a good source of text.

Zahed: This is not harmful, but not sure we need it... what to do is up to the client anyway.

Mirja: this is not generic, this is about masque... It sounds like you want less text which is fine. Please let me know.

Martin: "client should take the minimum of two values", which is not correct, each piece of advice applies to the flow on which it was received if you have quic-on-quic tunneling. What you have is fine, it's just a large expansion on that basic idea. 

ECN/L4S and SCONE: Feedback provided on list

Stuart remains unconvinced by this. Discusses possible use cases around rate limiting video traffic.

Martin: that's a very pragmartic position. There is value to having transparency about those practices.

Marcus: Most operators built these shapers a decade ago and haven't touched them since.

Christian: recognize when you have testing traffic ... 

Stuart: something something volkswagen

Christian: +1 to Martin about transparency

Mirja notes that the document give a lot of advice for operators, but little to endpoints. Maybe remove all guidance for endpoints and just call the document manageability. 

Brian suggests that we engage the list to help drive the number of open PRs to 0 before IETF 127.

Zahed: we don't need to wait for IETF 127, let's resolve the PRs. It'll never be perfect, let's push it out. 

Brian refers to discussions here that might be PRs, people will go on vacation etc. We just want to give some time.

Gorry: ADs also have holidays.. there's time for the WG to get this right. We need to settle Mirja's comment on removing applicavbility. 

Brian, maybe it's just a piece of text cut less than 10%, and change of title.

Gorry: if it's less disruptive it might be ok, but let's be clear on what we do. 

Zahed: having applicability in there causes no harm.. but fine with what WG will do. 

Mirja: likely less that 1/10 of text, no full sections would need to go, just small rewrite. 

Brian: This would be an easier discussion around a concrete PR. Volunteers Mirja. 

Gorry: do we want to send them together or separately? are we really going to get these together in half a cycle?

Marcus: there is some urgency here

Matt + Zahed: agree.

Zahed: Waiting a month is fine from a 3gpp point of view. If we won't get it done by December, though... 

Sanjay: document is pretty tight

Mirja: I'd like to send the protocol now, it's a clear signal that we're done here. Up to the AD how long they take... but want it out of the WG.

Anoop: Agree with Marcus. Important to advance protocol.There is a real urgency for protocol doc to move to next stage both from 3GPP and field deployment stand point.

Marcus: Protocol does a good job of being self-contained.

Brian: After vacations people will be able to close the PRs, give people some time to digest/discuss and ideally we can have a WGLC by October. 

Future of the working group
-----
Related documents: SCONE echo, Martin Duke, fairly positive reception. If people want to work on it, great, if not, also ok. Google will probably implement anyway. Urges people to share feedback on privacy aspects etc. 

Brian: are there other venues than SCONE where you can get the feedback.
Martin D: QUIC is a likely a good fit, this being a QUIC extension. 

Martin T: The working group will likely need to stay open for managing publication. No urgency to close now, or close later. Related documents can go to other groups.

Lars: close the group once you get RFCs and other stuff can be dispatched elsewhere. If you really need some of this, put the energy in now. 

Martin D: what do I need to do to make it more ready (recharter required)? Nag people to file issues? Will solicit comments from the list. 

Brian: you can get it ready in parallel with possible recharter and WGLC.

Gorry: Only one on this list is simple; scone-echo. Read it and comment, it may possible fit the charter. The others are extra work for the AD. 

Zahed: agrees that closing the WG is a good way to signal that we're done. Let's decide at IETF 127.

Mirja: no strong opinion on QUIC echo, but it belongs in QUIC

Tianji: New scenarios and technologies want to use these principles. Proposes to keep SCONE open, QUIC was a starting point, new charter can relax that. 

Martin D: re parallel calls, implementations. 

Lars: RoCe works through tight integration, you already have more knobs than SCONE, doesn't see how SCONE adds anything. 

Tianji: RoCe challenge, long RTTs may impair convergence.

Gorry: RoCe doc looks like tsvwg. 

**Brian: If you have interesting engineering work for SCONE that would need recharter, have it ready for IETF 127**

Gorry: The original concerns around the initial SCONE charterin likely applies to the SCONE echo. 

Brian: there is also interest in the SCONE API space, just like other proposals, be ready for IETF 127. 

Tianji: Potential 6G architecture might make masque for scone a viable option. 

Tianji: Regarding app-man, it refers to what we do now with QUIC. New SCONE work might influence applicability and manageability. 

Brian (as individual): Possible new protocols should handle that in operational considerations sections. 

