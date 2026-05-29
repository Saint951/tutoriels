# Documentation de déploiement d'une forêt AD

## Matériel (vm proxmox):

Server AD1:

    * 8GiB Ram
    * 50GB Disk
    * IP: 192.168.10.248

Server AD2:

    * 8GiB Ram
    * 50GB Disk
    * IP: 192.168.10.247

## Configuration de AD1

>[!TIP]
>Profitez du panneau de configuration pour le renommer de manière propre
> Ex: DC1

>[!warning]
>Mettez à jour vos serveurs! 
>Avec les temps qui courrent il faut sécuriser nos infrastructures même privées.

### Network:

    > IP: 192.168.10.248
    > Masque de sous-réseau: 255.255.255.0
    > Passerelle: 192.168.10.1
    > DNS préféré: 127.0.0.1 (AD1 sera le serveur DNS de la forêt en tant que DC)
    > DNS Alternatif: 192.168.10.1 (accès à internet)

### Logiciels

Dans le paneau de gestion du serveur:

    * Ajout de rôle et de fonctions,
    * Suivez l'installeur,
    * Sélectionnez votre serveur,
    * Cochez "Services de domaine Active Directory",
    * Acceptez, Suivant et installer,
    * Redemarrez si besoin

### Forêt

Dans Gestion de serveur:
    Cliquez sur le drapeau jaune qui est apparu:
        Promouvoir ce serveur en contrôleur de domaine:
            Configuration de Déploiement: 
                Ajouter une Nouvelle forêt:
                    Nom de domaine de la racine: evil.corp (Nom de domaine de votre entreprise, merci de vous réferer à vos demandes, si c'est pour un test mettez pas vos nom de domaines publiques)
            Options du contrôleur de domaine:
                S'assurer que Serveur DNS est bien coché
                Définissez votre mot de passe DSRM
            Skippez toutes les options

## Configuration de AD2

### Network:

    > IP: 192.168.10.247
    > Masque de sous-réseau: 255.255.255.0
    > Passerelle: 192.168.10.1
    > DNS préféré: 192.168.10.248
    > DNS Alternatif: 127.0.0.1

### Logiciels

Se réferer aux instructions AD1

### Forêt

Dans Gestion de Serveur:
    Cliquez sur le drapeau jaune qui est apparu:
        Promouvoir ce serveur en contrôleur de domaine:
            Configuration de Déploiement:
                Ajouter un contrôleur de domaine à un domaine existant:
                    Domaine: evil.corp
                    Fournir les informations d'identifications pour cette opération:
                        Nom d'utilisateur: Administrateur@evil.corp
                        Mot de passe: votre_password_admindc1
            Options du contrôleur de réseau:
                Verifier que DNS et Catalogue global soient bien cochés,
                Définissez votre mot de passe DSRM
            Skippez les autres options

## Mot de fin

Et bien voilà, c'est peu tout, c'est un active directory en haute disponibilité.
Vous pouvez faire beaucoup de choses avec grâce au LDAP.
