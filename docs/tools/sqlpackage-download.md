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
ms.openlocfilehash: f966de4951e5c90dac8d6e48f00f8de6ff067e3c
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73033007"
---
# <a name="download-and-install-sqlpackage"></a>Baixar e instalar o sqlpackage

O sqlpackage é executado no Windows, macOS e Linux.

Baixar e instalar a versão mais recente do .NET Framework e as versões prévias do macOS e Linux:

|Plataforma|Download|Data de liberação|Versão|Compilação
|:---|:---|:---|:---|:---|
|Windows (x64)|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2108813)|29 de outubro de 2019|18.4|15.0.4573.2|
|macOS .NET Core (x64)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2108815)|29 de outubro de 2019| 18.4|15.0.4573.2|
|Linux .NET Core (x64) |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2108814)|29 de outubro de 2019| 18.4|15.0.4573.2|
|Windows .NET Core (x64) |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2109019)|29 de outubro de 2019| 18.4|15.0.4573.2|

Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](release-notes-sqlpackage.md). Para baixar idiomas adicionais, consulte a seção [idiomas disponíveis](#available-languages) .

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="get-sqlpackage-for-windows"></a>Obter o sqlpackage para Windows

Esta versão do sqlpackage inclui uma experiência padrão do instalador do Windows e um .zip: 

1. Baixe e execute o [instalador DacFramework.msi para Windows](https://go.microsoft.com/fwlink/?linkid=2108813).
2. Abra uma nova janela do prompt de comando e execute sqlpackage.exe
    - O sqlpackage é instalado na pasta ```C:\Program Files\Microsoft SQL Server\150\DAC\bin```

## <a name="get-sqlpackage-net-core-for-windows"></a>Obter o .NET Core do SqlPackage para Windows

1. Baixe o [sqlpackage para Windows](https://go.microsoft.com/fwlink/?linkid=2109019).
2. Para extrair o arquivo clicando com o botão direito do mouse no arquivo no Windows Explorer e selecionando ' extrair tudo... ' e selecione o diretório de destino.
3. Abra uma nova janela de terminal e CD para o local em que SqlPackage foi extraído:

   ```cmd
   > sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-macos"></a>Obter o .NET Core do SqlPackage para macOS

1. Baixe o [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=2108815).
2. Para extrair o arquivo e iniciar o sqlpackage, abra uma nova janela do terminal e digite os seguintes comandos:

   ```bash
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   $ echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   $ source ~/.bash_profile
   $ sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-linux"></a>Obter o .NET Core do SqlPackage para Linux

1. Baixe o [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=2108814) usando um dos instaladores ou arquivos tar.gz:
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

Janelas SqlPackage:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x40a)

Janelas do .NET Core do SqlPackage:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x40a)

SqlPackage .NET Core macOS:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x40a)

SqlPackage .NET Core Linux:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x40a)

## <a name="next-steps"></a>Next Steps

- Saiba mais sobre o [sqlpackage](sqlpackage.md)

[Política de Privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
