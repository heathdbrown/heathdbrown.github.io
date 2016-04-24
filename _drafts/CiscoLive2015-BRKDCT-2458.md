NXOS Maintenance Best Practices
Cisco Live 2015
BRKDCT-2458
PDF: http://d2zmdbbm9feqrf.cloudfront.net/2016/eur/pdf/BRKDCT-2458.pdf

VPC Best Practice
* VPC Domain IDS
** use unique vpc domain ids within a contingous L2 domain to avoid MAC overlap
* VPC Peer Link
** Should be point-to-point connection & dedicated links
* VPC Keeapalive Link
** Dedicate control plane in a dual-supervisor environment. Use management switch
* VPC Peer Gateway
** Acts as active gateway for frames addressed to peer switch. Avoid Peer Link forwarding.
** High Impact/Easy to Implement Quick win
* VPC Peer Switch
** Optimizes BPDU Processing, single logical L2 entity
** High Impact/Easy to Implement Quick win
* Distribute port-channel member interfaces across line cards within the same chassis
* Create a map for oversubscription aligned to current and future demand.
** Deployment practive -- 20:1 at access and 2:1 at Core

* VPC Auto Recory
** During the scenario of loss of peer link the secondary places VPCs into suspended state.
** The VPC KL goes down and the secondary receives no keep alives
** AFter missing 3 keepalives S2 changes role to VPC primary
** Used when peer-link fails and after period of time VPC KL fails
** Both VPC peers are reloaded but only one comes back up

* VPC Self-isolation
** used for the case no vlan up on peer link, which takes down vlan for the entire Vlan domain.
** Caused by misconfig, hardware programming error.

* VPC Object Tracking
** Used for better isolation on faults

* SSO
** Stateful Switch Over

* Routing Protocol
** NSF takes signaling to push over the state to the standy sup
** NSR continues to place routes on the standby supervisor
** NSF = Graceful Restart
** NSR = Stateful Restart

* Standalone Chassis Redundant Core
** enable BFD on all OSPF neighbor links
** Adjust OSPF SPF Throttling timers

* Case Study of VPC Tranditional change
** Routing Protocol Best Practice
** VPC best Practice
** HA Best practice

