# TP - Private Key Infrastructure (PKI)

# Partie 1 : Chiffrement symétrique avec OpenSSL
#### \[Exercice 1.1\]
#### \[Exercice 1.2\]
1. Chiffrer le fichier fichier1.txt avec un algorithme symétrique et le déchiffrer. Comparer le fichier déchiffré avec le chiffré.
2. Visualiser le fichier en clair et le fichier chiffré avec la commande ***cat***.
```bash
openssl enc --aes-128-cbc -in fichier1.txt -out fichier1.dechiffre
```
3. Comparer les tailles des fichiers clair et chiffré. Y a-t-il une différence ? Donner une explication.

#### \[Exercice 1.3\]
1. Le mot de passe est codé en base64 ("c2VjcmV0"). A l'aide de la commande openssl, décoder le mot de passe.
2. Déchiffrer le fichier cryptogamics
#### \[Exercice 1.4\]
1. Chiffrer le fichier fichier2.txt avec l'algorithme AES en mode CBC, en utilisant le vectuer d'initialisation et la clé de votre choix.
2. CHiffrer un fichier de votre choix, l'envoyer à l'un de vos camarades en lui précisant l'algorithme de chiffrement, le mode opératoire, la clé et le vecteur d'initialisation. Le récepteur doit déchiffrer le fichier pour voir le clair.

# Partie 2 : RSA et Certificats avec OpenSSL

#### \[Exercice 2.1\]
Menu Firefox => Options => Vie privée et sécurité => Afficher les certificats
Parcourir les certificats installés sur la machine puis en examiner un en repérant les informations ; notamment :
* taille clé RSA
* clé publique e
* modulo n 
* dates de validité
* identification de l'organisme
#### \[Exercice 2.2\]
1. Rechercher le programme de certification de Mozilla (https://wiki.mozilla.org/CA) et trouver la liste des certificats CA.
2. Evaluer les différents algorithmes à clé publique utilisés
3. Existe-t-il un certificat racine CA non conforme aux recommandations de l'ANSSI pour les algorithmes à clé publique ?
4. Expliquer pourquoi cela peut arriver
#### \[Exercice 2.3\]
Générer puis visualiser deux paires de clé RSA. Remarquer que la valeur de la clé publique est toujours e=65537. Comment expliquer cela ?
#### \[Exercice 2.4\]
1. Avec la commande cat observer le contenu de l'un des deux fichiers générés (exercice précédent) puis le chiffrer avec AES. Utiliser à nouveau la commande rsa pour visualiser le contenu du fichier.
2. Quelles sont les différences ?
3. Que signifie chaque partie du DEK-info ?
#### \[Exercice 2.5\]
1. Exporter les parties publiques des clés RSA générées
2. Utiliser la commande rsa et visualiser les clés publiques. Vous devez préciser l'option -pubin puisque seule la partie publique figure dans le fichier ClersaPublique.pem.
#### \[Exercice 2.6\]
1. Utiliser le générateur de nombre pseudo-aléatoire d'Openssl avec la commande ***rand*** pour construire une clé de session de 256 bits. Utiliser -base64 ou -hex.
2. CHiffrer la clé de session avec la clé publique du destinataire (vous pouvez aussi utiliser les deux clés générées dans l'exercice 3.2 pour faire les deux rôles expéditeur et destinataire ou demandez la clé publique de l'un de vos camarades). Le destinataire réceptionne le mesage et le déchiffre avec sa clé privée pour découvrir la clé de session.
#### \[Exercice 2.7\]
1. Créer un fichier avec un texte quelconque, générer son empreinte (fonction de hashage recommandée par l'ANSSI) puis modifier un octet et regénérer l'empreinte. Observer les deux empreintes. 
2. Générer le MAC du fichier créé avec une clé au choix. Modifier un caractère dans la clé choisie et regénérer le MAC pour observer l'effet avalanche.
3. Le fichier nomme *signature* est peut-être la signature du fichier nommé *clair* avec la clé publique maClePub.pub. Comment procéder pour vérifier l'authentification avec dgst ?
4. Essayer avec rsautl et le hash. La signature correspond-elle à celle du fichier en clair ? Quelle est la différence ? (utiliser la sortie hexadécimale - pour obtenir la valeur d'un fichier binaire : cat | od -A n -t xl)
#### \[Exercice 2.8\]
Générer une paire de clés RSA d'une taille de 4096 bits nommée *rsakey.pem* et exporter la partie publique dans un fichier *rsakey.pub*.

#### \[Exercice 2.10\]
Créer un certificat signé pour la clé pkey.pem.
* créer une clé pour l'AC à l'aide d'une des courbes du Logarithme discret sur courbes elliptiques (EC-DLOG) recommandée par l'ANSSI. Enquêter sur "openssl ecparam" et "openssl ec"
* créer un certificat racine et l'auto signer
* générer un certificat avec le CSR et la clé. Le signer avec la clé racine de la CA.
