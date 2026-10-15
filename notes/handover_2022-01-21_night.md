# Shift handover -- night of 2022-01-21

Analyst on shift: Sam Whitaker (SOC, tier 2).

Sam Whitaker reviewed the vpn host after a run of "Multiple IDS alerts for same id" alerts. Most of them
come from 172.19.131.174, which is the VPN gateway's own address, so they look like normal tunnel noise.
At 12:58 UTC there was a level-10 "Multiple IDS events from same source ip" alert on vpn from the external
address 213.13.146.142; Sam Whitaker blocked 213.13.146.142 at the perimeter as a precaution.

Sam Whitaker also reviewed inet-firewall. Nothing there needs escalation. Tess Baker owns both vpn and
inet-firewall and has been informed.
