** Networkconfiguration **

$path = /etc/netplan



apply
--------------------------------
sudo netplan apply
sudo netplan --debug apply
--------------------------------


DHCP
------------------------
** freigeben der IP
dhclient -r

** neue anfordern
dhclient
------------------------




Configs
-----------------------------------------------------------------------------------------------

-----------------------------------------------------------------------------
# This file is generated from information provided by
# the datasource.  Changes to it will not persist across an instance.
# To disable cloud-init's network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    ethernets:
        enp0s3:
            addresses: [192.168.1.2/24]
            gateway4: 192.168.1.1
            nameservers:
              addresses: [8.8.8.8,8.8.4.4]
            dhcp4: no
    version: 2
-----------------------------------------------------------------------------


DHCP
-----------------------------------------------------------------------------
# This file is generated from information provided by
# the datasource.  Changes to it will not persist across an instance.
# To disable cloud-init's network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    ethernets:
        ens38:
            addresses: []
            dhcp4: true
    version: 2
-----------------------------------------------------------------------------

end
-----------------------------------------------------------------------------------------------



Users
------------------------------------------------------------------------------------------

assistent
-----------------
adduser "name"
-----------------


manuell
-----------------------------------------------
useradd "name" -d /home/name -m -s /bin/false
>> useradd fritz -c "Test User Fritz" -d /home/fritz/ -m -s /bin/bash/
-----------------------------------------------


change parameter
----------------------------
usermod -s /bin/false max
----------------------------


deluser
------------------------------------------------
deluser "name" --remove-home --remove-all-files
------------------------------------------------


primär group
-----------------------------------------
sudo usermod -g GRUPPENNAME BENUTZERNAME 
-----------------------------------------


sekundär group
-----------------------------------------
sudo usermod -aG GRUPPENNAME BENUTZERNAME 
-----------------------------------------

end
------------------------------------------------------------------------------------------




SFTP Server
------------------------------------------------------------------------------------------

1. set root PW
-------------------
sudo su
passwd
-------------------

2. install sudo
---------------------
apt-get install sudo
---------------------

3. change DIR
---------------------
cd /etc/sudoers.d
---------------------

4. change user to root
------------------------
sudo su
------------------------

5. creat file
-------------------------
visudo -f nopwsftp

>> deinbenutzer ALL=NOPASSWD: /usr/lib/openssh/sftp-server
-------------------------


6. rechte anpassen
--------------------------
chmod o-r nopwsftp
chmod ugo-w nopwsftp
--------------------------


7. winSCP ADVANCT settings
-------------------------------------------------------------
>> sudo /usr/lib/openssh/sftp-server
-------------------------------------------------------------

end
------------------------------------------------------------------------------------------



SUDO
------------------------------------------------------------------------------------------


1. Fügen Sie den neu erstellten Benutzer [max] der Gruppe [sudo] hinzu
-----------------------------------------------------------------------
usermod max -G sudo
-----------------------------------------------------------------------

2. Prüfen Sie, ob der neu erstellte Benutzer [max] in der Gruppe [sudo] Mitglied ist
-----------------------------------------------------------------------
less /etc/group | grep sudo
-----------------------------------------------------------------------

3. Fügen Sie den zweiten neuen Benutzer [fritz] der [sudoers] Datei manuell hinzu.
-----------------------------------------------------------------------
visudo
>> fritz ALL=PASSWD: ALL
-----------------------------------------------------------------------

4. Testen Sie, ob der neu erstellte Benutzer [fritz] den Befehl [sudo] verwenden kann
-----------------------------------------------------------------------
su fritz
-----------------------------------------------------------------------

5.Starten Sie WinSCP und stellen Sie mit [max] eine Verbindung zum Linux Server her
-----------------------------------------------------------------------
