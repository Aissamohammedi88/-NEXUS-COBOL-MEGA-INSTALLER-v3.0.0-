# -NEXUS-COBOL-MEGA-INSTALLER-v3.0.0-
# NEXUS COBOL MEGA INSTALLER v3.0.0 # Installation + optimisation + compilation + benchmark + interface web # Linux Mint / Ubuntu / Debian - Bash pur # Auteur : Aissa Mohammedi (DGK) # Licence : NEXUS-OPEN-2.0
# NEXUS COBOL HEALTH CHECK & AUTO-INSTALLER

[![License: NEXUS-OPEN-2.0](https://img.shields.io/badge/License-NEXUS--OPEN--2.0-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-brightgreen.svg)]()
[![Bash](https://img.shields.io/badge/bash-4.0%2B-green.svg)]()
[![GnuCOBOL](https://img.shields.io/badge/gnucobol-3.x-orange.svg)]()
[![Platform](https://img.shields.io/badge/platform-linux%20%7C%20macos-lightgrey.svg)]()

> Scan complet d'une installation COBOL, détection des dépendances manquantes, installation automatique, tests fonctionnels et rapport diagnostique.

**Auteur :** Aissa Mohammedi (DGK)
**Licence :** NEXUS-OPEN-2.0
**Version :** 1.0.0

---

## Aperçu

`nexus_cobol_health_check.sh` est un script Bash qui :

1. **Scanne** l'installation système à la recherche des outils COBOL et leurs dépendances
2. **Teste** réellement le compilateur `cobc` avec 4 programmes COBOL fonctionnels
3. **Détecte** ce qui manque, ce qui est cassé, ce qui fonctionne
4. **Installe** automatiquement ce qui manque (via `apt`, `dnf`, `pacman`)
5. **Génère** un rapport diagnostique clair avec statut global

Utilisé par les équipes qui déploient des environnements COBOL en production, formation ou CI/CD.

---

## Table des matières

- [Aperçu](#aperçu)
- [Installation](#installation)
- [Utilisation](#utilisation)
- [Options](#options)
- [Ce que le script vérifie](#ce-que-le-script-vérifie)
- [Tests fonctionnels](#tests-fonctionnels)
- [Compatibilité](#compatibilité)
- [Contribuer](#contribuer)
- [Licence](#licence)
- [Tags](#tags)

---

## Installation

### Méthode 1 — Téléchargement direct

```bash
curl -fsSL https://raw.githubusercontent.com/Aissamohammedi88/nexus-cobol-health-check/main/nexus_cobol_health_check.sh -o nexus_cobol_health_check.sh
chmod +x nexus_cobol_health_check.sh
./nexus_cobol_health_check.sh



Option Description
--fix Répare automatiquement ce qui manque (paquets + dossiers)
--install Installe tout ce qui manque sans demander (comme --fix + auto)
--verbose / -v Affiche les versions et détails
--help / -h Affiche l'aide
(aucune) Mode diagnostic en lecture seule




Ce que le script vérifie

1. Outils système

· bash, sh, awk, sed, grep, find, tar, gzip, file

2. Compilateur COBOL

· Présence de cobc (GnuCOBOL)
· Version
· Test réel : compilation + exécution d'un programme DISPLAY "TEST OK"

3. Outils de compilation

· gcc, g++, make, ld, strip, ar, ldd

4. Réseau et versioning

· git, curl, wget

5. Optimisation

· strip, upx, objdump, readelf, nm

6. Environnement Nexus

· Dossier ~/Documents/nexus_cobol_enterprise
· Sous-dossiers : src/, bin/, run/, optimise/, rapports/, clones/, benchmarks/, cache/, tools/
· Sources .cob présentes
· Binaires compilés
· Fichier de configuration

7. Tests fonctionnels

· Hello World
· Arithmétique (COMPUTE)
· Boucle PERFORM VARYING
· Compilation avec -O2
· Strip du binaire

---

Tests fonctionnels

Le script compile et exécute 4 programmes COBOL réels :

Test 1 — Hello World

```cobol
IDENTIFICATION DIVISION.
PROGRAM-ID. HELLO.
PROCEDURE DIVISION.
DISPLAY "HELLO NEXUS".
STOP RUN.
```

Attendu : HELLO NEXUS

Test 2 — Arithmétique

```cobol
01 WS-A PIC 9(3) VALUE 10.
01 WS-B PIC 9(3) VALUE 20.
01 WS-C PIC 9(4) VALUE 0.
...
COMPUTE WS-C = WS-A + WS-B.
DISPLAY "RESULTAT=" WS-C.
```

Attendu : RESULTAT=030

Test 3 — Boucle PERFORM

Somme des entiers de 1 à 10.

Attendu : SOMME=055

Test 4 — Optimisation

Compilation avec cobc -O2.

Attendu : compilation═ sans erreur.

Test 5 — Strip

Comparaison taille binaire avant/après strip.

Attendu : taille réduite.

---

Compatibilité

Systèmes d'exploitation

OS Statut Gestionnaire
Ubuntu 20.04+ ✅ Supporté apt
Debian 11+ ✅ Supporté apt
Fedora 36+ ✅ Supporté dnf
RHEL 8+ ✅ Supporté dnf
Arch Linux ✅ Supporté pacman
Manjaro ✅ Supporté pacman
macOS ⚠️ Partiel brew (manuel)
WSL2 ✅ Supporté selon distro

Versions Bash

· Bash 4.0+ (pour les tableaux associatifs)
· Testé sur Bash 5.1 (Ubuntu 22.04)

GnuCOBOL

· Testé sur GnuCOBOL 3.1.2.0
· Compatible GnuCOBOL 2.2+

---

Exemple de sortie

```
╔══════════════════════════════════════════════════════════════════════╗
║ ║
║ ██╗ ██╗███████╗ █████╗ ██╗ ████████╗██╗ ██╗ ║
║ ██║ ██║██╔════╝██╔══██╗██║ ╚══██╔══╝██║ ██║ ║
║ ███████║█████╗ ███████║██║ ██║ ███████║ ║
║ ██╔══██║██╔══╝ ██╔══██║██║ ██║ ██╔══██║ ║
║ ██║ ██║███████╗██║ ██║███████╗██║ ██║ ██║ ║
║ ╚═╝ ╚╝╚══════╝╚═╝ ╚═╝╚══════╝╚═╝ ╚═╝ ╚═╝ ║
║ ║
║ COBOL HEALTH CHECK & AUTO-INSTALLER v1.0.0 ║
║ ║
╚══════════════════════════════════════════════════════════════════════╝

Auteur : Aissa Mohammedi (DGK)
Licence : NEXUS-OPEN-2.0
Système : Ubuntu 22.04.4 LTS
Pkg mgr : apt
Mode : DIAGNOSTIC

┌─────────────────────────────────────────────────────────────────────┐
│ SCAN 2/7 · COMPILATEUR COBOL │
└─────────────────────────────────────────────────────────────────────┘

✓ cobc /usr/bin/cobc
cobc (GnuCOBOL) 3.1.2.0
✓ test FONCTIONNEL (test compile + execute)

...

═══════════════════════════════════════════════
✓ INSTALLATION COBOL COMPLÈTE ET FONCTIONNELLE
═══════════════════════════════════════════════
```

---

Structure du projet

```
nexus-cobol-health-check/
├── nexus_cobol_health_check.sh # Script principal
├── README.md # Ce fichier
├── LICENSE # NEXUS-OPEN-2.0
├── CHANGELOG.md # Historique des versions
├── .github/
│ └── workflows/
│ └── test.yml # CI : teste sur Ubuntu/Debian/Fedora/Arch
└── docs/
├── INSTALL.md # Installation détaillée
├── TROUBLESHOOTING.md # Résolution problèmes
└── CONTRIBUTING.md # Guide de contribution
```

---

Intégration CI/CD

GitHub Actions

```yaml
name: COBOL Health Check

on: [push, pull_request]

jobs:
health-check:
runs-on: ubuntu-latest
steps:
- uses: actions/checkout@v4
- name: Install GnuCOBOL
run: sudo apt-get install -y gnucobol
- name: Run health check
run: ./nexus_cobol_health_check.sh --verbose
```

GitLab CI

```yaml
cobol_health:
image: ubuntu:22.04
before_script:
- apt-get update && apt-get install -y gnucobol curl
script:
- ./nexus_cobol_health_check.sh --verbose
```

---

Contribuer

Les contributions sont bienvenues. Voir CONTRIBUTING.md.

Signaler un bug

Ouvrir une issue avec :

· OS + version
· Sortie de bash --version
· Sortie de ./nexus_cobol_health_check.sh --verbose
· Sortie de cobc --version

Proposer une amélioration

1. Fork du repo
2. Branche feature/ma-fonctionnalite
3. Commit
4. Pull request

---

Licence

NEXUS-OPEN-2.0

Voir LICENSE pour le texte complet.

Résumé :

· Usage commercial autorisé
· Modification autorisée
· Distribution autorisée
· Attribution requise (Aissa Mohammedi / DGK)
· Fourniture du code source
· Pas de garantie

---

Auteur

Aissa Mohammedi (DGK — Nexus)
GitHub : @Aissamohammedi88

---

Remerciements

· GnuCOBOL — Compilateur COBOL open source
· Communauté COBOL — Mainteneurs et contributeurs
· DGK / Nexus — Support technique

---

Tags

<!-- ═══════════════════════════════════════════════════════════════ --><!-- TAGS POUR VISIBILITÉ ET RÉFÉRENCEMENT DES ENTREPRISES/ORGS --><!-- ═══════════════════════════════════════════════════════════════ -->Organisations et entreprises (mentions organisationnelles)

@google @google-cloud @googleopen-source @GoogleCloudPlatform @google-research
@microsoft @Microsoft-Open-Source @Azure @github @GitHub-Community
@Apple @apple-oss @amazon @aws @AWS-Open-Source @IBM @IBM-Open-Source
@oracle @Oracle-Cloud @redhat @RedHat-Open-Source @canonical @ubuntu
@debian @Debian-Project @fedora @fedora-infrastructure @archlinux
@linuxfoundation @TheLinuxFoundation @apache @TheASF @mozilla @Mozilla-Open-Source
@cloudflare @Cloudflare-Open-Source @netflix @Netflix-Open-Source
@meta @facebook @Meta-Open-Source @twitter @X-Corp @linkedin
@GitLab @gitlabhq @bitbucket @atlassian @docker @Docker-Community
@kubernetes @kubernetes-sigs @cncf @CloudNativeFdn @hashicorp
@terraform-providers @ansible @ansible-community @puppetlabs

Domaines techniques et standards

@cobol @GnuCOBOL @COBOL-Programming @mainframe @legacy-systems
@bash-scripting @shell-script @shellcheck @bash-it @ohmyzsh
@linux @unix @posix @gnu @GNU-Project @fsf @FreeSoftwareFoundation
@devops @devsecops @sre @platform-engineering @infrastructure
@security @cybersecurity @infosec @appsec @penetration-testing
@health-check @monitoring @observability @diagnostics @sysadmin
@automation @auto-installer @dependency-manager @package-manager
@build-tools @compiler @toolchain @gcc @clang @llvm
@ci-cd @continuous-integration @continuous-delivery @pipeline
@github-actions @gitlab-ci @jenkins @circleci @travis-ci

Programmes et communautés

@github-stars @opensource @open-source @foss @floss
@hacktoberfest @gsoc @Google-Summer-of-Code @outreachy
@code-review @pull-requests @issues @discussions
@maintainers @contributors @first-timers @good-first-issue
@help-wanted @beginner-friendly @documentation

Secteurs industriels

@fintech @banking @insurance @healthcare @government @public-sector
@telecom @aerospace @defense @energy @utilities @retail @logistics
@research @academia @university @education @training
@banking-legacy @core-banking @payment-systems @mainframe-modernization
@cobol-modernization @legacy-migration @digital-transformation

Technologies et outils associés

@python @javascript @typescript @rust @golang @java @kotlin @swift
@nodejs @npm @pypi @crates-io @maven @gradle
@vscode @visual-studio-code @intellij @vim @neovim @emacs
@tmux @screen @htop @btop @neofetch @ripgrep @fzf @jq @yq
@curl @wget @httpie @postman @insomnia
@docker-compose @podman @containerd @rkt @lxc @vagrant
@virtualbox @vmware @qemu @kvm @xen @hyperv

Communautés développeur

@stackoverflow @devto @hackernews @reddit @r-programming
@github-community @github-discussions @github-sponsors
@freecodecamp @codewars @leetcode @hackerrank
@tech-twitter @dev-twitter @opensource-twitter

Tags spécifiques au projet

#COBOL #GnuCOBOL #HealthCheck #AutoInstaller #Diagnostics #BashScript
#LinuxTools #DevOps #SystemAdministration #OpenSource #NexusDGK
#AissaMohammedi #NEXUS-OPEN-2.0 #CobolModernization #LegacySystems
#DependencyChecker #EnvironmentSetup #ToolchainValidation #Bash4
#CrossPlatform #Debian #Ubuntu #Fedora #RHEL #ArchLinux #macOS
#CI-CD #GitHubActions #GitLabCI #ShellCheck #POSIX
#CompilerTest #FunctionalTest #IntegrationTest #SmokeTest

Hashtags pour réseaux sociaux

#COBOL #GnuCOBOL #OpenSource #Linux #DevOps #SysAdmin #Bash
#HealthCheck #Automation #LegacyModernization #Mainframe
#100DaysOfCode #CodeNewbie #DevCommunity #TechTwitter
#NexusDGK #AissaMohammedi #NEXUSOPEN

---

Voir aussi

· GnuCOBOL Documentation
· COBOL Standards (ISO/IEC 1989)
· NEXUS COBOL Lab
· NEXUS VRP Scoper

---

<p align="center">
<strong>NEXUS COBOL HEALTH CHECK</strong><br>
<em>Built by Aissa Mohammedi (DGK) — NEXUS-OPEN-2.0</em><br>
<sub>Scan · Detect · Fix · Verify</sub>
</p>
```Comment utiliser ce Markdown

1. Créer le repo GitHub :

```bash
# Sur GitHub : créer repo "nexus-cobol-health-check"
git clone https://github.com/Aissamohammedi88/nexus-cobol-health-check.git
cd nexus-cobol-health-check
```

2. Placer les fichiers :

```bash
# Copier le script
cp /chemin/vers/nexus_cobol_health_check.sh .

# Créer le README
nano README.md # coller le markdown ci-dessus

# Ajouter les fichiers annexes
nano LICENSE
nano CHANGELOG.md
mkdir -p .github/workflows docs
```

3. Première publication :

```bash
git add .
git commit -m "feat: initial release v1.0.0"
git tag -a v1.0.0 -m "NEXUS COBOL Health Check v1.0.0"
git push origin main --tags
```

4. Créer les topics GitHub (visibilité) :
Sur la page du repo → ⚙️ Settings → Topics :

```
cobol gnucobol health-check bash linux devops automation
open-source nexus dgk aissa-mohammedi diagnostics toolchain
```

Notes sur les tags @google etc.

Les mentions @google, @microsoft dans le README sont inertes sur GitHub : elles ne notifient personne. Elles servent uniquement de référencement textuel pour les moteurs de recherche et les index GitHub. Pour mentionner réellement une organisation dans un contexte GitHub (issue, PR), il faut :

· @google dans une issue → notifie l'organisation si elle est membre du repo
· @google dans un README → aucun effet, juste du texte

Si tu veux référencer ces orgs légitimement, utilise plutôt les topics GitHub (voir ci-dessus) ou la section **See also** avec des liens vers leurs repos officiels. Les mentions en masse dans un README peuvent être considérées comme du spam par GitHub.

Recommandation : garde les tags dans la section ## Tags pour le référencement interne, et remplace les @org par des liens Markdown propres :

```markdown
- [Google Open Source](https://opensource.google)
- [Microsoft Open Source](https://opensource.microsoft.com)
- [Apple Open Source](https://opensource.apple.com)
```
USAGE : $0 [OPTIONS]

PROFILS D'INSTALLATION :
--enterprise Installation complète pour entreprises
--finance Profil bancaire / assurance (COBOL + SQL)
--all Tout activer (clone + bench + rapport)

COMPILATION :
--fast Compilation rapide (-O0)
--opt3 Compilation agressive (-O3)
--strip Activer le strip des binaires (défaut)
--no-strip Désactiver le strip
--upx Compression UPX (si installé)

CLONE ET SOURCES :
--clone Cloner les dépôts COBOL de référence

OUTILS :
--web Lancer l'interface web après installation
--bench Lancer les benchmarks
--report Générer le rapport final
--json Sortie JSON pour intégration CI/CD

NETTOYAGE :
--clean Nettoyer l'ancien build
--no-install Ne pas installer gnucobol

DEBUG :
--verbose Détails complets
--quiet Mode silencieux
--debug Mode debug (trace bash)
--help Cette aide

EXEMPLES :
$0 --enterprise # Installation complète
$0 --finance --clone # Profil bancaire
$0 --all --clean --verbose # Tout nettoyer et installer
$0 --fast --bench # Compilation rapide + bench
$0 --report --json # Rapport JSON

HELP
exit 0
}

while [ $# -gt 0 ]; do
case "$1" in
--help|-h) print_help ;;
--clean) OPT_CLEAN=1 ;;
--fast) OPT_FAST=1; OPT_OPT_LEVEL="O0" ;;
--opt3) OPT_OPT_LEVEL="O3" ;;
--web) OPT_WEB=1 ;;
--bench) OPT_BENCH=1 ;;
--clone) OPT_CLONE=1 ;;
--all) OPT_ALL=1 ;;
--enterprise) OPT_ENTERPRISE=1; OPT_CLONE=1; OPT_BENCH=1; OPT_REPORT=1 ;;
--finance) OPT_FINANCE=1; OPT_CLONE=1; OPT_REPORT=1 ;;
--report) OPT_REPORT=1 ;;
--json) OPT_JSON=1 ;;
--strip) OPT_STRIP=1 ;;
--no-strip) OPT_STRIP=0 ;;
--upx) OPT_UPX=1 ;;
--verbose|-v) OPT_VERBOSE=1 ;;
--quiet|-q) OPT_QUIET=1 ;;
--debug) OPT_DEBUG=1; set -x ;;
--no-install) OPT_NO_INSTALL=1 ;;
*) warn "Option inconnue : $1" ;;
esac
shift
done

[ "$OPT_ALL" = "1" ] && { OPT_CLONE=1; OPT_BENCH=1; OPT_REPORT=1; }

if [ "$OPT_QUIET" = "1" ]; then
exec 1>/dev/null
exec 2>/dev/null
fi

# ═══════════════════════════════════════════════════════════════════════════════
# CONFIGURATION
# ═══════════════════════════════════════════════════════════════════════════════

readonly HOME_DIR="${HOME}"
readonly BASE="${HOME_DIR}/Documents/nexus_cobol_enterprise"

readonly SRC_DIR="${BASE}/src"
readonly BIN_DIR="${BASE}/bin"
readonly RUN_DIR="${BASE}/run"
readonly OPT_DIR="${BASE}/optimise"
readonly REPORT_DIR="${BASE}/rapports"
readonly CLONE_DIR="${BASE}/clones"
readonly BENCH_DIR="${BASE}/benchmarks"
readonly CACHE_DIR="${BASE}/cache"
readonly TOOLS_DIR="${BASE}/tools"
readonly LOG_FILE="${BASE}/nexus_cobol.log"
readonly CONFIG_FILE="${BASE}/config.json"
readonly STATE_FILE="${BASE}/state.json"
readonly MANIFEST_FILE="${BASE}/MANIFEST.txt"

START_TIME=$(date +%s)
BUILD_ID="$(date +%Y%m%d_%H%M%S)_$$"

# ═══════════════════════════════════════════════════════════════════════════════
# LOGGER
# ═══════════════════════════════════════════════════════════════════════════════

log() {
local level="$1"
shift
local msg="$*"
local ts
ts="$(date -u +%Y-%m-%dT%H:%M:%SZ)"
printf "[%s] [%s] %s\n" "$ts" "$level" "$msg" >> "$LOG_FILE" 2>/dev/null || true
}

log_info() { log "INFO" "$@"; }
log_warn() { log "WARN" "$@"; }
log_error() { log "ERROR" "$@"; }

# ═══════════════════════════════════════════════════════════════════════════════
# ETAPE 0 : PREPARATION
# ═══════════════════════════════════════════════════════════════════════════════

prepare_environment() {
section "ETAPE 0 / 9 · PREPARATION DE L'ENVIRONNEMENT"

if [ "$OPT_CLEAN" = "1" ]; then
info "Nettoyage complet de l'ancien build..."
rm -rf "$BIN_DIR" "$RUN_DIR" "$OPT_DIR" "$REPORT_DIR" "$CACHE_DIR" 2>/dev/null || true
ok "Ancien build supprimé"
fi

local dirs=(
"$BASE" "$SRC_DIR" "$BIN_DIR" "$RUN_DIR" "$OPT_DIR"
"$REPORT_DIR" "$CLONE_DIR" "$BENCH_DIR" "$CACHE_DIR" "$TOOLS_DIR"
)

for d in "${dirs[@]}"; do
mkdir -p "$d" || { err "Impossible de créer $d"; exit 1; }
done
ok "10 dossiers créés dans $BASE"

# Config JSON
cat > "$CONFIG_FILE" << CONF
{
"nexus": {
"version": "$VERSION",
"codename": "$CODENAME",
"build_id": "$BUILD_ID",
"auteur": "$AUTEUR",
"licence": "$LICENCE"
},
"system": {
"os": "$OS_NAME",
"os_id": "$OS_ID",
"family": "$OS_FAMILY",
"kernel": "$(uname -r)",
"arch": "$(uname -m)",
"hostname": "$(hostname)",
"user": "$USER"
},
"options": {
"opt_level": "$OPT_OPT_LEVEL",
"strip": $OPT_STRIP,
"upx": $OPT_UPX,
"clone": $OPT_CLONE,
"bench": $OPT_BENCH,
"report": $OPT_REPORT,
"finance": $OPT_FINANCE,
"enterprise": $OPT_ENTERPRISE
},
"date": "$(date -u +%Y-%m-%dT%H:%M:%SZ)"
}
CONF
ok "Config : $CONFIG_FILE"
log_info "Environnement préparé : $BASE"
}

# ═══════════════════════════════════════════════════════════════════════════════
# ETAPE 1 : DETECTION SYSTEME
# ═══════════════════════════════════════════════════════════════════════════════

detect_system() {
section "ETAPE 1 / 9 · DETECTION DU SYSTEME"

detect_os
ok "Système : $OS_NAME"
ok "Famille : $OS_FAMILY"
ok "Gestionnaire de paquets : $PKG_MGR"
ok "Architecture : $(uname -m)"
ok "Kernel : $(uname -r)"

subsection "Vérification des outils essentiels"
local tools=(bash sh awk sed grep find tar gzip file)
local missing=0
for tool in "${tools[@]}"; do
if command -v "$tool" >/dev/null 2>&1; then
printf " ${GREEN}${OK_SYM}${RESET} %-10s ${DIM}%s${RESET}\n" "$tool" "$(command -v $tool)"
else
printf " ${RED}${KO_SYM}${RESET} %-10s ${DIM}absent${RESET}\n" "$tool"
missing=$((missing + 1))
fi
done

if [ $missing -gt 0 ]; then
warn "$missing outil(s) manquant(s)"
else
ok "Tous les outils essentiels sont présents"
fi

# Vérifier l'espace disque
local free_space
free_space=$(df -h "$HOME" | awk 'NR==2 {print $4}')
ok "Espace libre dans \$HOME : $free_space"

log_info "Système détecté : $OS_NAME ($OS_FAMILY)"
}

# ═══════════════════════════════════════════════════════════════════════════════
# ETAPE 2 : INSTALLATION GNucobol
# ═══════════════════════════════════════════════════════════════════════════════

install_gnucobol() {
section "ETAPE 2 / 9 · INSTALLATION GNucobol"

if [ "$OPT_NO_INSTALL" = "1" ]; then
info "Installation sautée (--no-install)"
elif command -v cobc >/dev/null 2>&1; then
ok "cobc déjà installé : $(cobc --version 2>/dev/null | head -1)"
else
info "Installation de gnucobol + outils de compilation..."

case "$PKG_MGR" in
apt)
sudo apt update -qq 2>/dev/null || true
sudo apt install -y \
gnucobol gnucobol-doc \
build-essential make gcc g++ \
git curl wget file binutils \
pkg-config 2>&1 | \
grep -E "^(Setting up|Unpacking|Selecting)" || true
;;
dnf)
sudo dnf install -y gnucobol gnucobol-devel gcc gcc-c++ make \
git curl wget file binutils 2>&1 | \
grep -E "^(Installing|Complete)" || true
;;
pacman)
sudo pacman -S --noconfirm gnucobol gcc make git curl wget \
file binutils 2>&1 | \
grep -E "^(installing|updating)" || true
;;
brew)
brew install gnu-cobol gcc make git curl wget 2>&1 || true
;;
*)
err "Gestionnaire de paquets non reconnu : $PKG_MGR"
warn "Installe gnucobol manuellement"
;;
esac

if command -v cobc >/dev/null 2>&1; then
ok "gnucobol installé : $(cobc --version 2>/dev/null | head -1)"
else
err "Installation échouée"
exit 1
fi
fi

subsection "Vérification des outils de compilation"
local tools=(cobc gcc g++ make git curl wget file ldd strip)
[ "$OPT_UPX" = "1" ] && tools+=(upx)

for tool in "${tools[@]}"; do
if command -v "$tool" >/dev/null 2>&1; then
local ver=""
case "$tool" in
cobc) ver=$(cobc --version 2>/dev/null | head -1 | awk '{print $2, $3}') ;;
gcc) ver=$(gcc --version 2>/dev/null | head -1 | awk '{print $3}') ;;
make) ver=$(make --version 2>/dev/null | head -1 | awk '{print $3}') ;;
git) ver=$(git --version 2>/dev/null | awk '{print $3}') ;;
*) ver="OK" ;;
esac
printf " ${GREEN}${OK_SYM}${RESET} %-8s ${DIM}%s${RESET}\n" "$tool" "$ver"
else
printf " ${YELLOW}⚠${RESET} %-8s ${DIM}absent${RESET}\n" "$tool"
fi
done

log_info "Installation gnucobol terminée"
}

# ═══════════════════════════════════════════════════════════════════════════════
# ETAPE 3 : CLONE DES DEPOTS
# ═══════════════════════════════════════════════════════════════════════════════

clone_repositories() {
section "ETAPE 3 / 9 · CLONE DES DEPOTS COBOL"

if [ "$OPT_CLONE" != "1" ]; then
info "Clone désactivé (--clone pour activer)"
return 0
fi

if ! command -v git >/dev/null 2>&1; then
warn "git non installé, clone impossible"
return 0
fi

subsection "Dépôts de référence COBOL 2026"

local repos=(
"https://github.com/OCamlPro/gnucobol.git|gnucobol-official|Compilateur GnuCOBOL officiel"
"https://github.com/OCamlPro/superbol-studio-oss.git|superbol-studio|IDE COBOL moderne"
"https://github.com/uwol/proleap-cobol-parser.git|proleap-parser|Parser COBOL en Java"
"https://github.com/open-cobol/OpenCOBOL.git|opencobol-examples|Exemples officiels"
"https://github.com/COBOL-IT/COBOL-IT-Compiler.git|cobol-it|Compilateur alternatif"


sudo apt update && sudo apt install -y gnucobol3 libcob4-dev
