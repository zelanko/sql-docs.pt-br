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
ms.reviewer: drskwier; sstein
ms.date: 10/02/2020
ms.openlocfilehash: 1a722b41576136bdcc509c96626f8cf4351629e4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721577"
---
# <a name="download-and-install-sqlpackage"></a>Baixar e instalar o sqlpackage

O sqlpackage é executado no Windows, macOS e Linux.

Baixar e instalar a versão mais recente do .NET Framework e as versões prévias do macOS e Linux:

|Plataforma|Baixar|Data de liberação|Versão|Build
|:---|:---|:---|:---|:---|
|[Windows](#get-sqlpackage-for-windows)|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2143544)|18 de setembro de 2020| 18.6 | 15.0.4897.1 |
|[.NET Core para macOS](#get-sqlpackage-net-core-for-macos) |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2143659)|18 de setembro de 2020| 18.6| 15.0.4897.1 |
|[.NET Core para Linux](#get-sqlpackage-net-core-for-linux) |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2143497)|18 de setembro de 2020| 18.6| 15.0.4897.1 |
|[.NET Core para Windows](#get-sqlpackage-net-core-for-windows) |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2143496)|18 de setembro de 2020| 18.6| 15.0.4897.1 |

Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](release-notes-sqlpackage.md). Para baixar idiomas adicionais, confira a seção [Idiomas disponíveis](#available-languages).

## <a name="dacfx"></a>DacFx
O DacServices ([Microsoft.SqlServer.Dac](https://docs.microsoft.com/dotnet/api/microsoft.sqlserver.dac.dacservices)) é um mecanismo relacionado para integrar a implantação de banco de dados no seu pipeline de aplicativo.  A API do DacServices está disponível em um pacote por meio do nuget [Microsoft.SqlServer.DACFx](https://www.nuget.org/packages/Microsoft.SqlServer.DACFx).  A versão atual do DacFx é 150.4897.1.

A instalação do pacote nuget por meio da CLI do .NET é realizada com este comando:

```cmd
> dotnet add package Microsoft.SqlServer.DACFx
```

>[!NOTE]
> Pacotes nuget adicionais foram publicados com o nome DacFx, "Microsoft.SqlServer.DacFx.x64" e "Microsoft.SqlServer.DacFx.x86". O suporte para ambas as plataformas é abordado no pacote "Microsoft.SqlServer.DACFx". Novas referências devem ser feitas neste pacote e não nas variantes x64 ou x86.

## <a name="get-sqlpackage-for-windows"></a>Obter o sqlpackage para Windows

Esta versão do sqlpackage inclui uma experiência padrão do instalador do Windows e um .zip: 

1. Baixe e execute o [instalador DacFramework.msi para Windows](https://go.microsoft.com/fwlink/?linkid=2143544).
2. Abra uma nova janela do prompt de comando e execute sqlpackage.exe
    - O sqlpackage é instalado na pasta ```C:\Program Files\Microsoft SQL Server\150\DAC\bin```

## <a name="get-sqlpackage-net-core-for-windows"></a>Obter o Get sqlpackage .NET Core para Windows

1. Baixe o [sqlpackage para Windows](https://go.microsoft.com/fwlink/?linkid=2143496).
2. Para extrair o arquivo, clique com o botão direito do mouse no arquivo no Windows Explorer, selecione "Extrair tudo…" e então selecione o diretório de destino.
3. Abra uma nova janela de Terminal e CD para a localização em que o SqlPackage foi extraído:

   ```cmd
   > sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-macos"></a>Obter o .NET Core do sqlpackage para macOS

1. Baixe o [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=2143659).
2. Para extrair o arquivo e iniciar o sqlpackage, abra uma nova janela do terminal e digite os seguintes comandos:

   ```bash
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-osx-<version string>.zip -d ~/sqlpackage 
   $ echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   $ source ~/.bash_profile
   $ sqlpackage
   ```

   > [!NOTE]
   > As configurações de segurança podem exigir modificações para executar o sqlpackage no macOS. Use os comandos a seguir para interagir com o Gatekeeper usando a linha de comando.

   **Antes de executar sqlpackage:**
   ```bash
   $ sudo spctl --master-disable
   ```

   **Depois de executar sqlpackage:**
   ```bash
   $ sudo spctl --master-enable
   ```

## <a name="get-sqlpackage-net-core-for-linux"></a>Obter o .NET Core do sqlpackage para Linux

1. Baixe o [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=2143497) usando um dos instaladores ou arquivos tar.gz:
2. Para extrair o arquivo e iniciar o sqlpackage, abra uma nova janela do terminal e digite os seguintes comandos:

   ```bash
   $ cd ~
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

## <a name="uninstall-sqlpackage"></a>Desinstalar o sqlpackage

Se você instalou o sqlpackage usando o instalador do Windows, desinstale da mesma forma que você remove aplicativos do Windows.

Se você instalou o sqlpackage com um arquivo .zip ou outros arquivos, exclua os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

O sqlpackage é executado no Windows, no macOS e no Linux, além de ser criado usando o .NET Core 3.1.  Os [requisitos do sistema operacional do .NET Core 3.1](https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md) se aplicam ao sqlpackage.

### <a name="windows-x64"></a>Windows (x64)

- Windows 10 (1607+)
- Windows 8.1
- Windows 7 SP1
- Núcleo do Windows Server
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2019

### <a name="macos"></a>macOS

- macOS 10.15 "Catalina"
- macOS 10.14 "Mojave"
- macOS 10.13 "High Sierra"

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7+
- SUSE Linux Enterprise Server v12 SP2+
- Ubuntu 16.04+

## <a name="available-languages"></a>Idiomas disponíveis

Esta versão do sqlpackage pode ser instalada nos seguintes idiomas:

sqlpackage Windows:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2143544&clcid=0x40a)

sqlpackage .NET Core Windows:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2143496&clcid=0x40a)

sqlpackage .NET Core macOS:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2143659&clcid=0x40a)

sqlpackage .NET Core Linux:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2143497&clcid=0x40a)


## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [sqlpackage](sqlpackage.md)

[Política de Privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
