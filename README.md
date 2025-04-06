# assumptions-in-cyber-sec
A public talk about assumption in cyber-sec

Assumptions in Cybersecurity: A Presentation-Inspired Analysis

Presenter: Alex BregerTitle: Expect the Unexpected — Interconnected Systems and Dangerous AssumptionsFormat: Converted talk/presentation for technical audiencesTags: Incident Response, Assumptions, Systemic Failure, Stuxnet, NotPetya, AWS, Supply Chain, War Game

Overview

This repository captures the essence of a presentation delivered on the systemic failures and assumptions made in cybersecurity—especially in environments built on complex, interconnected infrastructures.

The goal is to showcase, through real-world case studies, how even mundane or routine actions can cause cascading failures or security catastrophes. It emphasizes the theme of "expect the unexpected" in technical and operational design.

Framing the Problem

The Problem Space:

Over-reliance on operational assumptions

Intertwined and opaque system behaviors

Dependence on third-party systems (sometimes unknowingly)

Fragile automation and procedural blind trust

We assume:

Systems fail predictably

Failures stay contained

Third-party integrations are safe by default

Case Study #1: AWS S3 Outage (2017)

What Happened

During routine maintenance in US-EAST-1, an operator followed an established playbook.

A mistyped parameter caused more servers than intended to be removed.

Two critical subsystems — Index and Placement — were taken offline.

Restarting and validating metadata took hours, resulting in massive outages.

Root Cause

Reliance on a long-standing operation without verifying its effect on scaled-up infrastructure.

Assumptions Broken

We assume routine maintenance is safe

We assume playbooks are accurate

We assume full restarts won’t be needed (because they haven’t happened recently)

Impact

Widespread service outages including:
GitHub, Docker Hub, Travis CI, Slack, Coursera, Trello, Medium, Twilio, SEC, AWS Console, etc.

Takeaway

Scale can silently break old procedures.

Chaos engineering and failure simulations must scale with systems.

Case Study #2: Stuxnet

What Happened

A 500KB worm was deployed via USB into an air-gapped Iranian nuclear facility.

It chained four 0-days, stole digital certificates, targeted Windows + Siemens Step7 PLC software.

It self-updated and spread internally before accidentally escaping into the wild.

Key Tactics

USB propagation in an air-gapped network

Digital certificate forgery

Precision targeting of physical systems

Assumptions Broken

Malware would stay contained within the air-gapped zone

Logic bombs would not leak due to built-in propagation limits (e.g., 3-machine spread, 21-day expiry)

Impact

Widespread infection across unintended hosts globally (Germany, China, Kazakhstan, etc.)

Public exposure forced adversaries to rebuild exploits with new 0-days

Takeaway

Propagation control in malware is not infallible.

Even well-resourced state actors can lose control of weapons.

Case Study #3: NotPetya

What Happened

The M.E.Doc tax software update infrastructure in Ukraine was compromised.

Russian threat actors injected destructive malware into an update which used EternalBlue + Mimikatz.

Malware encrypted MBR, rendering systems inoperable.

Masked as ransomware, but was purely destructive.

Assumptions Broken

Attack would only affect Ukraine

Malware would target users of M.E.Doc and not spread globally

Impact

$10 billion in damages globally

Hit major companies: Maersk, Rosneft, Mondelez, Merck

Critical global logistics and shipping systems paralyzed

Takeaway

Attacks don’t remain localized.

Supply chain attacks can be asymmetric and uncontrollable.

Pattern Recognition: Common Failure Themes

Theme

Explanation

Operational Assumptions

Legacy workflows fail silently at scale

Complex System Dependencies

Small failures cascade into large outages

Over-trust in Containment

Air gaps, role-based limits, controlled propagation often break

Supply Chain Vulnerability

3rd-party trust chains exploited to deploy malware

Mitigation Strategies

AWS Case

Validate playbooks against current system scale

Add constraints to limit operator impact

Simulate large-scale system restarts

Stuxnet Case

Control physical interface access (removable media)

Monitor internal traffic for abnormal peer-to-peer propagation

NotPetya Case

Isolate update infrastructure

Code-signing and auditing

Patch legacy protocols (SMBv1)

Backups and network segmentation

Reflection Questions (for your team or org)

What assumptions does your infrastructure rely on today?

When was the last time you simulated one of those assumptions breaking?

What third-party systems have unchecked trust paths into your stack?

Could a localized compromise become global in your architecture?

Presentation Resources

AWS Postmortem - S3 Outage

IEEE - Real Story of Stuxnet

CSO Online - Stuxnet Analysis

Wired - NotPetya

License

MIT License © 2025 Alex Breger

Disclaimer

This repository captures insights from a live presentation. The examples are real, the commentary is technical. The goal is to raise awareness about systemic risk, not just specific vulnerabilities.

