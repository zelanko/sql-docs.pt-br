---
title: Baixe e instale o sqlpackage | Microsoft Docs
description: Baixe e instale o sqlpackage para Windows, macOS ou Linux
ms.custom: tools|sos
ms.date: 06/18/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: ecefe3f1abe47a1a4f1af967cb1a15ee9f4dd52b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800254"
---
# <a name="download-and-install-sqlpackage"></a>Baixe e instale o sqlpackage

sqlpackage é executado no Windows, macOS e Linux.

Baixe e instale a versão mais recente do .NET Framework e o macOS e Linux visualizações:

|Plataforma|Download|Data de liberação|Versão|Compilação|
|:---|:---|:---|:---|:---|
|Windows|[Instalador](https://go.microsoft.com/fwlink/?linkid=875508)|22 de junho de 2018|17.8|14.0.4079.2|
|macOS (versão prévia)|[.zip](https://go.microsoft.com/fwlink/?linkid=873927)|9 de maio de 2018 |0.0.1|15.0.4057.1|
|Linux (versão prévia)|[.zip](https://go.microsoft.com/fwlink/?linkid=873926)|9 de maio de 2018 |0.0.1|15.0.4057.1|

Para obter detalhes sobre a versão mais recente, consulte o [notas de versão](sqlpackage-release-notes.md).

## <a name="get-sqlpackage-for-windows"></a>Obter sqlpackage para Windows

Esta versão do sqlpackage inclui uma experiência padrão do Windows installer e. zip: 

1. Baixe e execute o [dacframework. msi installer para Windows](https://go.microsoft.com/fwlink/?linkid=875508).
2. Abra uma nova janela de Prompt de comando e execute sqlpackage.exe
    - sqlpackage é instalado para o ```C:\Program Files\Microsoft SQL Server\140\DAC\bin``` pasta

## <a name="get-sqlpackage-preview-for-macos"></a>Obter sqlpackage (visualização) para macOS

1. Baixe [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=873927).
2. Para extrair o arquivo e inicie o sqlpackage, abra uma nova janela do Terminal e digite os seguintes comandos:

   **Instalação do .zip:**

   ```bash
   mv ~/Downloads/sqlpackage-linux-<version string> ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage
   ```

## <a name="get-sqlpackage-preview-for-linux"></a>Obter sqlpackage (visualização) para Linux

1. Baixe [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=873926) usando um dos instaladores ou gz arquivo morto:
2. Para extrair o arquivo e inicie o sqlpackage, abra uma nova janela do Terminal e digite os seguintes comandos:

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
   > No Ubuntu, Redhat e Debian, você pode ter dependências ausentes. Use os comandos a seguir para instalar essas dependências, dependendo de sua versão do Linux:

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

Se você instalou o sqlpackage usando o instalador do Windows, desinstale da mesma maneira que você remova qualquer aplicativo do Windows.

Se você instalou o sqlpackage com um. zip ou de outro arquivo, simplesmente exclua os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

sqlpackage é executado no Windows, macOS e Linux e é suportado nas seguintes plataformas:

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

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- Saiba mais sobre [sqlpackage](sqlpackage.md)

[Política de Privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
