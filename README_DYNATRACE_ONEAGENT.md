# Formatin Dynatrace
# Connexion de OneAgent Dynatrace (Linux / WSL)

Ce guide explique comment connecter une machine Linux (ou WSL) à Dynatrace avec OneAgent.

## 1) Prérequis

- Un tenant Dynatrace actif (ex: `https://gak65816.live.dynatrace.com`)
- Un token Dynatrace valide (ne jamais le partager)
- `curl` ou `wget`
- Droits `sudo`

## 2) Télécharger l'installateur OneAgent

Utiliser un token via variable d'environnement (plus sûr que le coller en clair dans l'historique).

```bash
read -s DT_API_TOKEN
curl -sS -L -w "HTTP:%{http_code}\n" \
  -o Dynatrace-OneAgent-Linux.sh \
  "https://gak65816.live.dynatrace.com/api/v1/deployment/installer/agent/unix/default/latest?arch=x86&flavor=default" \
  -H "Authorization: Api-Token ${DT_API_TOKEN}"
```

Alternative avec `wget`:

```bash
wget -O Dynatrace-OneAgent-Linux.sh \
  "https://gak65816.live.dynatrace.com/api/v1/deployment/installer/agent/unix/default/latest?arch=x86&flavor=default" \
  --header="Authorization: Api-Token ${DT_API_TOKEN}"
```

## 3) Vérifier que le fichier est valide

```bash
ls -lh Dynatrace-OneAgent-Linux.sh
file Dynatrace-OneAgent-Linux.sh
```

Attendu:
- taille en **MB** (pas quelques octets/Ko)
- type `POSIX shell script`

Si vous voyez `HTTP:401` ou un fichier très petit, le token est invalide ou incorrect.

## 4) Vérifier la signature (recommandé)

```bash
wget https://ca.dynatrace.com/dt-root.cert.pem

(
  echo 'Content-Type: multipart/signed; protocol="application/x-pkcs7-signature"; micalg="sha-256"; boundary="--SIGNED-INSTALLER"'
  echo
  echo
  echo '----SIGNED-INSTALLER'
  cat Dynatrace-OneAgent-Linux.sh
) | openssl cms -verify -CAfile dt-root.cert.pem > /dev/null
```

Résultat attendu:
- `CMS Verification successful`

## 5) Installer OneAgent

```bash
sudo /bin/sh Dynatrace-OneAgent-Linux.sh \
  --set-monitoring-mode=fullstack \
  --set-app-log-content-access=true
```

## 6) Vérifier l'installation

```bash
echo $?
sudo /opt/dynatrace/oneagent/agent/tools/oneagentctl --get-host-id
```

Attendu:
- code retour `0`
- un `host-id` (ex: `ECFAAC199ABD27DC`)

Vérifier ensuite dans Dynatrace:
- `Infrastructure` -> `Hosts`
- la machine doit apparaître en état actif

## 7) Test API local (exemple)

Sous PowerShell, utiliser `curl.exe` (pas `curl` alias).

```powershell
curl.exe -i "http://127.0.0.1:8000/api/blog_view_public?lang=fr"
```

## 8) Dépannage rapide

### Erreur: `cannot open Dynatrace-OneAgent-Linux.sh`
- le fichier n'est pas dans le dossier courant
- vérifier avec `ls -lh`

### Erreur: `HTTP:401` / `Token Authentication failed`
- token invalide, expiré, révoqué, ou mauvais tenant
- recréer un token et retester

### Fichier téléchargé très petit (0, 62, 67 octets)
- ce n'est pas l'installateur, c'est un JSON d'erreur API

### `Unit oneagent.service could not be found`
- souvent script vide/invalide exécuté
- retélécharger correctement puis réinstaller

## 9) Sécurité

- Ne jamais coller un token Dynatrace dans un chat ou un dépôt Git
- Révoquer immédiatement tout token exposé
- Créer un nouveau token avec permissions minimales nécessaires

# Formatin Dynatrace et Kubernetes

