<p align="center">
<h1 align="center"> OmniEdge </h1>
<p align="center">What happens in intranet, stays in intranet.</p>
</p>

<p align="center">
<a href="https://omniedge.io">
<img alt="Website" src="https://img.shields.io/website?label=omniedge.io&url=https%3A%2F%2Fomniedge.io">
</a>
<a href="https://github.com/omniedgeio/omniedge">
<img src="https://img.shields.io/github/license/omniedgeio/omniedge">
</a>
<a href="https://github.com/omniedgeio/omniedge">
<img src="https://img.shields.io/github/downloads/omniedgeio/app-release/total">
</a>

<a href="https://twitter.com/intent/follow?screen_name=omniedgeio">
<img src="https://img.shields.io/twitter/follow/omniedgeio?label=follows&style=social" />
</a>
  <a href="https://github.com/omniedgeio/omniedge-cli">
    <img src="https://img.shields.io/github/languages/top/omniedgeio/omniedge-cli" />
  </a> 
    <a href="https://github.com/omniedgeio/omniedge-iOS">
    <img src="https://img.shields.io/github/languages/top/omniedgeio/omniedge-iOS" />
  </a>
      <a href="https://github.com/omniedgeio/omniedge-macOS">
    <img src="https://img.shields.io/github/languages/top/omniedgeio/omniedge-macOS" />
  </a> 
      <a href="https://github.com/omniedgeio/omniedge-windows">
    <img src="https://img.shields.io/github/languages/top/omniedgeio/omniedge-windows" />
  </a> 
        <a href="https://github.com/omniedgeio/omniedge-android">
<img src="https://img.shields.io/github/languages/top/omniedgeio/omniedge-android"
</a>
          <a href="https://github.com/omniedgeio/omniedge-synology">
    <img src="https://img.shields.io/github/languages/top/omniedgeio/omniedge-synology" />
  </a> 
</p>

[【English】](../README.md) [【繁体中文】](README-zh-Hant.md) [【简体中文】](README-zh-Hans.md) [【日本语】](README-JP.md) [【Español】](README-ES.md) [【Italiano】](README-IT.md) [【한국어】](README-KR.md) 
[【العربي】](README-AR.md) [【Tiếng Việt】](README-VN.md) [【แบบไทย】](README-TH.md)

OmniEdge è un'infrastruttura VPN di livello 2 p2p open source basata sul protocollo [n2n](https://github.com/ntop/n2n), un'alternativa VPN tradizionale. Nessun server centrale, facile da scalare con meno manutenzione. Ciò che accade in intranet, rimane in intranet.
   
![OmniEdge-clients](../OmniEdge-clients.png)

## Caratteristiche principali:

||||
|----|----|----|
|Gestione amministrazione dashboard|VPN mesh|App GUI desktop per MacOS(barra dei menu) e Windows(systray)|
|Reti virtuali multiple|VPN da sito a sito|App cli da riga di comando per Linux, FreeBSD, Raspbian e MacOS|
|Multi utenti|Trasferimento dati illimitato|App cli riga di comando per armv7, arm64, RISC-V64, x86_64 e amd64|
|Multi dispositivi|Connessione peer-to-peer crittografata|App mobili per iOS e Android|
|Supernodo self-hosted |Relè di connessione crittografato|App per tablet per iPad, tablet Android e Android TV|
|Condivisione rete virtuale|Supporto cloud ibrido|App NAS per Synology|
|Chiavi di sicurezza| Zero-Config|Assegnazione automatica dei supernodi pubblici|
|[Controllo dispositivo remoto](https://omniedge.io/docs/article/Cases/VNC)|[Rilascia file in remoto](https://omniedge.io/docs/article/Cases/landrop) |Assegnazione IP automatica |


Puoi trovare altre funzionalità nella pagina [Pricing](https://omniedge.io/pricing) per Enterprise.

## Inizia in 5 minuti

1. Registra il tuo account: [Registrati](https://omniedge.io/register)
2. [Scarica](https://omniedge.io/download) App OmniEdge per la tua piattaforma
3. Oppure esegui il seguente comando se desideri utilizzare la versione cli:
```bash
curl https://omniedge.io/install/omniedge-install.sh | bash
```
4. Accedi con la tua Email e password, seleziona la tua rete virtuale, connettiti!

Siete a posto!

E se vuoi accedere con la **chiave di sicurezza**, o gestire i tuoi dispositivi, vai e controlla [Documentazione](https://omniedge.io/docs) per ulteriori informazioni.

## Compila

### OmniEdge Cli

1. Ambiente: Golang 1.16.6
2. Compila:

- 2.1. Ubuntu /linux

```bash
sudo -E apt-get -y update
sudo -E apt-get install -y openssl
sudo -E apt-get install -y build-essential
sudo -E apt-get install -y libssl-dev
sudo -E apt-get install -y zip
git clone https://github.com/omniedgeio/omniedge-cli
cd omniedge-cli
go mod download
go generate
BUILD_ENV=prod make build
```

- 2.2. macOS

```bash
brew install autoconf automake libtool
git clone https://github.com/omniedgeio/omniedge-cli
cd omniedge-cli
go mod download
go generate
BUILD_ENV=prod make build-darwin
```

- 2.3. freebsd

```bash
su
pkg update && pkg install go gmake git openssl zip autoconf automake libtool
git clone https://github.com/omniedgeio/omniedge-cli
cd omniedge-cli
go mod download
go generate
BUILD_ENV=prod make build-freebsd
```

3. Compilazione incrociata

- 3.1 RISC-V

Sistema operativo host: Ubuntu 20.04

```bash
apt-get update
apt-get install -y openssl autoconf build-essential libssl-dev zip wget g++-riscv64-linux-gnu gcc-riscv64-linux-gnu

wget https://go.dev/dl/go1.18.4.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.18.4.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go version
export GOOS=linux
export GOARCH=riscv64
export CGO_ENABLED=1
export CC=riscv64-linux-gnu-gcc
git clone https://github.com/omniedgeio/omniedge-cli.git
cd omniedge-cli
go mod download
go generate
BUILD_ENV=prod make build-riscv64
```

L'omniedge-cli compilato si troverà in **/out/**

### OmniEdge Android

1. Scarica Android Studio: https://developer.android.com/studio
2. Ottieni il repository e compila

```bash
git clone https://github.com/omniedgeio/omniedge-android.git`
./gradlew test --stacktrace
./gradlew assembleDebug --stacktrace
```

Abbiamo anche preparato il CI per Github e Gitlab per la compilazione automatica.

1. Github: https://github.com/omniedgeio/omniedge-android/blob/main/.github/workflows/build.yml
2. GitLab: https://github.com/omniedgeio/omniedge-android/blob/main/.gitlab-ci.yml


### OmniEdge iOS

1. Scarica e installa Xcode
2. Ottieni il repository e compila

```bash
git clone https://github.com/omniedgeio/omniedge-iOS.git
cd omniedge-iOS
open OmniEdgeNew/OmniEdgeNew.xcworkspace
```

Xcode si aprirà automaticamente, devi impostare il tuo account sviluppatore per avviare la compilazione. Ti consigliamo di compilare il pacchetto sui tuoi dispositivi separatamente, in particolare il pacchetto **Tunnel**.

<img width="902" alt="image" src="https://user-images.githubusercontent.com/93888/180374544-0ae0fbd8-3413-427f-8e9b-ec0c49249f0e.png">

### OmniEdge-macOS

1. Scarica e installa Xcode
2. Ottieni il repository e compila

```bash
git clone https://github.com/omniedgeio/omniedge-macOS.git
cd omniedge-macOS
open Omniedge.xcodeproj
```

Xcode si aprirà automaticamente, devi impostare il tuo account sviluppatore per avviare la compilazione.

### OmniEdge-windows

1. Scarica e installa QT
2. Ottieni il repository e compila

```bash
git clone https://github.com/omniedgeio/omniedge-windows.git
cd omniedge-windows
```

apri **OmniEdge.pro** e inizia a compilare.

## Utilizzo

- [Virtual Network, Devices, Security Key, and Settings](https://omniedge.io/docs/article/admin)
- [Windows 7,10,11 for Intel or Arm](https://omniedge.io/docs/article/install/windows)
- [Android](https://omniedge.io/docs/article/install/android)
- [Linux Cli for raspberry Pi, Nvidia Jeston,and more](https://omniedge.io/docs/article/install/cli)
- [MacOS Cli](https://omniedge.io/docs/article/install/macoscli)
- [Synology](https://omniedge.io/docs/article/install/synology)
- [Docker](https://omniedge.io/docs/article/install/docker)
- [Github Action](https://omniedge.io/docs/article/install/github-action)
- [iOS](https://omniedge.io/docs/article/install/ios)
- [Setup custom supernode](https://omniedge.io/docs/article/install/customize-supernode)

## Casi d'uso

> Dicci il tuo caso d'uso, così possiamo condividerlo con gli altri

- [Remote connect windows without exposing public IP with Omniedge](https://omniedge.io/docs/article/Cases/RDP)
- [Display and control macOS, Linux and Windows ](https://omniedge.io/docs/article/Cases/VNC)
- [Keep connection with your AI based Project on Jetson](https://omniedge.io/docs/article/Cases/jetson)
- [Display and control your Android device with Omniedge from anywhere on MacOS, Windows and Linux](https://omniedge.io/docs/article/Cases/android-remote)
- [Talk to your family and share photos in a LAN on the internet](https://omniedge.io/docs/article/Cases/lan-messenger)
- [Air Drop Any Files between MacOS, Windows, Routers, Linux and Android with Omniedge from anywhere](https://omniedge.io/docs/article/Cases/landrop)

## Confrontare

- [VPN vs. OmniEdge](https://omniedge.io/docs/article/compare/vpn-vs-omniedge)
- [Express VPN vs. OmniEdge](https://omniedge.io/docs/article/compare/expressvpn-vs-omniedge)
- [frp/ngrok vs. OmniEdge](https://omniedge.io/docs/article/compare/frp-ngrok-vs-omniedge)
- [ZeroTier vs. OmniEdge](https://omniedge.io/docs/article/compare/zerotier-vs-omniedge)
- [n2n vs. OmniEdge](https://omniedge.io/docs/article/compare/n2n-vs-omniedge)

## Chi parla di noi

- [Founded by a Single Tweet Startup OmniEdge’s effort to let connect without concern](https://threat.technology/founded-by-a-single-tweet-startup-omniedges-effort-to-let-connect-without-concern/)
- [voonze: OmniEdge, to access your Intranet from the Internet using P2P](https://voonze.com/omniedge-to-access-your-intranet-from-the-internet-using-p2p/)
- [wwwhatsnew: OMNIEDGE, PARA ACCEDER A TU INTRANET DESDE INTERNET USANDO P2P](https://wwwhatsnew.com/2022/03/03/omniedge-para-acceder-a-tu-intranet-desde-internet-usando-p2p/)
- [l'Entrepreneur: OmniEdge, pour accéder à votre Intranet depuis Internet en P2P](https://lentrepreneur.co/style/technologie/omniedge-pour-acceder-a-votre-intranet-depuis-internet-en-p2p-04032022)
- [RunaCapital: Awesome OSS alternatives](https://github.com/RunaCapital/awesome-oss-alternatives)



## Contributors

[harri8807](https://github.com/orgs/omniedgeio/people/harri8807) , [Tex-Tang](https://github.com/Tex-Tang), [ivyxjc](https://github.com/orgs/omniedgeio/people/ivyxjc), [kidylee](https://github.com/kidylee), [EbenDang](https://github.com/orgs/omniedgeio/people/EbenDang)
,[zteshadow](https://github.com/zteshadow), [ChenYouping](https://github.com/orgs/omniedgeio/people/ChenYouping),[ddrandy](https://github.com/orgs/omniedgeio/people/ddrandy), **Tsingv**, [mtx2d](https://github.com/mtx2d)，[Blackrose](https://github.com/Blackrose), [cheung-chifung](https://github.com/cheung-chifung),[我不是矿神](https://imnks.com/5768.html)

> sentiti libero di parlarci di qualsiasi post relativo a noi tramite problema o PR.

----

Se hai altre domande, sentiti libero di parlare con noi su [Discussions](https://github.com/omniedgeio/omniedge/discussions).