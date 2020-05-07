---
title: Baixar e instalar o sqlpackage
description: Baixar e instalar o sqlpackage para Windows, macOS ou Linux
ms.custom: tools|sos
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
ms.reviewer: alayu; sstein
ms.date: 06/20/2018
ms.openlocfilehash: ed2292c2f2a5fe067b5602ffcf46d52ca93c2f08
ms.sourcegitcommit: bfb5e79586fd08d8e48e9df0e9c76d1f6c2004e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82262020"
---
# <a name="download-and-install-sqlpackage"></a>Baixar e instalar o sqlpackage

O sqlpackage é executado no Windows, macOS e Linux.

Baixar e instalar a versão mais recente do .NET Framework e as versões prévias do macOS e Linux:

|Plataforma|Baixar|Data de liberação|Versão|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2128142)|28 de abril de 2020|18.5|15.0.4769.1|
|.NET Core para macOS |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2128145)|28 de abril de 2020| 18.5|15.0.4769.1|
|.NET Core para Linux |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2128144)|28 de abril de 2020| 18.5|15.0.4769.1|
|.NET Core para Windows |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2128143)|28 de abril de 2020| 18.5|15.0.4769.1|

Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](release-notes-sqlpackage.md). Para baixar idiomas adicionais, confira a seção [Idiomas disponíveis](#available-languages).

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="get-sqlpackage-for-windows"></a>Obter o sqlpackage para Windows

Esta versão do sqlpackage inclui uma experiência padrão do instalador do Windows e um .zip: 

1. Baixe e execute o [instalador DacFramework.msi para Windows](https://go.microsoft.com/fwlink/?linkid=2128142).
2. Abra uma nova janela do prompt de comando e execute sqlpackage.exe
    - O sqlpackage é instalado na pasta ```C:\Program Files\Microsoft SQL Server\150\DAC\bin```

## <a name="get-sqlpackage-net-core-for-windows"></a>Obter o Get sqlpackage .NET Core para Windows

1. Baixe o [sqlpackage para Windows](https://go.microsoft.com/fwlink/?linkid=2128143).
2. Para extrair o arquivo, clique com o botão direito do mouse no arquivo no Windows Explorer, selecione "Extrair tudo…" e então selecione o diretório de destino.
3. Abra uma nova janela de Terminal e CD para a localização em que o SqlPackage foi extraído:

   ```cmd
   > sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-macos"></a>Obter o .NET Core do sqlpackage para macOS

1. Baixe o [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=2128145).
2. Para extrair o arquivo e iniciar o sqlpackage, abra uma nova janela do terminal e digite os seguintes comandos:

   ```bash
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   $ echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   $ source ~/.bash_profile
   $ sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-linux"></a>Obter o .NET Core do sqlpackage para Linux

1. Baixe o [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=2128144) usando um dos instaladores ou arquivos tar.gz:
2. Para extrair o arquivo e iniciar o sqlpackage, abra uma nova janela do terminal e digite os seguintes comandos:

   ```bash
   cd ~
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-linux-<version string>.zip -d ~/sqlpackage 
   $ echo "export PATH=\"\$PATH:$HOME/sqlpackage\"" >> ~/.bashrc
   $ chmod a+x ~/sqlpackage/sqlpackage
   $ source ~/.bashrc
   $ sqlpackage
   ```

   > [!NOTE]
   > No Debian, Redhat e Ubuntu, você pode ter dependências ausentes. Use os seguintes comandos para instalar estas dependências, de acordo com sua versão do Linux:

   **Debian:**

   ```bash
   $ sudo apt-get install libunwind8
   ```

   **Red Hat:**

   ```bash
   $ yum install libunwind
   $ yum install libicu
   ```

   **Ubuntu:**

   ```bash
   $ sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   $ sudo apt-get install libicu52      # for 14.x
   $ sudo apt-get install libicu55      # for 16.x
   $ sudo apt-get install libicu57      # for 17.x
   $ sudo apt-get install libicu60      # for 18.x
   ```

## <a name="uninstall-sqlpackage-preview"></a>Desinstalar o sqlpackage (versão prévia)

Se você instalou o sqlpackage usando o instalador do Windows, desinstale da mesma forma que você remove aplicativos do Windows.

Se você instalou o sqlpackage com um arquivo .zip ou outros arquivos, exclua os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

O sqlpackage é executado no Windows, macOS e Linux, é tem suporte nas plataformas a seguir:

### <a name="windows"></a>Windows

- Windows 10
- Windows 8.1
- Windows 7 SP1
- Windows Server 2008 R2
- Windows Server 2012 R2
- Windows Server 2016

### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="available-languages"></a>Idiomas disponíveis

Esta versão do sqlpackage pode ser instalada nos seguintes idiomas:

sqlpackage Windows:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2128142&clcid=0x40a)

sqlpackage .NET Core Windows:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2128143&clcid=0x40a)

sqlpackage .NET Core macOS:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2128145&clcid=0x40a)

sqlpackage .NET Core Linux:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2128144&clcid=0x40a)

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [sqlpackage](sqlpackage.md)

[Política de Privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
