---
title: Comandi Utili
author: Giuliano Dedda 
date: 16/12/2014
---

#Operazioni su files

*sed* può avere problemi con l'escape dei caratteri (specialmente il \\) per eliminare questi problemi 
fare un file esterno con i comandi sed per ogni linea (ed eventualmente con #) e lanciarlo con

    sed -i -f nomefile.sed

Comando                                               	| Effetto
--------------------------------------------------------| --------------------------------------------------------
sed -i 's/orig/dst/' file.txt 			                | Sostituisce il testo orig con dst nel file.txt
sed 's/[^[:print:]]/#/g' input.log > output.txt 		| Rimuove tutti i caratteri non stampabili 
sed -i  "s/<\(.\)>/(\1)/g"  filename                    | sostituisce le parentesi (lasciando il contenuto)
sed -i "s/\xE2\x80\x93/-/g" filename                    | sostiuisce stringhe unicode
sort in.txt > output.txt                       			| Ordina un file di testo
cat file1.txt file2.txt file\*.txt > output.txt  		| unire più files di testo in uno solo
rsync -avh --progress Sorgente  Dir_Destinazione        | Copia un file o directory mostrando  la una progress bar
diff -e file.old file.new > diff1.txt                   | salva il diff di due file in formato ed 
(cat diff1.txt diff2.txt ... && echo w) | ed - file.old | usa il file diff.txt per modificare il file.old (verificare)


Per trovare i duplicati e ordinarli per dimensione:

    fdupes -R -S ./ > dup.txt
    awk '$1=""$1' RS='' FS='\n' OFS='\034' dup.txt |  sort -n |  awk '$1=""$1' FS='\034' OFS='\n' ORS='\n\n' > dup.sort.txt


# Filesystem

Comando                                               	| Effetto
--------------------------------------------------------| --------------------------------------------------------
grep parola *									  		| Cerca una parola all'interno dei file -i (case insensitive) -v (escludi parola)
lndir /dir/sorgente /dir/destinazione			  		| crea una copia di link di una directory (usare i nomi delle directory completi)
lsof											  		| mostra i files aperti
parted											  		| serve per ridimensionare le partizioni
mmls												  	| Gestisce i dischi creati con dd
fdupes -r ./										  	| Trova i files duplicati in una directory
tune2fs -m 0 /dev/sdb1                                  | mette a 0% lo spazio riservato a root
e2label /dev/sdd1 ETICHETTA                             | imposta l'etichetta per una partizione
file -Ls /dev/sdb1                                      | informazioni sul filesystem (tipo , uuid ..)

# Stato sistema
Comando                             | Effetto
------------------------------------| ------------------------------------
free								| Informazioni sulla memoria (La memoria utilizzata è il primo numero della riga: -/+ buffers/cache: )
lshw <br> lshw -html 				| Mostra l'hardware presente sulla macchina (eventualmente in formato html)
lsusb								| Mostra le periferiche usb (i dischi vengono visti come dischi scsi)
uptime								| Mostra le informazioni di uptime, numero di utenti e carico
id									| Mostra gli id dell’utente
lsblk								| Mostra i dischi e le partizioni


#Networking
Comando                             | Effetto
------------------------------------| ------------------------------------
tracepath IP                        | come traceroute
sudo netstat -plnt                  | vede le porte aperte con relativo processo
lsof -Pan -i tcp -i udp             | come sopra ma usa lsof

#Utenti e gruppi
Comando                             | Effetto
------------------------------------| ------------------------------------
useradd -m -G sudo -s /bin/bash pino    | Crea l'utente _pino_ con la home (-m) e con il gruppo aggiuntivo 'sudo'
usermod -aG sudo pino                   | Aggiunge il gruppo sudo all'utente _pino_
groupadd -g 2000 nomeGruppo         | aggiunge il gruppo con id 2000

#Comando Find

Esegue una funzione dopo il find   (il comando execdir esegue il comando all'interno della directory del file)

    find ./ -name '*.pdf' -exec ls -la {} \;     
    find ./ -name '*.c' -exec grep ciao {} \;
    find ./ -name '*.pdf' -exec rm -f {} \;
    find ./ -name *.rar -execdir unrar e  {} \;     # estrae tutti i rar nei subfolder
    

copia una directory completamente in un altra   

    find . -depth -print0 | cpio --null --sparse --preserve-modification-time -pvd /mnt/newhome/
    find /SouceDir -xdev | cpio -pm /DestDir`  

Trova le directory vuote   

    find . -type d -empty

Trova e cancella le directory vuote   

    find . -type d -empty -exec rmdir {} \;
    
#Sicurezza

Comando                             | Effetto
------------------------------------| ------------------------------------
last -i     				        | mostra il last con l'IP al posto del nome
lastlog                             | mostre l'utlimo login degli utetni su un sistema

#Altri Comandi

Comando                             | Effetto
------------------------------------| ------------------------------------
seq --format='%f' 3 11				| scrive i numeri da 3 a 11 utilizzando il formato printf (in questo caso floating)
seq --format="%02g" 5 2 41          | scrive i numeri da 5 a 41 con passo due utilizzando 2 cifre (05 07 09 11 ..)
DATE=\`date +%Y-%m-%d\`             | La variabile DATA ha la data in formato YYYY-mm-DD
DATE=\`date +%Y-%m-%d:%H:%M:%S\`    | come sopra con l'ora
time comando                        | valuta il tempo di esecuzione di un comando
