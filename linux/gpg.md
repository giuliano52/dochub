#GPG

##Encrypt e decrypt

   gpg --encrypt -o secret.tar.gpg secret.tar
   gpg --decrypt secret.tar.gpg


##Generare le chiavi

    gpg --gen-key
   (se per caso si blocca nella parte dove richiede abbastanza entropia lanciare il comando:)

    yaourt -S rng-tools
    sudo rngd -r /dev/urandom

##Gestione Chiavi
per vedere le chiavi nel proprio keyring

    gpg --list-keys
    gpg --list-secret-keys
    
per esportare la chiave pubblica

    gpg --export -a "User Name" > public.key

per esportare la chiave privata

    gpg --export-secret-key -a "User Name" > sec.key
   
le chiavi di pgp sono compatibili (usare -import)

    gpg -e nomefile per crittografare (usare come ID Nome Cognome)
		-s nomefileper firmare
    gpg nomefile per de-crittografare 
         --import --allow-secret-keys-import per importare le chiavi private
		 --list-keyper vedere le chiavi pubbliche
		 --list-secret-keysper vedere le chiavi private
		 --gen-keygenera le chiavi
		 --import nomefileimporta chiavi di altri

le chiavi sono in $HOME/.gpg/pubring.gpg e secring.gpg

         --clearsign nomefilefirma in ascii
		 --verify nomefileverifica un file
		 --edit-key nomechiavecambia la password
		 -a --export esporta la chiave pubblica in ascii