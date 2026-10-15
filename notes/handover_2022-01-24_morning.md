# Shift handover -- morning of 2022-01-24

Analyst on shift: Dana Ortiz (SOC, tier 1). SOC manager: Lena Yamamoto.

Between 03:57 and 03:58 UTC intranet-server raised 548 level-10 alerts "Multiple web server 400 error codes
from same source ip", all from 172.19.131.174. Dana Ortiz escalated intranet-server to the SOC manager.
Lena Yamamoto reviewed intranet-server. Because 172.19.131.174 belongs to the vpn host, she did not block it;
the VPN session logs will be checked instead. Mina Lee, who owns intranet-server, has been told.
