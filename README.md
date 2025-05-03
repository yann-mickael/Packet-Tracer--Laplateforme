# Packet-Tracer-Laplateforme

#Configuration Routeur

SWITCH

# Renommer switchs
Conf t
Hostname SWITCH1

----
# DESACTIVER LES PORTS INUTILES
Conf t
Int range fa0/10 -24
Shutdown
Exit
End
Wr

-------
# METTRE MOT DE PASS sur Switch
En
Conf t
Line console 0
Password Laplateforme,1,2,3 ( Switchs)
Login
Exit

---
ROUTEUR MOT DE PASS
En
Conf t
Line 0
Enable secret Laplateforme
Exit
Wr

---



-----------
# SWITCH  1, 2 et 3 / CREATION DES VLANS

Enable
Conf t

Vlan 1
Name VoIP
Exit

Vlan 10
Name PT_WIFI
Exit

Vlan 20
Name PC_FIXES
Exit

vlan 30
Name ADMIN
Exit

-------------------------------------------------------------
Int range fa0/2 -3
Switchport mode access
Switchport access vlan 1
Exit

Int range fa0/4 -5
Switchport mode access
Switchport access vlan 10
Exit

Interface range fa0/6 -7
Switchport mode access
Switchport access vlan 20
Exit

Int fa0/8
Switchport mode access
Switchport access vlan 30
Exit

Interface range fa0/1, fa0/9
Switchport mode trunk
Exit
End
Wr

---

# Modification Configuration Ip Phone 7960
Int fa0/2
Switchport mode access
Switchport access vlan 1
Spanning-tree portfastD
Description VoIP_Telephone_1
Exit

Int fa0/3
Switchport mode access
Switchport access vlan 1
Spanning-tree portfast
Description VoIP_Telephone_2
Exit

---------------
# ROUTEUR - Avtivation du routage
# initialisation Routeur 1941
En
Conf t
Ip routing
Int gig0/0
No shut
Exit

-----------
# ROUTEUR 1941 ( Configuration des VLANS)
En
Conf t
Int g0/0.1
Encapsulation dot1Q 1 native
Ip address 192.168.0.1 255.255.255.0
Exit

Int g0/0.10
Encapsulation dot1Q 10
Ip address 192.168.10.1 255.255.255.0
Exit

Int g0/0.20
Encapsulation dot1Q 20
Ip address 192.168.20.1 255.255.255.0
Exit

Int g0/0.30
Encapsulation dot1Q 30
Ip address 192.168.30.1 255.255.255.0
Exit

------------
# CONFIGURATION DHCP - ROUTEUR 1941
En
Conf t

Int gig0/0
No shut
Exit

Ip dhcp excluded-address 192.168.0.1 192.168.0.9
Ip dhcp pool vlan1
Network 192.168.0.0 255.255.255.0
Default-router 192.168.0.1
Dns-server 8.8.8.8

Ip dhcp excluded-address 192.168.10.1 192.168.10.9
Ip dhcp pool vlan10
Network 192.168.10.0 255.255.255.0
Default-router 192.168.10.1
Dns-server 8.8.8.8

Ip dhcp excluded-address 192.168.20.1 192.168.20.9
Ip dhcp pool vlan20
etwork 192.168.20.0 255.255.255.0
default-router 192.168.20.1
Dns-server 8.8.8.8

Ip dhcp excluded-address 192.168.30.1 192.168.30.9
Ip dhcp pool vlan30
Network 192.168.30.0 255.255.255.0
Default-routeur 192.168.30.1
Dns-server 8.8.8.8
Exit
End
Wr

---------------
MDP routeur, Laplateforme
MDP switch, Laplateforme, Laplateforme1, Laplteforme2

