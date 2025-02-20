# My Home Server

This is a brief overview of the hardware and software used in my home server, and why I chose it.

## Requirements

- Large amount of storage for media and backups (>10TB)
- Enough processing power for a couple minecraft servers
- 32GB RAM or more for minecraft servers and other services
- Dedicated hardware for media transcoding
- Cheap

## Hardware

Using the above requirements, I chose the following components:
(PCPartPicker List: https://au.pcpartpicker.com/list/GyFBPJ)

- i7 4790 w/ free stock cooler
- 32GB G.Skill Ripjaws
- 2x Seagate Barracuda 8TB drive
- 1x WB Blue 8TB drive
- Gigabyte GTX 1660 super

<p align="center">
  <img src="https://github.com/user-attachments/assets/cb8a476d-fa60-4c86-b741-553b08d0b673" width="45%" />
  <img src="https://github.com/user-attachments/assets/dcaf102e-f819-49b9-b280-9b9a732a62a4" width="45%" />
</p>


The i7 4790 was chosen as it was still quite powerfull, with enough single and multi-threaded performance and high abundance in the used market. 32GB was the max RAM supported by this CPU, so thats what I got. For the Hard drives, I knew I was going to go with 2 storage drives and 1 parity drive. The cheapest drives on the market were the Seagate Baracuda's, however as they are SMR (Shingled Magnetic Recording) drives, if I used this drive for parity, it could cause premature wear and failure. Hence, I used the more expensive WD Blue drive for parity as its CMR (Conventional Magnetic Recording) and the cheaper SMR drives for storage. Finally, the GTX 1660 super was chosen as it had the latest encoders/ decoders able to decode in AV1, and was cheap in the used market.

## OS

For the OS, I looked into running a linux distro and using software Raid. However in my research I saw that Raid wasn't very ideal as I could risk losing *all* my data in a multiple drive failure senario. This turned me to Unraid, which took a very simple strategy towards parity, allowing the data of the working drives to remain untouched even in the case of multi drive failures. Additionally, there seemed to be a lot of online support around Unraid with the applications I had in mind.

## Networking

From the beginning, I wanted to be very safe with how I handled exposing my server to the internet. I firstly tried an nginx reverse proxy with Let's Encrypt for certificates, providing a little bit of protection with some firewall rules etc, but it still exposed my public IP to users. What I wanted was a reverse proxy in the cloud, providing another level of isolation from my home server. This is when I came across Cloudflare's Zero Trust Tunnel service. This service builds a secure tunnel between Cloudflare's proxy server and my server, hence not requiring port forwarding. Additionally, they by default provide basic protection against DDoS and handle https certificates automatically! All I had to do was install the Cloudflare Tunnel client on my server.

I used Cloudflare's tunnel to proxy all my http based services, but unfortunately this tunnel doesn't support niche protocols like the Minecraft server protocol. To reverse proxy my Minecraft servers, I looked into getting the free tier VPS from Oracle, but they seemed to have shut that program down as they denied my request. With no other free options, I was left to just port forward my Minecraft servers, and add a DDNS client on my server to update my IP on Cloudflare's DNS service.
