---
title: Instalar ferramentas de linha de comando do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve como instalar as ferramentas do SQL Server no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: 80bff9787e750e39a0747be831b1fc902d6923a8
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51270169"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Instalar o sqlcmd e bcp ferramentas de linha de comando do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

As etapas a seguir instalam as ferramentas de linha de comando, os drivers ODBC da Microsoft e suas dependências. O **mssql-tools** pacote contém:

- **Sqlcmd**: utilitário de linha de comando de consulta.
- **BCP**: em massa de utilitário de importação / exportação.

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

1. **Opcional**: adicione `/opt/mssql-tools/bin/` para seu **caminho** variável de ambiente em um shell bash.

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

1. **Opcional**: adicione `/opt/mssql-tools/bin/` para seu **caminho** variável de ambiente em um shell bash.

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

1. **Opcional**: adicione `/opt/mssql-tools/bin/` para seu **caminho** variável de ambiente em um shell bash.

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
brew install --no-sandbox mssql-tools
#for silent install: 
#ACCEPT_EULA=y brew install --no-sandbox mssql-tools
```

## <a id="docker"></a> Docker

Ferramentas de linha de comando do SQL Server são incluídas na imagem do Docker. Se você anexar à imagem com um prompt de comando interativo, você pode executar as ferramentas localmente.

## <a name="offline-installation"></a>Instalação offline

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

A tabela a seguir fornece o local para os pacotes de ferramentas mais recentes:

| Pacote de ferramentas | Versão | Download |
|-----|-----|-----|
| Pacote de ferramentas do Red Hat RPM | 14.0.5.0-1 | [pacote RPM MSSQL-tools](https://packages.microsoft.com/rhel/7.3/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Pacote de ferramentas de RPM do SLES | 14.0.5.0-1 | [pacote RPM MSSQL-tools](https://packages.microsoft.com/sles/12/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian o pacote de ferramentas | 14.0.5.0-1 | [pacote de ferramentas de MSSQL Debian](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |
| Pacote de ferramentas Ubuntu 16.10 Debian | 14.0.5.0-1 | [pacote de ferramentas de MSSQL Debian](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |

Esses pacotes dependem **msodbcsql**, que deve ser instalado primeiro. O **msodbcsql** pacote também tem uma dependência nos **unixODBC devel** (RPM) ou **unixodbc-dev** (Debian). O local do **msodbcsql** pacotes são listados na tabela a seguir:

| pacote de msodbcsql | Versão | Download |
|-----|-----|-----|
| Pacote do Red Hat RPM msodbcsql | 13.1.6.0-1 | [pacote RPM msodbcsql](https://packages.microsoft.com/rhel/7.3/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Pacote de msodbcsql SLES RPM | 13.1.6.0-1 | [pacote RPM msodbcsql](https://packages.microsoft.com/sles/12/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Pacote do Ubuntu 16.04 msodbcsql Debian | 13.1.6.0-1 | [pacote de Debian msodbcsql](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |
| Pacote do Ubuntu 16.10 msodbcsql Debian | 13.1.6.0-1 | [pacote de Debian msodbcsql](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |

Para instalar manualmente esses pacotes, use as seguintes etapas:

1. **Mover os pacotes baixados em seu computador Linux**. Se você usou um computador diferente para baixar os pacotes, uma maneira de mover os pacotes para sua máquina Linux é com o **scp** comando.

1. **Instalar os pacotes e**: instalar o **mssql-tools** e **msodbc** pacotes. Se você receber quaisquer erros de dependência, ignorá-las até a próxima etapa.

    | Plataforma | Comandos de instalação do pacote |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo yum localinstall mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | SLES | `sudo zypper install msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo zypper install mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_13.1.6.0-1_amd64.deb`<br/>`sudo dpkg -i mssql-tools_14.0.5.0-1_amd64.deb` |

1. **Resolver dependências ausentes**: você pode ter dependências ausentes no momento. Caso contrário, você pode ignorar esta etapa. Em alguns casos, você deve manualmente localizar e instalar essas dependências.

    Para pacotes RPM, você pode inspecionar as dependências necessárias com os seguintes comandos:

    ```bash
    rpm -qpR msodbcsql-13.1.6.0-1.x86_64.rpm
    rpm -qpR mssql-tools-14.0.5.0-1.x86_64.rpm
    ```

    Para pacotes Debian, se você tiver acesso a repositórios aprovados que contém essas dependências, a solução mais fácil é usar o **apt-get** comando:

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > Este comando conclui a instalação dos pacotes do SQL Server.

    Se isso não funcionar para seu pacote Debian, você pode inspecionar as dependências necessárias com os seguintes comandos:

    ```bash
    dpkg -I msodbcsql_13.1.6.0-1_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_14.0.5.0-1_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>Próximas etapas

Para obter um exemplo de como usar **sqlcmd** para se conectar ao SQL Server e criar um banco de dados, consulte um dos seguintes inícios rápidos:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)

Para obter um exemplo de como usar **bcp** para importação e exportação em massa dados, consulte [dados de cópia em massa para o SQL Server no Linux](sql-server-linux-migrate-bcp.md).
