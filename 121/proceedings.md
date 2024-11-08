Standard Communication with Network Elements (SCONE) WG
Agenda IETF 121 Dublin
Thursday 7 November 2024, 9:30 - 11:30 UTC, Liffey B

https://meetings.conf.meetecho.com/ietf121/?session=33576

# Welcome / Note Well	Chairs (Q. Wu + B. Trammell)

The chairs opened the session and presented the note well and Note Really well. The talked about the goals and the session agenda.

Mohamed Boucadair asked about the reasons why their work are out of scope for the WG. Brian pointed to an email sent to the mailing list and made clear that they have instructions from the AD to keep to the WG scope. Mohamed question this as there have not been any discussion. 

Zahed (AD) thought they had more functionality than throughput advice. Will review again. 

Discussion resulted in an agenda bash: First review charter, then let Network Rate-limit Policies present, then the rest of the proposals. 

Chairs reviewed the charter. 

Gorry: What is the scope of the work, is this for policy limiters or actually path limits or both? Discussion brought up. It is clearly configured limits. It is unclear if one can seperate a path limitation and policy enforcement. 

Lars Eggert, is the endpoint the one causing the bottleneck occupancy, or the IP endpoint, i.e. a Masque proxy? 

Martin Duke, wondered about if "need not be a congestion ..." on Slide 8. Answer, yes that is deliberatle. 

Stuart Cheshire, the motivation for the WG work appear to built on a false assumption. ECN could be used to tell the flow to slow down with less impact than packet losses. 

Dan Drutta it would be good to actually have the use cases documented to make it clear that the main thing are applications volunteerly keeping within recommendations. 

# Discovery of Network Rate-Limit Policies	M. Boucadair
[draft-brw-scone-rate-policy-discovery-00](https://datatracker.ietf.org/doc/draft-brw-scone-rate-policy-discovery/)

Mohamad presented. No clarifying questions. 

# MASQUE signaling extension for media bitrate	M. Ihlar
[draft-ihlar-scone-masque-mediabitrate-01](https://datatracker.ietf.org/doc/draft-ihlar-scone-masque-mediabitrate/)

Marcus presented. Eric Kinnear asked for what usage of Masque that this can be used. Marcus said that can be added. 

Tommy Pauly: are there an internal SCONE throughput signalling format that would be common across multiple protocols? Yes, that is what is intended. 

# TRAIN	M. Thomson
[draft-thomson-scone-train-protocol-00](https://datatracker.ietf.org/doc/draft-thomson-scone-train-protocol/)

Martin presented. 

Ian Swett: regarding if the question if the network nodes needs to know the broad type of the applicaiton. This can't be answered in 30 seconds. 

Brian indicated that this topic might be suitable for the next meeting. 

# QUIC version for SCONE	M. Joras
[draft-joras-scone-quic-protocol-00](https://datatracker.ietf.org/doc/draft-joras-scone-quic-protocol/)

Matt presented. 

Martin Thomson: Clarify that Initials are version 1 specific. The packet is designed to look like a QUIC v1 Initial. 

Francois Michel asked whether another element like a WIFI AP intercept this packet. 

Ian Swett noted that there are some middlebox out there that does not accpet multi initial packets. 

# Flavors of SCONE (+ Discussion)	S. Dawkins

Martin Thomson asked for clarification on Client Initiated. Spencer said this was It was concluded that Train proposal likely are a yes as it requires both client and server to support TRAIN for it to work. Mirja noted that in comparision to other proposals this is a difference. 

Kazuho Oku [missing, something about assymetric paths]

Gorry Fairhurst: Throughput advice has directionality, we might need both. It was also noted that the format of Throughput advice extensibility is something the WG will discuss and is likely to change.

Ian Swett: we need to have a solution that works when QUIC connections migrate to another ephermal port [or IP]. Ian also like to have bi-directional advice. 

Abhishek Tiwari: we need more consensus on the throughput information. What is the process for this discussion? Brian thinks that one can seperate the signal semantics and the possibility to do implementation on a coverged protocol solution.

Dan Drutta: the current proposals are not touching on some things. For example the throughput signal and how to calculate bitrate. Intended to bring a proposal on bit-rate calculation. Next is the question is how frequency of sending the signal to enable efficient processing by the involved elements. 

Ted Hardie notes that a difference between SCONE and TRAIN is that the upstream sender is involved as that might really be necessary for functionality. Proposed a desgin team to have SCONE and TRAIN come to a converged solution that consideres the deployment aspects carefully. MASQUE is an alternative. NLPR ...

Matt Joras notes that the ones that will set the rates are doing this based on economic reasons, and these changes. Concerned that we need to have sufficient extensibility and format flexibility to enable easily adjust to future requirements. 

Gorry Fairhurst: unsure about the impact of the frequency of signal. Also don't see a need to do this for all, only the heavy hitters. So one may not know initial. But getting going is also good. 

Martin Thomson notes that TRAIN doesn't encapsualte, TRAIN and the application protocol are adjacent packets. The security aspect, there are a big difference between the SCONE and TRAIN here to minimize havoc. Brian notes again that the WG should develop what to signal and how in parallel. 

Kazuho Oku we have to look on the security. For example Multiple middleboxes will result in multiple response. 

Tianji Jiang: important to ensure that the operator have sufficent control to say what they want. 

Tommy Pauly supports that Masque solution is a complement and can be used for certain tests during developlement and experimentation especially the through put adive inforamtion itself. 

Sanjay Mishra supports working on what the throughput advice is and enable boundaries as max. 

Ian Swett: less CPU is good. Want something that is multipath and connection migration friendly. Don't need to indicate the traffic type early, that can wait for the future. Injecting packets makes me scared. The field size we can adjust. Supporting moving 

Chris Seal: I am bothered by the single number. Want to give multiple advices at the same time, and avoid needing to update the signal for each video. Persistance.

Mirja Kühlewind: MASQUE is a complement lets start working on it. We need to go through the different main design differences and analyze them from security and deployability. Brian noted that appear a consensus emerging for a Masque solution that uses the same infromation model. 

Daniel Huang what about giving advice across multiple flows for the total forwarding capacity. For communiation across multiple hops, whether protocol message sent from network device from each hop or only one single specific network device

# Establishing SCONE + open discussion	Chairs 

Brian Trammell as chair proposed to do two Design Team one for information model and another from the protocol. Martin Thomson thinks they are too closely realted. 

Spencer Dawkins indicated that more deep presentations would be suitable for a first Virtual Interim. 

Dan notes that there appear confusion about the use cases and what requirements that means. A seperate design team can work on the requirements for the information model. 

Marcus Ihlar thinks two design teams and that they can coordinate. 

Gorry, requests that design team don't go to detailed before ensuring 

Mirja thinks that there should be no design teams, since the charter scope is narrow and we can develop this in the WG and have the authors either agree or develop until there are convergance. 

Zahed:  please don't create two WG within the WG. Want to know how the rate limiting do impact the protocol requirements. 

Intended to schedule one Virtual Interim one per month. The first is to go through the main design points and how the impact things. 


Session ended

# Lightning Talks, Time Allowing

Time did not allow.

## draft-shi-scone-rtc-requirement-01

## draft-ruan-scone-use-cases-and-requirements-00
