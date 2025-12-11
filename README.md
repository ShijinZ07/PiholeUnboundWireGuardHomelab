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
  </p>
  
<h2>Step 6: Install WireGuard so my start device can tunnel to my home network and access pihole and its features. I will be installing WireGaurd without scripts because the PiVPN script is EOL and doesnt support Linus Mint.</h2>
<p align="center">
  <img src="https://i.imgur.com/wfIjFdS.png" height="55%" width="55%" alt=Terminal"/>
  <h3>I will be using these commands to create a private/public key pair for the Server and my phone.</h3>
    <p align="center">
  <img src="https://i.imgur.com/GuagIdc.png" height="55%" width="55%" alt=Terminal"/>
  <h3>Create a config file manually nano /etc/wireguard/wg0.conf and replace Keys with generated keys.</h3>
    <p align="center">
  <img src="https://i.imgur.com/VJoykEb.png" height="55%" width="55%" alt=Terminal"/>
  <img src="https://i.imgur.com/1Kewbd6.png" height="55%" width="55%" alt=Terminal"/>
  <h3>Give WireGuard perrmission to route the traffic and make it permanant.</h3>
    <p align="center">
  <img src="https://i.imgur.com/GWvW7yZ.png" height="55%" width="55%" alt=Terminal"/>
      <h3>Enable the server.</h3>
      <p align="center">
  <img src="https://i.imgur.com/ynO3miy.png" height="55%" width="55%" alt=Terminal"/>
      <h3>Start the server.</h3>
        <p align="center">
  <img src="https://i.imgur.com/1stslgL.png" height="55%" width="55%" alt=Terminal"/>
      <h3>Create a text file for phone settings so you can generate a QR code using "nano phone.conf" and replace the server key and phone keys with the ones generated earlier.</h3>
          <p align="center">
  <img src="https://i.imgur.com/svlEz5r.png" height="55%" width="55%" alt=Terminal"/>
      <h3>Get the WireGuard on phone and scan the QR code.</h3>
  
