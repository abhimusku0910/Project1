# Network Setup

## Assumptions

The business is a small accounting services company in Brisbane with 8 employees – 1 Manager, 4 accounting staff, 2 administrative staff and one IT support. The website displays the basic information about the business, details of the project, student names, student ID and current date.

## OpenWRT and VirtualBox Setup

The lab network used an OpenWRT VM in VirtualBox. The Windows host connected through the host-only adapter `192.168.56.1/24`, while OpenWRT used `br-mng` at `192.168.56.2/24`. Interface `eth0` was bridged to `br-mng`, and `eth1` was used as the WAN/NAT interface. Connectivity was confirmed using ping, and the website was hosted from `/srv/www/index.html`.

![OpenWRT ip addr output](./images/openwrt-ip-addr.png)
*Figure 1: OpenWRT IP address configuration using the `ip addr` command.*

![OpenWRT ip route output](./images/openwrt-ip-route.png)
*Figure 2: OpenWRT routing table showing default and local network routes.*

![OpenWRT network configuration](./images/openwrt-uci-network.png)
*Figure 3: OpenWRT UCI network configuration for LAN and WAN interfaces.*

![Windows host-only adapter](./images/windows-ipconfig-hostonly.png)
*Figure 4: Windows host-only adapter configuration using `ipconfig`.*

![Successful ping test](./images/windows-ping-success.png)
*Figure 5: Successful ping test confirming connectivity between host and OpenWRT VM.*

![Website HTML file](./images/openwrt-website-html.png)
*Figure 6: HTML source code of the hosted website stored in `/srv/www/index.html`.*

![Website in browser](./images/browser-website-success.png)
*Figure 7: Website successfully accessed through the browser.*

![Lab Network Diagram](./images/Lab%20Network%20Diagram.png)
*Figure 8: Lab network topology showing VirtualBox, OpenWRT, and host-only network connections.*

[View lab network draw.io file](./Lab%20Network%20Diagram.drawio)

## Firewall Configuration

Firewall rules were tested with before-and-after evidence. HTTP port 80 was allowed, then blocked using `Block_HTTP_Test`, making the website inaccessible. The rule was then changed back to `ACCEPT`. SSH was changed from port 22 to 2222, ICMP was blocked and re-enabled, and management access on port 81 was restricted while port 80 remained accessible.

![HTTP firewall rule edit](./images/firewall-http-rule-edit.png)
*Figure 9: Firewall rule configuration used to block HTTP traffic on port 80.*

![HTTP rule in UCI output](./images/firewall-http-rule-uci.png)
*Figure 10: UCI firewall configuration showing the HTTP blocking rule.*

![HTTP blocked in browser](./images/http-blocked-browser.png)
*Figure 11: Browser output showing HTTP access blocked by firewall rules.*

![SSH port 22 success](./images/ssh-port22-success.png)
*Figure 12: Successful SSH connection using the default port 22 before modification.*

![Dropbear changed to port 2222](./images/dropbear-port-2222.png)
*Figure 13: Dropbear SSH service configuration changed from port 22 to port 2222.*

![SSH port 22 refused](./images/ssh-port22-refused.png)
*Figure 14: SSH connection attempt on port 22 refused after port modification.*

![SSH port 2222 success](./images/ssh-port2222-success.png)
*Figure 15: Successful SSH connection established using port 2222.*

![ICMP ping before block](./images/icmp-ping-success-before.png)
*Figure 16: Successful ICMP ping test before firewall restrictions were applied.*

![ICMP firewall rule](./images/firewall-icmp-rule.png)
*Figure 17: Firewall rule configuration used to block ICMP traffic.*

![ICMP blocked](./images/icmp-ping-blocked.png)
*Figure 18: Failed ICMP ping response after ICMP traffic was blocked.*

![Management port 81 rule](./images/firewall-management-port81-rule.png)
*Figure 19: Firewall rule restricting management access on port 81.*

![Port 81 blocked and port 80 working](./images/management-port81-blocked-port80-working.png)
*Figure 20: Port 81 access blocked while web access on port 80 remained operational.*

## Production Network Design

The production design includes an OpenWRT router/firewall, staff LAN, DMZ web server, management network, and internet connection. The production IP scheme uses `90.x.x.x` addresses based on student ID `12317190`.

![Production Network Diagram](./images/Production%20Network%20Diagram.png)
*Figure 21: Proposed production network topology including LAN, DMZ, management network, and internet connection.*

[View production network draw.io file](./Production%20Network%20Diagram.drawio)
