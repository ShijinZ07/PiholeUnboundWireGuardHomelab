# PiholeUnboundWireGuard-Homelab

<h1>Description</h1>
This project integrates Pi-hole for network-wide ad-blocking, Unbound for private DNS resolution, and WireGuard to securely extend these protections to my mobile devices while I am away from home.
<br />
<br />

<h2>Step 1: Open your terminal and check repositories for the latest version of all the software on your system.</h2>
<p align="center">
  <img src="https://i.imgur.com/zQO8Dn9.png" width="55%" alt="Terminal"/>
</p>
<br />

<h2>Step 2: Set IP of server to static (Servers should never have changing IPs).</h2>
<p align="center">
  <img src="https://i.imgur.com/2VBYWZM.png" width="55%" alt="Network Settings"/>
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
  <img src="https://i.imgur.com/fJxMVMU.png" width="55%" alt="Pihole Dashboard"/>
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
  <img src="https://i.imgur.com/1Kewbd6.png" width="55%" alt="Terminal"/>
</p>

<h3>Give WireGuard permission to route the traffic and make it permanent by uncommenting the line "net.ipv4.ip_forward=1".</h3>
<p align="center">
  <img src="https://i.imgur.com/GWvW7yZ.png" width="55%" alt="Terminal"/>
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
