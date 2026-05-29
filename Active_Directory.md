# Documentation de déploiement d'une fôret AD

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

### Network:

    > IP: 192.168.10.248
    > Masque de sous-réseau: 255.255.255.0
    > Passerelle: 192.168.10.1
    > DNS préféré: 127.0.0.1 (AD1 sera le serveur DNS de la fôret en tant que DC)
    > DNS Alternatif: 192.168.10.1 (accès à internet)

## Configuration de AD2

### Network:

    > IP: 192.168.10.247
    > Masque de sous-réseau: 255.255.255.0
    > Passerelle: 192.168.10.1
    > DNS préféré: 192.168.10.248
    > DNS Alternatif: 127.0.0.1
