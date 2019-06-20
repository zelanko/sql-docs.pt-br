---
title: Instalar ferramentas de linha de comando do SQL Server no Linux
titleSuffix: SQL Server
description: Este artigo descreve como instalar as ferramentas do SQL Server no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/07/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: d6e10c384d799ee416facee150e5e2318b381ea6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66810273"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Instalar o sqlcmd e bcp ferramentas de linha de comando do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

As etapas a seguir instalam as ferramentas de linha de comando, os drivers ODBC da Microsoft e suas dependências. O **mssql-tools** pacote contém:

- **sqlcmd**: Utilitário de linha de comando de consulta.
- **bcp**: Utilitário de importação / exportação em massa.

Instale as ferramentas para sua plataforma:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

Este artigo descreve como instalar as ferramentas de linha de comando. Se você estiver procurando por exemplos de como usar **sqlcmd** ou **bcp**, consulte a [links](#next-steps) no final deste tópico.

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>Instalar as ferramentas em RHEL 7

Use as etapas a seguir para instalar o **mssql-tools** no Red Hat Enterprise Linux. 

1. Entre no modo de superusuário.

   ```bash
   sudo su
   ```

1. Baixe o arquivo de configuração do repositório Microsoft Red Hat.

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. Sair do modo de superusuário.

   ```bash
   exit
   ```

1. Se você tiver uma versão anterior do **mssql-tools** instalado, remova quaisquer pacotes mais antigos do unixODBC.

   ```bash
   sudo yum remove mssql-tools unixODBC-utf16-devel
   ```

1. Execute os seguintes comandos para instalar **mssql-tools** com o pacote de desenvolvedor do unixODBC.

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Para atualizar para a versão mais recente do **mssql-tools** execute os seguintes comandos:
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **Opcional**: Adicione `/opt/mssql-tools/bin/` para seu **caminho** variável de ambiente em um shell bash.

   Para tornar **sqlcmd/bcp** acessível do shell bash para sessões de logon, modificar sua **caminho** no **~/.bash_profile** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para tornar **sqlcmd/bcp** acessível a partir do shell bash para sessões interativas/não logon, modificar o **caminho** no **~/.bashrc** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="ubuntu"></a>Instalar as ferramentas no Ubuntu 16.04

Use as etapas a seguir para instalar o **mssql-tools** no Ubuntu. 

1. Importe as chaves GPG repositório público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre o repositório Microsoft Ubuntu.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. Atualize a lista de fontes e execute o comando de instalação com o pacote de desenvolvedor do unixODBC.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > Para atualizar para a versão mais recente do **mssql-tools** execute os seguintes comandos:
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **Opcional**: Adicione `/opt/mssql-tools/bin/` para seu **caminho** variável de ambiente em um shell bash.

   Para tornar **sqlcmd/bcp** acessível do shell bash para sessões de logon, modificar sua **caminho** no **~/.bash_profile** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para tornar **sqlcmd/bcp** acessível a partir do shell bash para sessões interativas/não logon, modificar o **caminho** no **~/.bashrc** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="SLES"></a>Instalar as ferramentas no SLES 12

Use as etapas a seguir para instalar o **mssql-tools** no SUSE Linux Enterprise Server. 

1. Adicione o repositório do Microsoft SQL Server para o Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Instale **mssql-tools** com o pacote de desenvolvedor do unixODBC.

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Para atualizar para a versão mais recente do **mssql-tools** execute os seguintes comandos:
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **Opcional**: Adicione `/opt/mssql-tools/bin/` para seu **caminho** variável de ambiente em um shell bash.

   Para tornar **sqlcmd/bcp** acessível do shell bash para sessões de logon, modificar sua **caminho** no **~/.bash_profile** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para tornar **sqlcmd/bcp** acessível a partir do shell bash para sessões interativas/não logon, modificar o **caminho** no **~/.bashrc** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="macos"></a> Instalar as ferramentas no macOS

Uma visualização da **sqlcmd** e **bcp** agora está disponível no macOS. Para obter mais informações, consulte o [comunicado](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/).

*Instale [Homebrew](https://brew.sh) se você ainda não o tiver:*

        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Para instalar as ferramentas para Mac El Capitan e Serra, use os seguintes comandos:

```
# brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install mssql-tools
#for silent install: 
#HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=y brew install mssql-tools
```

## <a id="docker"></a> Docker

Ferramentas de linha de comando do SQL Server são incluídas na imagem do Docker. Se você anexar à imagem com um prompt de comando interativo, você pode executar as ferramentas localmente.

## <a name="offline-installation"></a>Instalação offline

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

1. Primeiro, localize e copie as **mssql-tools** pacote para a sua distribuição do Linux:

   | Distribuição do Linux | **ferramentas de MSSQL** local do pacote |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools) |

1. Também, localize e copie as **msodbcsql** pacote, que é uma dependência. O **msodbcsql** pacote também tem uma dependência nos **unixODBC devel** (Red Hat e SLES) ou **unixodbc-dev** (Ubuntu). O local do **msodbcsql** pacotes são listados na tabela a seguir:

   | Distribuição do Linux | Local de pacotes do ODBC |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [**msodbcsql**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql)<br/>[**unixodbc-dev**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/u/unixodbc/) |

1. **Mover os pacotes baixados em seu computador Linux**. Se você usou um computador diferente para baixar os pacotes, uma maneira de mover os pacotes para sua máquina Linux é com o **scp** comando.

1. **Instalar os pacotes e**: Instalar o **mssql-tools** e **msodbc** pacotes. Se você receber quaisquer erros de dependência, ignorá-las até a próxima etapa.

    | Plataforma | Comandos de instalação do pacote |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-<version>.rpm`<br/>`sudo yum localinstall mssql-tools-<version>.rpm` |
    | SLES | `sudo zypper install msodbcsql-<version>.rpm`<br/>`sudo zypper install mssql-tools-<version>.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_<version>.deb`<br/>`sudo dpkg -i mssql-tools_<version>.deb` |

1. **Resolver dependências ausentes**: Você pode ter dependências ausentes no momento. Caso contrário, você pode ignorar esta etapa. Em alguns casos, você deve manualmente localizar e instalar essas dependências.

    Para pacotes RPM, você pode inspecionar as dependências necessárias com os seguintes comandos:

    ```bash
    rpm -qpR msodbcsql-<version>.rpm
    rpm -qpR mssql-tools-<version>.rpm
    ```

    Para pacotes Debian, se você tiver acesso a repositórios aprovados que contém essas dependências, a solução mais fácil é usar o **apt-get** comando:

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > Este comando conclui a instalação dos pacotes do SQL Server.

    Se isso não funcionar para seu pacote Debian, você pode inspecionar as dependências necessárias com os seguintes comandos:

    ```bash
    dpkg -I msodbcsql_<version>_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_<version>_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>Próximas etapas

Para obter um exemplo de como usar **sqlcmd** para se conectar ao SQL Server e criar um banco de dados, consulte um dos seguintes inícios rápidos:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)

Para obter um exemplo de como usar **bcp** para importação e exportação em massa dados, consulte [dados de cópia em massa para o SQL Server no Linux](sql-server-linux-migrate-bcp.md).
