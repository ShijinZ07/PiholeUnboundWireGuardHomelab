# Secure Home DNS & VPN Gateway

<p align="center">
  <img src="https://raw.githubusercontent.com/pi-hole/graphics/refs/heads/master/Vortex/vortex_with_text.svg" width="15%" alt="Pihole"/>
  <img src="https://www.netdata.cloud/img/unbound.png" width="25%" alt="Unbound"/>
  <img src="https://www.computerhope.com/jargon/w/wireguard.png" width="30%" alt="WireGuard"/>
</p>
<br />

<h1>Description</h1>
📌 Project Overview
This project documents the deployment of a privacy-focused network gateway. It integrates Pi-hole for network-wide ad-blocking, Unbound for recursive, private DNS resolution, and WireGuard to securely extend these protections to mobile devices while off-site.

> **⚠️ Disclaimer:** This project was developed in a **controlled lab environment** for **educational and demonstration purposes**. While these configurations are functional, they are provided "as-is." Users should exercise caution and ensure they have a recovery plan before modifying their primary network infrastructure.

### 🚀 Key Features
* **Network-Wide Privacy:** Automatically blocks advertisements and tracking telemetries for all devices on the network without client-side software.
* **Recursive DNS:** By using Unbound, the network no longer relies on upstream providers (like Google or Cloudflare), reducing the data footprint left with third parties.
* **Encrypted Remote Access:** WireGuard provides a secure "tunnel" back to the home network, allowing for secure browsing on public Wi-Fi.

### 📖 Learning Objectives
The goal of this project was to gain hands-on experience with:
* **Linux Administration:** Managing services via CLI and configuring static IP assignments.
* **Networking Fundamentals:** Understanding DNS records, port forwarding, and VPN protocols.
* **Network Security:** Implementing local recursive DNS to prevent DNS hijacking and spoofing.

<br />
<br />

<h2>Step 1: Open your terminal and check repositories for the latest version of all the software on your system.</h2>
<p align="center">
  <img src="https://i.imgur.com/zQO8Dn9.png" width="55%" alt="Terminal"/>
</p>
<br />

<h2>Step 2: Set IP of server to static by going into your router and reserving the IP address so it wont be reassigned (Servers should never have changing IPs).</h2>
<p align="center">
  <img src="https://i.imgur.com/P3XqXnH.png" width="55%" alt="Network Settings"/>
</p>

<h2>Step 3: Install Pi-hole. Run the installer command in terminal and go through the prompts on the blue screen. At the end of the installer, you will be given a password. WRITE THIS DOWN!</h2>
<p align="center">
  <img src="https://i.imgur.com/X7GnKH0.png" width="55%" alt="Terminal"/>
  <img src="https://i.imgur.com/A2dq2Az.png" width="55%" alt="Blue Screen Prompts"/>
</p>

<h2>Step 4: Install Unbound to make Pi-hole independent.</h2>
<p>Instead of asking Google for DNS, it will ask the root servers directly. Since Unbound's default config is empty, we need to create a specific file for Pi-hole compatibility. After pasting the config file, press <b>Ctrl+X -> Y -> Enter</b> to save.</p>
<p align="center">
  <img src="https://i.imgur.com/p7WywWd.png" width="55%" alt="Terminal"/>
  <img src="https://i.imgur.com/bCcQBXG.png" width="55%" alt="Terminal"/>
  <img src="https://i.imgur.com/TAcMF7c.png" width="55%" alt="Terminal"/>
</p>

<h2>Step 5: Connect Pi-hole to Unbound.</h2>
<p>We are going to go to Pi-hole's dashboard page (http://PiholesIPAddress/admin). Go to <b>Settings</b>, uncheck the DNS provider, and use Unbound as a local DNS at <code>127.0.0.1#5335</code>. Check the "Permit all origins" box to allow the DNS resolver to respond to requests from WireGuard.</p>
<p align="center">
  <img src="https://i.imgur.com/Yogimhp.png" width="55%" alt="Pihole Dashboard"/>
</p>

<h2>Step 6: Install WireGuard.</h2>
<p>This allows my remote device to tunnel to my home network. I will be installing WireGuard without scripts because the PiVPN script is EOL and doesn't support Linux Mint.</p>
<p align="center">
  <img src="https://i.imgur.com/wfIjFdS.png" width="55%" alt="Terminal"/>
</p>

<h3>I will be using these commands to create a private/public key pair for the Server and my phone.</h3>
<p align="center">
  <img src="https://i.imgur.com/GuagIdc.png" width="55%" alt="Terminal"/>
</p>

<h3>Create a config file manually (<code>nano /etc/wireguard/wg0.conf</code>) and replace keys with the generated keys.</h3>
<p align="center">
  <img src="https://i.imgur.com/VJoykEb.png" width="55%" alt="Terminal"/>
</p>

<h3>Give WireGuard permission to route the traffic and make it permanent by uncommenting the line "net.ipv4.ip_forward=1".</h3>
<p align="center">
  <img src="https://i.imgur.com/ehjup9B.png" width="55%" alt="Terminal"/>
</p>

<h3>Enable the server.</h3>
<p align="center">
  <img src="https://i.imgur.com/ynO3miy.png" width="55%" alt="Terminal"/>
</p>

<h3>Start the server.</h3>
<p align="center">
  <img src="https://i.imgur.com/1stslgL.png" width="55%" alt="Terminal"/>
</p>

<h3>Create a text file for phone settings (<code>nano phone.conf</code>) and replace the server key and phone keys with the ones generated earlier.</h3>
<p align="center">
  <img src="https://i.imgur.com/svlEz5r.png" width="55%" alt="Terminal"/>
</p>

<h3>Get WireGuard on your phone and scan the QR code.</h3>
<p align="center">
  <img src="https://i.imgur.com/DbKaeIa.png" width="55%" alt="Router settings port forward"/>
</p>

<h3>Open up UDP port 51820 so WireGuard can connect to the home network.</h3>
<p align="center">
  <img src="https://i.imgur.com/C4x7ea9.png" width="55%" alt="Router settings port forward"/>
</p>

<h3>Test the connection.</h3>
<p>On your smartphone, turn off WiFi and use mobile data with the VPN tunnel on. Try to connect to the Pi-hole admin page. If it loads, the lab was successful! and now we have access to our home network outside of our home network and enjoy adblocking and other features.</p>
