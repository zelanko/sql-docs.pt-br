---
title: Baixar o driver ODBC para SQL Server
description: Baixe o Microsoft ODBC Driver for SQL Server para desenvolver aplicativos de código nativo que se conectam ao SQL Server e ao Banco de Dados SQL do Azure.
ms.date: 04/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53b09784-bb9d-4fd4-99d3-0492b3308ac4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba443225baa1e84a56fd9ce114ec8ff6fa96ebb9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488576"
---
# <a name="download-odbc-driver-for-sql-server"></a>Baixar o driver ODBC para SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

O Microsoft ODBC Driver for SQL Server é uma DLL (biblioteca de vínculo dinâmico) única que contém suporte de runtime aos aplicativos que usam APIs de código nativo para se conectar ao SQL Server. Use o Microsoft ODBC Driver 17 for SQL Server para criar aplicativos ou aprimorar os aplicativos existentes que precisam aproveitar os novos recursos do SQL Server.

## <a name="download-for-windows"></a>Download para Windows

O instalador redistribuível do Microsoft ODBC Driver 17 for SQL Server instala os componentes cliente, que são necessários durante o runtime para aproveitar os recursos mais recentes do SQL Server. Opcionalmente, ele instala os arquivos de cabeçalho necessários para desenvolver um aplicativo que usa a API ODBC. Na versão 17.4.2 em diante, o instalador também inclui e instala a Biblioteca de Autenticação do Microsoft Active Directory (ADAL.dll).

A versão 17.5.2 é a última versão em disponibilidade geral. Caso você tenha uma versão anterior do Microsoft ODBC Driver 17 for SQL Server instalada, a instalação da versão 17.5.2 fará um upgrade dela para a 17.5.2.

**[![Download](../../ssms/media/download-icon.png) Baixar o Microsoft ODBC Driver 17 for SQL Server (x64)](https://go.microsoft.com/fwlink/?linkid=2120137)**  
**[![Download](../../ssms/media/download-icon.png) Baixar o Microsoft ODBC Driver 17 for SQL Server (x86)](https://go.microsoft.com/fwlink/?linkid=2120140)**  

### <a name="version-information"></a>Informações da versão

- Número da versão: 17.5.2.1
- Lançado: 6 de março de 2020

> [!Note]
> Se você estiver acessando esta página em uma versão de idioma diferente do inglês e desejar ver o conteúdo mais atualizado, acesse a [versão do site em inglês dos EUA](https://aka.ms/downloadmsodbcsqlenglish). Você pode baixar idiomas diferentes do site da versão em inglês dos EUA selecionando [idiomas disponíveis](#available-languages).

## <a name="available-languages"></a>Idiomas disponíveis

Esta versão do Microsoft ODBC Driver for SQL Server pode ser instalada nos seguintes idiomas:

Microsoft ODBC Driver 17.5.2 for SQL Server (x64):  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x40a)

Microsoft ODBC Driver 17.5.2 for SQL Server (x86):  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x40a)

### <a name="release-notes-for-windows"></a>Notas sobre a versão do Windows

Para obter detalhes sobre esta versão no Windows, confira [as notas sobre a versão do Windows](windows\release-notes-odbc-sql-server-windows.md).

### <a name="previous-releases-for-windows"></a>Versões anteriores do Windows

Para baixar versões anteriores do Windows, confira [Versões anteriores do Microsoft ODBC Driver for SQL Server](windows\release-notes-odbc-sql-server-windows.md#previous-releases).

## <a name="download-for-linux-and-macos"></a>Download para Linux e macOS

O Microsoft ODBC Driver for SQL Server pode ser baixado e instalado com gerenciadores de pacotes para Linux e macOS por meio das instruções de instalação relevantes:  
[Instalar o ODBC for SQL Server (Linux)](linux-mac\installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Instalar o ODBC for SQL Server (macOS)](linux-mac\install-microsoft-odbc-driver-sql-server-macos.md)  

Se você precisar baixar os pacotes para instalação offline, todas as versões estarão disponíveis por meio dos links abaixo.

> [!Note]
> Os pacotes nomeados `msodbcsql17-*` são a última versão. Os pacotes nomeados `msodbcsql-*` são a versão 13 do driver.

### <a name="alpine"></a>Alpine

- [Pacote do Alpine](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.apk) ([Assinatura do PGP](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.sig))

### <a name="debian"></a>Debian

- [Pacotes .deb do Debian 10](https://packages.microsoft.com/debian/10/prod/pool/main/m/msodbcsql17/)
- [Pacotes .deb do Debian 9](https://packages.microsoft.com/debian/9/prod/pool/main/m/msodbcsql17/)
- [Pacotes .deb do Debian 8](https://packages.microsoft.com/debian/8/prod/pool/main/m/msodbcsql17/)
- [Pacotes .deb do Debian 8 (msodbcsql 13.x)](https://packages.microsoft.com/debian/8/prod/pool/main/m/msodbcsql/)

### <a name="redhat"></a>RedHat

- [Pacotes .rpm do Red Hat 8](https://packages.microsoft.com/rhel/8/prod/)
- [Pacotes .rpm do Red Hat 7](https://packages.microsoft.com/rhel/7/prod/)
- [Pacotes .rpm do Red Hat 6](https://packages.microsoft.com/rhel/6/prod/)

### <a name="suse"></a>Suse

- [Pacotes .rpm do SUSE 15](https://packages.microsoft.com/sles/15/prod/)
- [Pacotes .rpm do SUSE 12](https://packages.microsoft.com/sles/12/prod/)
- [Pacotes .rpm do SUSE 11](https://packages.microsoft.com/sles/11/prod/)

### <a name="ubuntu"></a>Ubuntu

- [Pacotes .deb do Ubuntu 19.10](https://packages.microsoft.com/ubuntu/19.10/prod/pool/main/m/msodbcsql17/)
- [Pacotes .deb do Ubuntu 18.04](https://packages.microsoft.com/ubuntu/18.04/prod/pool/main/m/msodbcsql17/)
- [Pacotes .deb do Ubuntu 16.04](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql17/)
- [Pacotes .deb do Ubuntu 14.04](https://packages.microsoft.com/ubuntu/14.04/prod/pool/main/m/msodbcsql17/)
- [Pacotes .deb do Ubuntu 16.04 (msodbcsql 13.x)](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/)
- [Pacotes .deb do Ubuntu 14.04 (msodbcsql 13.x)](https://packages.microsoft.com/ubuntu/14.04/prod/pool/main/m/msodbcsql/)

Confira também [Como instalar o driver do Linux](linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="macos"></a>macOS

- Confira o [Homebrew Formulae](https://github.com/Microsoft/homebrew-mssql-release) para obter detalhes.

Confira também [Como instalar o driver do macOS](linux-mac/install-microsoft-odbc-driver-sql-server-macos.md).

### <a name="older-linux-releases"></a>Versões mais antigas do Linux

- **Red Hat Enterprise Linux 5 e 6 (64 bits)**  - [Baixar o Microsoft ODBC Driver 11 for SQL Server – Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
- **SUSE Linux Enterprise 11 Service Pack 2 (64 bits)**  - [Baixar a versão prévia do Microsoft ODBC Driver 11 for SQL Server – SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)

### <a name="release-notes-for-linux-and-macos"></a>Notas sobre a versão do Linux e do macOS

Para obter detalhes sobre as versões do Linux e do macOS, confira [as notas sobre a versão do Linux e do macOS](linux-mac\release-notes-odbc-sql-server-linux-mac.md).
