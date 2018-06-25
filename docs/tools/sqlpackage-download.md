---
title: Baixe e instale o sqlpackage | Microsoft Docs
description: Baixe e instale o sqlpackage para Windows, macOS ou Linux
ms.custom: tools|sos
ms.date: 06/18/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: 4e5528ca046de83385171890fbda389928e41cf3
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703821"
---
# <a name="download-and-install-sqlpackage"></a>Baixe e instale o sqlpackage

sqlpackage é executado no Windows, macOS e Linux.

Baixe e instale a versão mais recente do .NET Framework e macOS e visualizações do Linux:

|Plataforma|Download|Data de liberação|Versão|Compilação|
|:---|:---|:---|:---|:---|
|Windows|[Instalador](https://go.microsoft.com/fwlink/?linkid=875508)|25 de janeiro de 2018|17.4.1|14.0.3917.1|
|macOS (visualização)|[.zip](https://go.microsoft.com/fwlink/?linkid=873927)|9 de maio de 2018 |0.0.1|15.0.4057.1|
|Linux (versão prévia)|[.zip](https://go.microsoft.com/fwlink/?linkid=873926)|9 de maio de 2018 |0.0.1|15.0.4057.1|

## <a name="get-sqlpackage-for-windows"></a>Obter sqlpackage para Windows

Esta versão do sqlpackage inclui uma experiência de instalação padrão do Windows e. zip: 

**Instalador**

1. Baixe e execute o [DacFramework.msi installer para Windows](https://go.microsoft.com/fwlink/?linkid=875508).
2. Abra uma nova janela de Prompt de comando e execute sqlpackage.exe
    - sqlpackage está instalado para o ```C:\Program Files\Microsoft SQL Server\140\DAC\bin``` pasta

## <a name="get-sqlpackage-preview-for-macos"></a>Obter sqlpackage (visualização) para macOS

1. Baixar [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=873927).
2. Para extrair o arquivo e inicie sqlpackage, abra uma nova janela do Terminal e digite os seguintes comandos:

   **Instalação do .zip:**
   ```bash 
   mv ~/Downloads/sqlpackage-linux-<version string> ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage 
   ``` 

## <a name="get-sqlpackage-preview-for-linux"></a>Obter sqlpackage (visualização) para Linux

1. Baixar [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=873926) usando os instaladores ou o arquivamento gz:
2. Para extrair o arquivo e inicie sqlpackage, abra uma nova janela do Terminal e digite os seguintes comandos:

   **Instalação do .zip:**
   ```bash 
   cd ~ 
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bashrc
   source ~/.bashrc 
   sqlpackage 
   ``` 

   > [!NOTE]
   > No Debian, Redhat e Ubuntu, você pode ter dependências ausentes. Use os comandos a seguir para instalar essas dependências, dependendo de sua versão do Linux:
   

   **Debian:** 
   ```bash
   sudo apt-get install libuwind8
   ```

   **Red Hat:** 
   ```bash
   yum install libunwind 
   yum install libicu 
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   sudo apt-get install libicu52      # for 14.x
   sudo apt-get install libicu55      # for 16.x
   sudo apt-get install libicu57      # for 17.x
   sudo apt-get install libicu60      # for 18.x
   ```


## <a name="uninstall-sqlpackage-preview"></a>Desinstalar o sqlpackage (visualização)

Se você instalou o sqlpackage usando o Windows installer, desinstale o da mesma maneira que você remova qualquer aplicativo do Windows.

Se você instalou sqlpackage com outros arquivamento ou. zip, simplesmente exclua os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

sqlpackage é executado no Linux, Windows e macOS e é suportado nas seguintes plataformas:

### <a name="windows"></a>Windows
- Windows 10
- Windows 8.1 
- Windows 8 
- Windows 7 SP1 
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012 
- Windows Server 2008 R2

### <a name="macos"></a>macOS
- macOS 10.13 Serra alta
- macOS 10.12 Serra

### <a name="linux-x64"></a>Linux (x64)
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- Saiba mais sobre [sqlpackage](sqlpackage.md)

[Política de Privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
