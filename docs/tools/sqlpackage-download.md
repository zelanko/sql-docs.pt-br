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
ms.openlocfilehash: 322a9ce1992bb2b4d0215cfefa747ea56e68472f
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050918"
---
# <a name="download-and-install-sqlpackage"></a>Baixe e instale o sqlpackage

sqlpackage é executado no Windows, macOS e Linux.

Baixe e instale a versão mais recente do .NET Framework e o macOS e Linux visualizações:

|Plataforma|Download|Data de liberação|Versão|Compilação
|:---|:---|:---|:---|:---|
|Windows|[Instalador MSI](https://go.microsoft.com/fwlink/?linkid=2033947)|24 de outubro de 2018|18.0|15.0.4200.1|
|macOS (versão prévia)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=873927)|9 de maio de 2018 |0.0.1|15.0.4057.1|
|Linux (versão prévia)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=873926)|9 de maio de 2018 |0.0.1|15.0.4057.1|

Para obter detalhes sobre a versão mais recente, consulte o [notas de versão](sqlpackage-release-notes.md).

## <a name="get-sqlpackage-for-windows"></a>Obter sqlpackage para Windows

Esta versão do sqlpackage inclui uma experiência padrão do Windows installer e. zip: 

1. Baixe e execute o [dacframework. msi installer para Windows](https://go.microsoft.com/fwlink/?linkid=2033947).
2. Abra uma nova janela de Prompt de comando e execute sqlpackage.exe
    - sqlpackage é instalado para o ```C:\Program Files\Microsoft SQL Server\150\DAC\bin``` pasta
    - Instalando o x86 versão em um x64 máquina, o sqlpackage é instalado para o ```C:\Program Files (x86)\Microsoft SQL Server\150\DAC\bin``` pasta

## <a name="get-sqlpackage-preview-for-macos"></a>Obter sqlpackage (visualização) para macOS

1. Baixe [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=873927).
2. Para extrair o arquivo e inicie o sqlpackage, abra uma nova janela do Terminal e digite os seguintes comandos:

   **Instalação do .zip:**

   ```bash
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
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
