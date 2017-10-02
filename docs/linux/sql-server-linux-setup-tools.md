---
title: Instalar ferramentas de linha de comando do SQL Server no Linux | Microsoft Docs
description: "Este tópico descreve como instalar as ferramentas do SQL Server no Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 130da2409070f0acfda0bf78fcf2c4326bbeec92
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Instalar as ferramentas de linha de comando do SQL Server de sqlcmd e bcp em Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

As etapas a seguir instalar as ferramentas de linha de comando, drivers de ODBC da Microsoft e suas dependências. O **mssql ferramentas** pacote contém:

- **Sqlcmd**: utilitário de linha de comando de consulta.
- **BCP**: utilitário de importação-exportação em massa de.

Instale as ferramentas para a sua plataforma:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

Este tópico descreve como instalar as ferramentas de linha de comando. Se você estiver procurando por exemplos de como usar **sqlcmd** ou **bcp**, consulte o [links](#next-steps) no final deste tópico.

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>Instalar as ferramentas em RHEL 7

Use as etapas a seguir para instalar o **mssql ferramentas** no Red Hat Enterprise Linux. 

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

1. Se você tiver uma versão anterior do **mssql ferramentas** instalado, remova quaisquer pacotes de unixODBC mais antigos.

   ```bash
   sudo yum update
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Execute os seguintes comandos para instalar **mssql ferramentas** com o pacote do desenvolvedor unixODBC.

   ```bash
   sudo yum update
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Para atualizar para a versão mais recente do **mssql ferramentas** execute os seguintes comandos:
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **Opcional**: adicionar `/opt/mssql-tools/bin/` para sua **caminho** variável de ambiente em um shell bash.

   Para fazer **sqlcmd/bcp** acessível no shell bash para sessões de logon, modificar o **caminho** no **~/.bash_profile** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para fazer **sqlcmd/bcp** acessível no shell bash para sessões/não-logon interativo, modifique o **caminho** no **~/.bashrc** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="ubuntu"></a>Instalar ferramentas no Ubuntu 16.04

Use as etapas a seguir para instalar o **mssql ferramentas** no Ubuntu. 

1. Importe as chaves GPG repositório público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre o repositório Microsoft Ubuntu.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. Atualizar a lista de fontes e execute o comando de instalação com o pacote do desenvolvedor unixODBC.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > Para atualizar para a versão mais recente do **mssql ferramentas** execute os seguintes comandos:
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **Opcional**: adicionar `/opt/mssql-tools/bin/` para sua **caminho** variável de ambiente em um shell bash.

   Para fazer **sqlcmd/bcp** acessível no shell bash para sessões de logon, modificar o **caminho** no **~/.bash_profile** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para fazer **sqlcmd/bcp** acessível no shell bash para sessões/não-logon interativo, modifique o **caminho** no **~/.bashrc** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="SLES"></a>Instalar as ferramentas em 12 SLES

Use as etapas a seguir para instalar o **mssql ferramentas** no SUSE Linux Enterprise Server. 

1. Adicione repositório do Microsoft SQL Server para Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Instalar **mssql ferramentas** com o pacote do desenvolvedor unixODBC.

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Para atualizar para a versão mais recente do **mssql ferramentas** execute os seguintes comandos:
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **Opcional**: adicionar `/opt/mssql-tools/bin/` para sua **caminho** variável de ambiente em um shell bash.

   Para fazer **sqlcmd/bcp** acessível no shell bash para sessões de logon, modificar o **caminho** no **~/.bash_profile** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Para fazer **sqlcmd/bcp** acessível no shell bash para sessões/não-logon interativo, modifique o **caminho** no **~/.bashrc** arquivo com o seguinte comando:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="macos"></a>Instalar as ferramentas em macOS

Uma visualização de **sqlcmd** e **bcp** agora está disponível em macOS. Para obter mais informações, consulte o [comunicado](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/).

Para instalar as ferramentas para Mac El Capitan e Serra, use os seguintes comandos:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
#brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox mssql-tools
#for silent install: 
#ACCEPT_EULA=y brew install --no-sandbox mssql-tools
```

## <a id="docker"></a>Docker

A partir do SQL Server de 2017 CTP 2.0, as ferramentas de linha de comando do SQL Server são incluídas na imagem do Docker. Se você anexar a imagem com um prompt de comando interativo, você pode executar as ferramentas localmente.

## <a name="offline-installation"></a>Instalação offline

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

A tabela a seguir fornece o local para os pacotes de ferramentas mais recentes:

| Pacote de ferramentas | Versão | Download |
|-----|-----|-----|
| Pacote de ferramentas do Red Hat RPM | 14.0.5.0-1 | [pacote RPM MSSQL ferramentas](https://packages.microsoft.com/rhel/7.3/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Pacote de ferramentas de RPM SLES | 14.0.5.0-1 | [pacote RPM MSSQL ferramentas](https://packages.microsoft.com/sles/12/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian o pacote de ferramentas | 14.0.5.0-1 | [pacote Debian MSSQL ferramentas](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |
| Ubuntu 16.10 Debian o pacote de ferramentas | 14.0.5.0-1 | [pacote Debian MSSQL ferramentas](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |

Esses pacotes dependem **msodbcsql**, que deve ser instalado primeiro. O **msodbcsql** pacote também tem uma dependência no **unixODBC devel** (RPM) ou **unixodbc-dev** (Debian). O local do **msodbcsql** pacotes são listados na tabela a seguir:

| pacote de msodbcsql | Versão | Download |
|-----|-----|-----|
| Pacote do Red Hat RPM msodbcsql | 13.1.6.0-1 | [pacote RPM msodbcsql](https://packages.microsoft.com/rhel/7.3/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Pacote de msodbcsql SLES RPM | 13.1.6.0-1 | [pacote RPM msodbcsql](https://packages.microsoft.com/sles/12/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Ubuntu 16.04 salvou Debian pacote | 13.1.6.0-1 | [pacote Debian salvou](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |
| Ubuntu 16.10 salvou Debian pacote | 13.1.6.0-1 | [pacote Debian salvou](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |

Para instalar manualmente esses pacotes, use as seguintes etapas:

1. **Mover os pacotes baixados para o computador Linux**. Se você usou uma máquina diferente para baixar os pacotes, uma maneira de mover os pacotes para o computador Linux é com o **scp** comando.

1. **Instalar os pacotes e**: instalar o **mssql ferramentas** e **msodbc** pacotes. Se você obtiver erros de dependência, ignorá-las até a próxima etapa.

    | Plataforma | Comandos de instalação do pacote |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo yum localinstall mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | SLES | `sudo zypper install msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo zypper install mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_13.1.6.0-1_amd64.deb`<br/>`sudo dpkg -i mssql-tools_14.0.5.0-1_amd64.deb` |

1. **Resolver dependências ausentes**: você pode ter dependências ausentes neste momento. Caso contrário, você pode ignorar esta etapa. Em alguns casos, você deve manualmente localizar e instalar essas dependências.

    Para pacotes RPM, você pode inspecionar as dependências necessárias com os seguintes comandos:

    ```bash
    rpm -qpR msodbcsql-13.1.6.0-1.x86_64.rpm
    rpm -qpR mssql-tools-14.0.5.0-1.x86_64.rpm
    ```

    Para pacotes Debian, se você tem acesso a repositórios aprovados que contém essas dependências, a solução mais fácil é usar o **apt get** comando:

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

Para obter um exemplo de como usar **sqlcmd** para se conectar ao SQL Server e criar um banco de dados, consulte uma da seguir rápida iniciar tutoriais:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)

Para obter um exemplo de como usar **bcp** para importação e exportação em massa dados, consulte [dados de cópia em massa para o SQL Server no Linux](sql-server-linux-migrate-bcp.md).

