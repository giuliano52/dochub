---
Titolo: X
---

#Login Manager

##LXDM

    systemctl enable lxdm
    
    
##LightDM
le configurazioni sono in: _/etc/lightdm/lightdm.conf_ 
e si sceglie il greeater con: 

    greeter-session=lightdm-gtk-greeter

per testartlo (ma non mi ha funzionato) 

    lightdm --test-mode --debug

abilitazione lightdm

    systemctl enable lightdm

##SDDM
la configurazione si può generare con il comando 

    sddm --example-config  > /etc/sddm.conf
    
poi le altre impostazioni sono nei file dei temi (di default /usr/share/sddm/themes) 
le facce si devono mettere in /usr/share/sddm/faces 

per provare i vari temi usare il comando:

    sddm-greeter --test-mode --theme /usr/share/sddm/themes/elarun/

#XDG
per ripristinare il default file manager usare il seguente comando:

    xdg-mime default Thunar.desktop inode/directory

#Accesso remoto
##x2go
sul client: intallare _x2goclient_

sul server installare x2goserver e lanciare il comando:

    sudo x2godbadmin --createdb
