---
title: 'Ubuntu: Instalar o SQL Server em Linux'
description: Este início rápido mostra como instalar o SQL Server 2017 ou o SQL Server 2019 no Ubuntu e criar e consultar um banco de dados com sqlcmd.
author: VanMSFT
ms.author: vanto
ms.date: 07/15/2020
ms.topic: conceptual
ms.prod: sql
ms.custom: seo-lt-2019
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: cce5af380f3706ef6fd6f22578c2b693aff1ad7c
ms.sourcegitcommit: 56f6892b3795da308d226d4b3c5c859ead2e830a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86438108"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>Início Rápido: Instalar o SQL Server e criar um banco de dados no Ubuntu
[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]


<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Neste início rápido, você instalará o SQL Server 2017 no Ubuntu 18.04. Em seguida, você se conecta ao **sqlcmd** parar criar seu primeiro banco de dados e executar consultas.

> [!TIP]
> Este tutorial requer a entrada do usuário e uma conexão com a Internet. Se estiver interessado nos procedimentos de instalação autônoma ou offline, confira [Diretrizes de instalação para o SQL Server em Linux](sql-server-linux-setup.md). Para ver uma lista das plataformas com suporte, confira nossas [Notas sobre a versão](sql-server-linux-release-notes.md).

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Neste início rápido, você instalará o SQL Server 2019 no Ubuntu 18.04. Em seguida, você se conecta ao **sqlcmd** parar criar seu primeiro banco de dados e executar consultas.

> [!TIP]
> Este tutorial requer a entrada do usuário e uma conexão com a Internet. Se estiver interessado nos procedimentos de instalação autônoma ou offline, confira [Diretrizes de instalação para o SQL Server em Linux](sql-server-linux-setup.md). Para ver uma lista das plataformas com suporte, confira nossas [Notas sobre a versão](sql-server-linux-release-notes-2019.md).

::: moniker-end

## <a name="prerequisites"></a>Pré-requisitos

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

É necessário ter um computador Ubuntu 16.04 ou 18.04 com **pelo menos 2 GB** de memória.

Para instalar o Ubuntu 18.04 em seu próprio computador, acesse <http://releases.ubuntu.com/bionic/>. Também é possível criar máquinas virtuais Ubuntu no Azure. Confira [Criar e gerenciar VMs do Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> Neste momento, não há suporte para o [Subsistema do Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 como um destino de instalação.

Para obter outros requisitos do sistema, confira [Requisitos do sistema do SQL Server em Linux](sql-server-linux-setup.md#system).

> [!NOTE]
> Há suporte para o Ubuntu 18.04 a partir do SQL Server 2017 CU20. Se você quiser usar as instruções neste artigo com o Ubuntu 18.04, use o [caminho de repositório](sql-server-linux-change-repo.md) correto, `18.04` em vez de `16.04`.
>
> Se você estiver executando o SQL Server em uma versão anterior, a configuração será possível com [modificações](https://blogs.msdn.microsoft.com/sql_server_team/installing-sql-server-2017-for-linux-on-ubuntu-18-04-lts/).

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

É necessário ter um computador Ubuntu 16.04 ou 18.04 com **pelo menos 2 GB** de memória.

Para instalar o Ubuntu 18.04 em seu próprio computador, acesse <http://releases.ubuntu.com/bionic/>. Também é possível criar máquinas virtuais Ubuntu no Azure. Confira [Criar e gerenciar VMs do Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> Neste momento, não há suporte para o [Subsistema do Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 como um destino de instalação.

Para obter outros requisitos do sistema, confira [Requisitos do sistema do SQL Server em Linux](sql-server-linux-setup.md#system).

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="install-sql-server"></a><a id="install"></a>Instalar o SQL Server

> [!NOTE]
> Os comandos do SQL Server 2017 a seguir apontam para o repositório do Ubuntu 18.04. Se você estiver usando o Ubuntu 16.04, altere o caminho abaixo para `/ubuntu/16.04/` em vez de `/ubuntu/18.04/`.

Para configurar o SQL Server no Ubuntu, execute os seguintes comandos em um terminal para instalar o pacote **mssql-server**.

1. Importe as chaves GPG do repositório público:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registre o repositório do Ubuntu do Microsoft SQL Server:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > Se quiser instalar o SQL Server 2019, você precisará registrar o repositório do SQL Server 2019. Use o seguinte comando para a instalações do SQL Server 2019:
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
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

## <a name="install-sql-server"></a><a id="install"></a>Instalar o SQL Server

> [!NOTE]
> Os seguintes comandos do SQL Server 2019 apontam para o repositório do Ubuntu 18.04. Se você estiver usando o Ubuntu 16.04, altere o caminho abaixo para `/ubuntu/16.04/` em vez de `/ubuntu/18.04/`.

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

## <a name="install-the-sql-server-command-line-tools"></a><a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

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

1. Atualize a lista de fontes e execute o comando de instalação com o pacote do desenvolvedor do unixODBC. Para obter mais informações, confira [Instalar o Microsoft ODBC Driver for SQL Server (Linux)](../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

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

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
