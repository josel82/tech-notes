# Troubleshooting Dante Networks
#Dante #VoIP #Networking 

A good way of troubleshooting a Dante Network is by dividing the problem into categories:

## Device discovery problem
- Devices aren't showing up? chances are there is a problem in the network. 
- Is 5353 port been blocked?

## Clocking problem
- Check the clocking status in Dante controller. There should only be one clock leader
- Many clock leaders? You've got a clocking problem.
- Maybe caused by jitter?
- Check that ports aren't blocked. 
- For 100mbps networks IGMP snooping is necessary.

## Media packet problem
- Out of flows?
- Sample rate mismatch?

## Latency problem
- Check the latency charts in Dante controller.

| Protocol | Transport | IP/Port |
|---|---|---|
| Discovery mDNS | Multicast (UDP) | 224.0.0.251:5353
| Clocking PTP | Multicast (UDP) | 204.0.0.129-132:319-320 |
| Audio/Video | Unicast (UDP) | \[Receiver IP]:14336-14600 |
| Audio/Video | Multicast (UDP) | 239.254.x.x:4321 |
