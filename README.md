# SSH

<h2>Description</h2>
Configure SW2 with what is necessary for a secure SSH remote connection through the console line connected to Laptop1's terminal.

- <b>Cisco Packet Tracer</b> (2.2.43) <br />

- <b>Cisco IOS C2900 Software, Version 15.1(4)M5</b>  <br />

- <b>Cisco IOS C2960 Software, Version 15.0(2)SE4</b> <br />

[Software Configuration Guide](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3650/software/release/16-3/configuration_guide/b_163_consolidated_3650_cg.html)<br />

<h2>Diagram </h2>
<img src="https://i.imgur.com/SL5T1cg.png" height="80%" width="80%" />

<h2>Walk-through:</h2>
Configure hostname, enable secret password, user with a username and a password, SVI VLAN 1 IP address, and default gateway. Verify results with 'show run'.
Switch(config)#hostname SW2<br />
SW2(config)#enable secret ccna<br />
SW2(config)#username jon secret ccna<br />
SW2(config)#int vlan1<br />
SW2(config-if)#ip address 192.168.2.253 255.255.255.0<br />
SW2(config-if)#no shut<br />
SW2(config-if)#exit<br />
SW2(config)#ip default-gateway 192.168.2.254<br />
<img src="https://i.imgur.com/l2SleEu.png" height="80%" width="80%" />
<img src="https://i.imgur.com/QFQLbIG.png" height="80%" width="80%" />
<br />
<br />
Configure line console 0 with local user authentication and an exec session timeout.
SW2(config-line)#login local<br />
SW2(config-line)#exec-timeout 5 0<br />
SW2(config-line)#do show run<br />
<img src="https://i.imgur.com/MvDYE74.png" height="80%" width="80%" />
<br />
<br />
Configure on VTY lines: domain name, encryption, exec timeout, restriction to SSH only, and ACL permitting only PC1. Verify results with 'show run' and attempting to connect to SW2 from R2 and PC1.
SW2(config)#ip domain-name jonsitlab.com<br />
SW2(config)#crypto key generate rsa<br />
Enter: 2048<br />
SW2(config)#line vty 0 15<br />
SW2(config-line)#login local<br />
SW2(config-line)#exec-timeout 5 0<br />
SW2(config-line)#transport input ssh<br />
SW2(config-line)#exit<br />
SW2(config)#access-list 1 permit host 192.168.1.1<br />
SW2(config)#line vty 0 15<br />
SW2(config-line)#access-class 1 in<br />
SW2(config-line)#do show run<br />
<img src="https://i.imgur.com/KRaipTr.png" height="80%" width="80%" />
<img src="https://i.imgur.com/D1d9Iyd.png" height="80%" width="80%" />
<img src="https://i.imgur.com/8WlADi9.png" height="80%" width="80%" />
<img src="https://i.imgur.com/PljsHpX.png" height="80%" width="80%" />
