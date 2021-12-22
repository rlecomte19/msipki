# TP - Private Key Infrastructure (PKI)

# Partie 1 : Chiffrement symétrique avec OpenSSL
#### \[Exercice 1.1\]
En tapant la commande :
```bash
openssl help
```
On obtient bien les différents algorithmes (enc) et fonctions de hashage (dgst) proposées.
> enc :

![enc](https://user-images.githubusercontent.com/72377954/146832519-f700bb36-79fc-4633-8836-5016b63a5498.png)

> dgst :

![dgt](https://user-images.githubusercontent.com/72377954/146832544-28f10976-b053-4004-95f0-0aad1fcc7af7.png)

#### \[Exercice 1.2\]
```bash
openssl enc --aes-128-cbc -in fichier1.txt -out fichier.chiffre
```
Déchiffrement de fichier.chiffre
```bash
openssl enc -d --aes-128-cbc -in fichier.chiffre -out fichier.dechiffre
```
Cotnenu de ces fichiers via la commande cat : 
> Fichier clair

![fichier1txt](https://user-images.githubusercontent.com/72377954/146831881-d7575963-ddc8-44a2-88fb-ceab4bed711a.png)

> Fichier chiffré

![fichier1chiffre](https://user-images.githubusercontent.com/72377954/146832026-92dfd5f1-c39c-447e-816d-8abd6427f57d.png)

> Fichier dechiffré

![fichier1dechiffre](https://user-images.githubusercontent.com/72377954/146832084-d338c0b1-9bd5-4c53-92d3-2ef02a2cfcf9.png)


3. Comparer les tailles des fichiers clair et chiffré. Y a-t-il une différence ? Donner une explication.
Grâce à la commande ***stat*** j'ai affiché le nombre d'octets. On voit ainsi que les deux fichiers font la même taille. Il parâit logique que ce soit le cas. En effet, on chiffre par bloc mémoire. Ainsi, il y aura autant de bits à l'arrivée qu'au départ.

![sizeoffichier1](https://user-images.githubusercontent.com/72377954/146832361-e2211bc8-ded4-4883-8d71-c8a6decfd2af.png)

#### \[Exercice 1.3\]
1. Le mot de passe est codé en base64 ("c2VjcmV0"). A l'aide de la commande openssl, décoder le mot de passe.
On peut utiliser la commande : 
```bash
openssl enc -base64 -d <<< c2VjcmV0
```
Cette dernière décodera le mot de passe. Le mot de passe déchiffré est ***secret***.

On peut déchiffrer le fichier cryptogamics avec une commande similaire à celle de la question 1.2 :
```bash 
openssl enc -d --aes-256-cbc -in cryptogramics -out cryptogramics.dechiffre
```
Cela nous donnera donc un déchiffrement du fichier cryptogamics. On obtient ainsi la phrase :
> Passer au point suivant chiffrement avec clé
#### \[Exercice 1.4\]
1. Voici la commande utilisée pour un chiffrement AES en CBC par blocs de 128 bits avec une clé et un vecteur d'initialisation (32 & 32) : 
```bash
openssl enc --aes-128-cbc -in fichier2.txt -out fichier2.chiffre -iv 730AEC20000000001420322325255220 -K 54F5A125000000000000000000000005
```

2. J'ai commencé par chiffrer le fichier ***'fichier2.txt'*** avec le même algorithme de chiffrement que le précédent :
```bash
openssl enc -des-cbc -in serverConfig.cnf -out encServCfg -iv 0123456789ABCDEF -K 0123456789ABCDEF
```
Mon camarade l'a donc décodé avec la commande : 
```bash
openssl enc -d -des-cbc -in endcServCfg -out serverConfig.cnf -iv 0123456789ABCDEF -K 0123456789ABCDEF
```

# Partie 2 : RSA et Certificats avec OpenSSL
#### \[Exercice 2.1\]
Pour cette question j'ai choisi le certificat : certSIGN Root CA G2. On y retrouve les informations suivantes :

* taille clé RSA : 4096 
* clé publique e : 

C0:C5:75:19:91:7D:44:74:74:87:FE:0E:3B:96:DC:D8:01:16:CC:EE:63:91:E7:0B:6F:CE:3B:0A:69:1A:7C:C2:E3:AF:82:8E:86:D7:5E:8F:57:EB:D3:21:59:FD:39:37:42:30:BE:50:EA:B6:0F:A9:88:D8:2E:2D:69:21:E7:D1:37:18:4E:7D:91:D5:16:5F:6B:5B:00:C2:39:43:0D:36:85:52:B9:53:65:0F:1D:42:E5:8F:CF:05:D3:EE:DC:0C:1A:D9:B8:8B:78:22:67:E4:69:B0:68:C5:3C:E4:6C:5A:46:E7:CD:C7:FA:EF:C4:EC:4B:BD:6A:A4:AC:FD:CC:28:51:EF:92:B4:29:AB:AB:35:9A:4C:E4:C4:08:C6:26:CC:F8:69:9F:E4:9C:F0:29:D3:5C:F9:C6:16:25:9E:23:C3:20:C1:3D:0F:3F:38:40:B0:FE:82:44:38:AA:5A:1A:8A:6B:63:58:38:B4:15:D3:B6:11:69:7B:1E:54:EE:8C:1A:22:AC:72:97:3F:23:59:9B:C9:22:84:C1:07:4F:CC:7F:E2:57:CA:12:70:BB:A6:65:F3:69:75:63:BD:95:FB:1B:97:CD:E4:A8:AF:F6:D1:4E:A8:D9:8A:71:24:CD:36:3D:BC:96:C4:F1:6C:A9:AE:E5:CF:0D:6E:28:0D:B0:0E:B5:CA:51:7B:78:14:C3:20:2F:7F:FB:14:55:E1:11:99:FD:D5:0A:A1:9E:02:E3:62:5F:EB:35:4B:2C:B8:72:E8:3E:3D:4F:AC:2C:BB:2E:86:E2:A3:76:8F:E5:93:2A:CF:A5:AB:C8:5C:8D:4B:06:FF:12:46:AC:78:CB:14:07:35:E0:A9:DF:8B:E9:AF:15:4F:16:89:5B:BD:F6:8D:C6:59:AE:88:85:0E:C1:89:EB:1F:67:C5:45:8E:FF:6D:37:36:2B:78:66:83:91:51:2B:3D:FF:51:77:76:62:A1:EC:67:3E:3E:81:83:E0:56:A9:50:1F:1F:7A:99:AB:63:BF:84:17:77:F1:0D:3B:DF:F7:9C:61:B3:35:98:8A:3A:B2:EC:3C:1A:37:3F:7E:8F:92:CF:D9:12:14:64:DA:10:02:15:41:FF:4F:C4:EB:1C:A3:C9:FA:99:F7:46:E9:E1:18:D9:B1:B8:32:2D:CB:14:0C:50:D8:83:65:83:EE:B9:5C:CF:CB:05:5A:4C:FA:19:97:6B:D6:5D:13:D3:C2:5C:54:BC:32:73:A0:78:F5:F1:6D:1E:CB:9F:A5:A6:9F:22:DC:D1:51:9E:82:79:64:60:29:13:3E:A3:FD:4F:72:6A:AB:E2:D4:E5:B8:24:55:2C:44:4B:8A:88:44:9C:CA:84:D3:2A:3B
* dates de validité : 06/02/2017 - 06/02/2042
* identification de l'organisme : CERTSIGN SA

#### \[Exercice 2.2\]
1. La liste des certificats des CA pour mozilla se trouve sur le site web
> https://ccadb-public.secure.force.com/mozilla/PublicAllIntermediateCerts

2. Les algorithmes utilisés sont majoritairement RSA avec une clé comprise entre 2048 et 4096 bits. 
3. Les certificats créés avec des algorithmes RSA avec une clé de 2048 bits précédemment évoqués sont dépréciés depuis 2017 mais encore très utilisés. Cela provoque donc une perte de sécurité.
4. Tous les sites ne manipulent pas des données spécifiquement sensibles ou personnelles. Les transferts ne doivent ainsi pas forcément être plus sécurisés. Par ailleurs, les coûts de changement, les temps de nouvelle acceptation de la CA racine ainsi que les temps de calcul pour des petits sites / organisations qui ne manipulent pas des données sensibles ne valent pas cette mise à jour.

#### \[Exercice 2.3\]
Afin de générer les deux paires de clé on utilise : 
```c
openssl genrsa -out Clersa.pem 4096
openssl genrsa -out Clersa2.pem 4096
```
Afin de visualiser ces dernières on utilise : 
```c
openssl rsa -in Clersa.pem -text -noout
openssl rsa -in Clersa2.pem -text -noout
```
Le nombre 65537 est le plus grand premier connu sous la forme (2^2^n + 1). Il est utilisé en RSA car ce chiffrement nécessite un nombre premier (3 marcherait aussi). Ici, du fait de sa taille, il est le plus apprécié par ce type d'algorithmes. On parle d'exposant de clé.

cf : https://www.quora.com/Why-is-e-65537-used-for-most-RSA-encryption

cf : https://en.wikipedia.org/wiki/65,537

#### \[Exercice 2.4\]
1. On visualise la première paire de clé générée avec ***cat*** :
```bash
cat ./Clersa.pem
```

![rsacle](https://user-images.githubusercontent.com/72377954/146982727-8e51f866-fd48-4551-9cfc-7d41c7714f78.png)

On chiffre ensuite cette paire avec AES 128 bits en mode CBC : 
```bash
openssl enc --aes-128-cbc -in Clersa.pem -out Clersa.chiffre
```

On visualise ensuite ce fichier chiffré avec RSA : 
```bash
openssl rsa -in Clersa.chiffre -text -noout
```

2. La différence principale entre AES et RSA est la rapidité de calcul. En effet, RSA est bien plus gourmand que AES.

cf : https://www.appvizer.fr/magazine/services-informatiques/protection-donnees/cryptage-aes

3. Le DEK INFO (à savoir l'entête de la paire de clés) contient : 
- le mode de chiffrement
- le nombre de bits utilisé
- le mode de fonctionnement (cbc...)
- le vecteur d'initialisation
- d'autres données intéressantes....

#### \[Exercice 2.5\]
1. L'export de la partie publique des RSA se fait grâce à l'option ***-pubout*** : 
```bash
openssl rsa -in Clersa.pem -pubout -out Clersa.pub
openssl rsa -in Clersa2.pem -pubout -out Clersa2.pub
```
2. On visualise désormais clé publique grâce à l'option ***-pubin*** :
```
openssl rsa -pubin -in Clersa.pem -text -noout
openssl rsa -pubin -in Clersa2.pem -text -noout
```
On obtient :

> Première clé

![clersapublique](https://user-images.githubusercontent.com/72377954/147122095-cadd3281-4737-43cb-b281-162e2109a068.png)

> Seconde clé

![clersa2publique](https://user-images.githubusercontent.com/72377954/147122084-f2e2a8f7-87aa-4de8-ab20-fdccd8306cea.png)

#### \[Exercice 2.6\]
1. J'ai utilisé la commandez ***openssl rand*** afin de créer cette clé de session :
```bash
openssl rand -hex 256 > session_key.pem
```

![sessionkey](https://user-images.githubusercontent.com/72377954/147123124-7c381e2e-9e38-4e1e-9d0c-e6158e2fa018.png)

4. On chiffre cette clé avec la clé publique ***Clersa.pub*** créée précédemment : 
```bash
openssl enc -aes-256-cbc -salt -in session_key.pem -out session_key.enc -pass file:./Clersa.pub
```

#### \[Exercice 2.7\]
1. J'ai premièrement créé un fichier en le remplissant avec ***vim*** : 
```bash
vim fichierquelconque
```
![fichierquelconque](https://user-images.githubusercontent.com/72377954/147126568-d76b7c5c-3cae-403f-90ea-98ab4ba9f254.png)

J'ai par la suite recherché les algorithmes de hashage recommandés par l'ANSSI : 

> https://www.ssi.gouv.fr/uploads/2021/03/anssi-guide-selection_crypto-1.0.pdf

J'ai ainsi opté pour l'agorithme SHA-3 : 
![anssirec](https://user-images.githubusercontent.com/72377954/147126403-24ee5815-26ae-41d5-8590-083e5cd08b6b.png)

On obtient donc le calcul de l'empreinte par : 
```bash
openssl dgst -SHA256 -out empreinte_quelconque fichierquelconque
```
On visualise désormais cette empreinte :

![empreinte](https://user-images.githubusercontent.com/72377954/147127088-408d3785-82c1-4320-a92f-b2a771d85c6e.png)

On enlève ensuite le *!* du fichier créé et on regénère l'emprunte. 
#### NOTA BENE : un caractère occupe 1 octet mémoire sur ma VM 

Les deux empreintes sont en effet différentes. 

![empreintemodifie](https://user-images.githubusercontent.com/72377954/147127559-b0414cdf-2a99-447a-89b6-5718c1429345.png)


3. Générer le MAC du fichier créé avec une clé au choix. Modifier un caractère dans la clé choisie et regénérer le MAC pour observer l'effet avalanche.
4. Le fichier nomme *signature* est peut-être la signature du fichier nommé *clair* avec la clé publique maClePub.pub. Comment procéder pour vérifier l'authentification avec dgst ?
5. Essayer avec rsautl et le hash. La signature correspond-elle à celle du fichier en clair ? Quelle est la différence ? (utiliser la sortie hexadécimale - pour obtenir la valeur d'un fichier binaire : cat | od -A n -t xl)
#### \[Exercice 2.8\]
Générer une paire de clés RSA d'une taille de 4096 bits nommée *rsakey.pem* et exporter la partie publique dans un fichier *rsakey.pub*.

#### \[Exercice 2.10\]
Créer un certificat signé pour la clé pkey.pem.
* créer une clé pour l'AC à l'aide d'une des courbes du Logarithme discret sur courbes elliptiques (EC-DLOG) recommandée par l'ANSSI. Enquêter sur "openssl ecparam" et "openssl ec"
* créer un certificat racine et l'auto signer
* générer un certificat avec le CSR et la clé. Le signer avec la clé racine de la CA.
