---
title: 'Ubuntu: Instalar o SQL Server em Linux'
description: Este início rápido mostra como instalar o SQL Server 2017 ou o SQL Server 2019 no Ubuntu e criar e consultar um banco de dados com sqlcmd.
author: VanMSFT
ms.author: vanto
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.custom: seo-lt-2019
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 69f1ac170d70c10d9a7061b3fc18f6c8a62db704
ms.sourcegitcommit: efb2bb07700f645b3fbfcb400a0666de01388305
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79319846"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>Início Rápido: Instalar o SQL Server e criar um banco de dados no Ubuntu
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]


<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Neste início rápido, você instalará o SQL Server 2017 no Ubuntu 16.04. Em seguida, você se conecta ao **sqlcmd** parar criar seu primeiro banco de dados e executar consultas.

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Neste início rápido, você instalará o SQL Server 2019 no Ubuntu 18.04. Em seguida, você se conecta ao **sqlcmd** parar criar seu primeiro banco de dados e executar consultas.

::: moniker-end

> [!TIP]
> Este tutorial requer a entrada do usuário e uma conexão com a Internet. Se estiver interessado nos procedimentos de instalação autônoma ou offline, confira [Diretrizes de instalação para o SQL Server em Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Pré-requisitos

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

É necessário ter um computador Ubuntu 16.04 com **pelo menos 2 GB** de memória.

Para instalar o Ubuntu 16.04 em seu próprio computador, acesse <http://releases.ubuntu.com/xenial/>. Também é possível criar máquinas virtuais Ubuntu no Azure. Confira [Criar e gerenciar VMs do Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> Neste momento, não há suporte para o [Subsistema do Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 como um destino de instalação.

Para obter outros requisitos do sistema, confira [Requisitos do sistema do SQL Server em Linux](sql-server-linux-setup.md#system).

> [!NOTE]
> Ainda não há suporte oficial ao Ubuntu 18.04, mas a execução do SQL Server é possível com [modificações](https://blogs.msdn.microsoft.com/sql_server_team/installing-sql-server-2017-for-linux-on-ubuntu-18-04-lts/).

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

É necessário ter um computador Ubuntu 18.04 com **pelo menos 2 GB** de memória.

Para instalar o Ubuntu 18.04 em seu próprio computador, acesse <http://releases.ubuntu.com/bionic/>. Também é possível criar máquinas virtuais Ubuntu no Azure. Confira [Criar e gerenciar VMs do Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> Neste momento, não há suporte para o [Subsistema do Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 como um destino de instalação.

Para obter outros requisitos do sistema, confira [Requisitos do sistema do SQL Server em Linux](sql-server-linux-setup.md#system).

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server no Ubuntu, execute os seguintes comandos em um terminal para instalar o pacote **mssql-server**.

1. Importe as chaves GPG do repositório público:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registre o repositório do Ubuntu do Microsoft SQL Server:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > Se quiser instalar o SQL Server 2019, você precisará registrar o repositório do SQL Server 2019. Use o seguinte comando para a instalações do SQL Server 2019:
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   > ```

3. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. Após a conclusão da instalação do pacote, execute a **instalação de mssql-conf** e siga os prompts para definir a senha SA e escolher sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > As seguintes edições do SQL Server 2017 são licenciadas gratuitamente: Evaluation, Developer e Express.

   > [!NOTE]
   > Especifique uma senha forte para a conta SA (comprimento mínimo de 8 caracteres, incluindo letras maiúsculas e minúsculas, 10 dígitos básicos e/ou símbolos não alfanuméricos).

5. Após concluir a configuração, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. Se planeja se conectar remotamente, talvez seja preciso abrir a porta TCP do SQL Server (padrão 1433) em seu firewall.

Neste momento, o SQL Server está em execução no seu computador Ubuntu e está pronto para uso!

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server no Ubuntu, execute os seguintes comandos em um terminal para instalar o pacote **mssql-server**.

1. Importe as chaves GPG do repositório público:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registre o repositório do Ubuntu do Microsoft SQL Server para o SQL Server 2019:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
   ```

3. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. Após a conclusão da instalação do pacote, execute a **instalação de mssql-conf** e siga os prompts para definir a senha SA e escolher sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Especifique uma senha forte para a conta SA (comprimento mínimo de 8 caracteres, incluindo letras maiúsculas e minúsculas, 10 dígitos básicos e/ou símbolos não alfanuméricos).

5. Após concluir a configuração, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. Se planeja se conectar remotamente, talvez seja preciso abrir a porta TCP do SQL Server (padrão 1433) em seu firewall.

Neste momento, o SQL Server 2019 está em execução no seu computador Ubuntu e está pronto para uso!

::: moniker-end

## <a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Para criar um banco de dados, é necessário conectar-se a uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As seguintes etapas instalam as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

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

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Para criar um banco de dados, é necessário conectar-se a uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As seguintes etapas instalam as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

Use as etapas a seguir para instalar o **mssql-tools** no Ubuntu. 

1. Importe as chaves GPG do repositório público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre o repositório do Microsoft Ubuntu.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
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

::: moniker-end

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
