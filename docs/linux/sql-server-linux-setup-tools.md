---
title: Instalar as ferramentas de linha de comando do SQL Server no Linux
titleSuffix: SQL Server
description: Este artigo descreve como instalar as Ferramentas do SQL Server no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 06/07/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: 056110966ece8e344320b73890dbead9d513230b
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68085719"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Instalar sqlcmd e bcp, as ferramentas de linha de comando do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

As etapas a seguir instalam as ferramentas de linha de comando, os drivers ODBC da Microsoft e as dependências deles. O pacote **mssql-tools** contém:

- **sqlcmd**: utilitário de consulta de linha de comando.
- **bcp**: utilitário de importação/exportação em massa.

Instale as ferramentas para a plataforma:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

Este artigo descreve como instalar as ferramentas de linha de comando. Se você estiver procurando exemplos de como usar o **sqlcmd** ou o **bcp**, confira os [links](#next-steps) no final deste tópico.

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>Instalar ferramentas no RHEL 7

Use as seguintes etapas a seguir para instalar o **mssql-tools** no Red Hat Enterprise Linux. 

1. Entre no modo de superusuário.

   ```bash
   sudo su
   ```

1. Baixe o arquivo de configuração do repositório do Red Hat da Microsoft.

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. Saia do modo de superusuário.

   ```bash
   exit
   ```

1. Se você tiver uma versão anterior do **mssql-tools** instalada, remova os pacotes unixODBC mais antigos.

   ```bash
   sudo yum remove mssql-tools unixODBC-utf16-devel
   ```

1. Execute os seguintes comandos para instalar **mssql-tools** com o pacote do desenvolvedor do unixODBC.

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Para atualizar para a versão mais recente do **mssql-tools**, execute os seguintes comandos:
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **Opcional**: Adicione `/opt/mssql-tools/bin/` à sua variável de ambiente **PATH** em um shell de Bash.

   Para tornar o **sqlcmd/bcp** acessível do shell de Bash para sessões de logon, modifique o **PATH** no arquivo **~/.bash_profile** com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para tornar o **sqlcmd/bcp** acessível do shell de Bash para sessões interativas/que não são de logon, modifique o **PATH** no arquivo **~/.bashrc** com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="ubuntu"></a>Instalar ferramentas no Ubuntu 16.04

Use as etapas a seguir para instalar o **mssql-tools** no Ubuntu. 

1. Importe as chaves GPG do repositório público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre o repositório do Microsoft Ubuntu.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. Atualize a lista de fontes e execute o comando de instalação com o pacote do desenvolvedor do unixODBC.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > Para atualizar para a versão mais recente do **mssql-tools**, execute os seguintes comandos:
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **Opcional**: Adicione `/opt/mssql-tools/bin/` à sua variável de ambiente **PATH** em um shell de Bash.

   Para tornar o **sqlcmd/bcp** acessível do shell de Bash para sessões de logon, modifique o **PATH** no arquivo **~/.bash_profile** com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para tornar o **sqlcmd/bcp** acessível do shell de Bash para sessões interativas/que não são de logon, modifique o **PATH** no arquivo **~/.bashrc** com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="SLES"></a>Instalar ferramentas no SLES 12

Use as seguintes etapas para instalar o **mssql-tools** no SUSE Linux Enterprise Server. 

1. Adicione o repositório do Microsoft SQL Server ao Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Instale o **mssql-tools** com o pacote do desenvolvedor unixODBC.

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Para atualizar para a versão mais recente do **mssql-tools**, execute os seguintes comandos:
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **Opcional**: Adicione `/opt/mssql-tools/bin/` à sua variável de ambiente **PATH** em um shell de Bash.

   Para tornar o **sqlcmd/bcp** acessível do shell de Bash para sessões de logon, modifique o **PATH** no arquivo **~/.bash_profile** com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para tornar o **sqlcmd/bcp** acessível do shell de Bash para sessões interativas/que não são de logon, modifique o **PATH** no arquivo **~/.bashrc** com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="macos"></a> Instalar ferramentas no macOS

Uma versão prévia do **sqlcmd** e do **bcp** está agora disponível no macOS. Para obter mais informações, confira o [comunicado](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/).

*Instale o [Homebrew](https://brew.sh) se você ainda não o tiver:*

        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Para instalar as ferramentas El Capitan e Sierra para Mac, use os seguintes comandos:

```
# brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install mssql-tools
#for silent install: 
#HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=y brew install mssql-tools
```

## <a id="docker"></a> Docker

As ferramentas de linha de comando do SQL Server estão incluídas na imagem do Docker. Se você anexar a imagem com um prompt de comando interativo, poderá executar as ferramentas localmente.

## <a name="offline-installation"></a>Instalação offline

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

1. Primeiro, localize e copie o pacote **mssql-tools** para sua distribuição do Linux:

   | Distribuição do Linux | Localização do pacote **mssql-tools** |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools) |

1. Além disso, localize e copie o pacote **msodbcsql**, que é uma dependência. O pacote **msodbcsql** também tem uma dependência em **unixODBC-devel** (Red Hat e SLES) ou **unixodbc-dev** (Ubuntu). A localização dos pacotes **msodbcsql** está listada na tabela a seguir:

   | Distribuição do Linux | Localização dos pacotes ODBC |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [**msodbcsql**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql)<br/>[**unixodbc-dev**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/u/unixodbc/) |

1. **Mova os pacotes baixados para o computador Linux**. Se você usou um computador diferente para baixar os pacotes, uma maneira de mover os pacotes para o computador Linux é com o comando **scp**.

1. **Instalar os pacotes mssql-tools e msodbc**: Instale os pacotes **mssql-tools** e **msodbc**. Se você obtiver erros de dependência, ignore-os até a próxima etapa.

    | Plataforma | Comandos de instalação de pacote |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-<version>.rpm`<br/>`sudo yum localinstall mssql-tools-<version>.rpm` |
    | SLES | `sudo zypper install msodbcsql-<version>.rpm`<br/>`sudo zypper install mssql-tools-<version>.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_<version>.deb`<br/>`sudo dpkg -i mssql-tools_<version>.deb` |

1. **Resolver dependências ausentes**: Você pode ter dependências ausentes neste momento. Caso contrário, você pode ignorar esta etapa. Em alguns casos, você deve localizar essas dependências manualmente e instalá-las.

    Para pacotes RPM, você pode inspecionar as dependências necessárias com os seguintes comandos:

    ```bash
    rpm -qpR msodbcsql-<version>.rpm
    rpm -qpR mssql-tools-<version>.rpm
    ```

    Para pacotes Debian, se você tiver acesso a repositórios aprovados que contenham essas dependências, a solução mais fácil será usar o comando **apt-get**:

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > Esse comando também conclui a instalação dos pacotes do SQL Server.

    Se isso não funcionar para o pacote do Debian, você poderá inspecionar as dependências necessárias com os seguintes comandos:

    ```bash
    dpkg -I msodbcsql_<version>_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_<version>_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>Próximas etapas

Para obter um exemplo de como usar o **sqlcmd** para se conectar ao SQL Server e criar um banco de dados, confira um dos seguintes inícios rápidos:

- [Instalação no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalação no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)

Para obter um exemplo de como usar o **bcp** para importar e exportar dados em massa, confira [Copiar dados em massa para o SQL Server em Linux](sql-server-linux-migrate-bcp.md).
