# PiholeUnboundWireGuard-Homelab

<h1>Description</h1>
This project integrates Pi-hole for network wide ad-blocking, Unbound for private DNS resolution, and WireGuard to securely extend these protections to my mobile devices while I am away from home.
<br />
<br />
<h2>Step 1: Open your terminal and check repositories for the latest version of all the software on your system.</h2>
<br />

<p align="center">
  <img src="https://i.imgur.com/zQO8Dn9.png" height="55%" width="55%" alt="Terminal"/>
</p>
<br />
<h2>Step 2: Set IP of server to static(Servers should never have changing IPs).</h2>
<p align="center">
  <img src="https://i.imgur.com/2VBYWZM.png" height="55%" width="55%" alt="Network Settings"/>
</p>
<h2>Step 3: Install Pi-hole, Run the installer command in terminal and go through the promts on the blue screen. At the end of the installer you will be given a password WRITE THIS DOWN!!.</h2>
<p align="center">
  <img src="https://i.imgur.com/X7GnKH0.png" height="55%" width="55%" alt=Terminal"/>
  <img src="https://i.imgur.com/A2dq2Az.png" height="55%" width="55%" alt="Blue Screen Prompts"/>
</p>
<h2>Step 4: Install Unbound to make pi-hole independent. Instead of asking google for DNS it will ask the root Servers direcerly.Then because Unbound's default config is empty. We need to create a specific file for Pi-hole compatibility. After the config file Ctrl+X -> Y -> Enter to save</h2>
<p align="center">
  <img src="https://i.imgur.com/p7WywWd.png" height="55%" width="55%" alt=Terminal"/>
  <img src="https://i.imgur.com/bCcQBXG.png" height="55%" width="55%" alt=Terminal"/>
  <img src="https://i.imgur.com/TAcMF7c.png" height="55%" width="55%" alt=Terminal"/>
  </p>
<h2>Step 5: Connect Pi-hole to unbound. Were going to go to Pi-hole's dashboard page which will be http://PiholesIPAddress/admin. There we will go to settings uncheck the dns and then use unbound as a local dns @127.0.0.1#5335 then we will check the Permit all origins box to let the DNS resolver listen and respond to DNS requests from any network interface and IP address as well as making it accessible from VPN's like Wireguard. </h2>
</p>
<p align="center">
  <img src="https://i.imgur.com/fJxMVMU.png" height="55%" width="55%" alt=Pihole Dashboard"/>
