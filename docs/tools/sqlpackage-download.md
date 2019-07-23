---
title: Baixar e instalar o sqlpackage | Microsoft Docs
description: Baixar e instalar o sqlpackage para Windows, macOS ou Linux
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
ms.openlocfilehash: 406fb50ceaba177d02bf8d79d0c37191dbe178f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986258"
---
# <a name="download-and-install-sqlpackage"></a>Baixar e instalar o sqlpackage

O sqlpackage é executado no Windows, macOS e Linux.

Baixar e instalar a versão mais recente do .NET Framework e as versões prévias do macOS e Linux:

|Plataforma|Download|Data de liberação|Versão|Compilação
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2087429)|15 de abril de 2019|18.2|15.0.4384.2|
|.NET Core para macOS (versão prévia)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2087247)|15 de abril de 2019 | 18.2 |15.0.4384.2|
|.NET Core para Linux (versão prévia)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2087431)|15 de abril de 2019 | 18.2 |15.0.4384.2|

Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](release-notes-sqlpackage.md).

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="get-sqlpackage-for-windows"></a>Obter o sqlpackage para Windows

Esta versão do sqlpackage inclui uma experiência padrão do instalador do Windows e um .zip: 

1. Baixe e execute o [instalador DacFramework.msi para Windows](https://go.microsoft.com/fwlink/?linkid=2087429).
2. Abra uma nova janela do prompt de comando e execute sqlpackage.exe
    - O sqlpackage é instalado na pasta ```C:\Program Files\Microsoft SQL Server\150\DAC\bin```
    - Instalando a versão x86 em um computador x64, o sqlpackage é instalado na pasta ```C:\Program Files (x86)\Microsoft SQL Server\150\DAC\bin```

## <a name="get-sqlpackage-preview-for-macos"></a>Obter o sqlpackage (versão prévia) para macOS

1. Baixe o [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=2087247).
2. Para extrair o arquivo e iniciar o sqlpackage, abra uma nova janela do terminal e digite os seguintes comandos:

   **Instalação do .zip:**

   ```bash
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage
   ```

## <a name="get-sqlpackage-preview-for-linux"></a>Obter o sqlpackage (versão prévia) para Linux

1. Baixe o [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=2087431) usando um dos instaladores ou arquivos tar.gz:
2. Para extrair o arquivo e iniciar o sqlpackage, abra uma nova janela do terminal e digite os seguintes comandos:

   **Instalação do .zip:**

   ```bash
   cd ~
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip -d ~/sqlpackage 
   echo "export PATH=\"\$PATH:$HOME/sqlpackage\"" >> ~/.bashrc
   chmod a+x ~/sqlpackage/sqlpackage
   source ~/.bashrc
   sqlpackage
   ```

   > [!NOTE]
   > No Debian, Redhat e Ubuntu, você pode ter dependências ausentes. Use os seguintes comandos para instalar estas dependências, de acordo com sua versão do Linux:

   **Debian:**

   ```bash
   sudo apt-get install libunwind8
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

## <a name="uninstall-sqlpackage-preview"></a>Desinstalar o sqlpackage (versão prévia)

Se você instalou o sqlpackage usando o instalador do Windows, desinstale da mesma forma que você remove aplicativos do Windows.

Se você instalou o sqlpackage com um arquivo .zip ou outros arquivos, simplesmente exclua os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

O sqlpackage é executado no Windows, macOS e Linux, é tem suporte nas plataformas a seguir:

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

- Saiba mais sobre o [sqlpackage](sqlpackage.md)

[Política de Privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
