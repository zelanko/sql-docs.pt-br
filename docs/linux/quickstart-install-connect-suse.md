---
title: 'SUSE: Instalar o SQL Server em Linux'
description: Este início rápido mostra como instalar o SQL Server 2017 ou o SQL Server 2019 no SUSE Linux Enterprise Server e criar e consultar um banco de dados com sqlcmd.
author: VanMSFT
ms.author: vanto
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: c9ac655959814370058059e86814d4ae1abcbc9a
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496988"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Início Rápido: instalar o SQL Server e criar um banco de dados no SUSE Linux Enterprise Server

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Neste início rápido, você instalará o SQL Server 2017 ou o SQL Server 2019 no SLES (SUSE Linux Enterprise Server) v12 SP2. Em seguida, você se conecta ao **sqlcmd** parar criar seu primeiro banco de dados e executar consultas.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Neste início rápido, você instalará o SQL Server 2019 no SLES (SUSE Linux Enterprise Server) v12. Em seguida, você se conecta ao **sqlcmd** parar criar seu primeiro banco de dados e executar consultas.

> [!IMPORTANT]
> O SQL Server 2019 tem suporte no SUSE Enterprise Linux Server v12 SP2, SP3, SP4 ou SP5.

::: moniker-end

> [!TIP]
> Este tutorial requer a entrada do usuário e uma conexão com a Internet. Se estiver interessado nos procedimentos de instalação [autônoma](sql-server-linux-setup.md#unattended) ou [offline](sql-server-linux-setup.md#offline), confira [Diretrizes de instalação para o SQL Server em Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Pré-requisitos

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

É necessário ter um computador SLES v12 SP2 com **pelo menos 2 GB** de memória. O sistema de arquivos deve ser **XFS** ou **EXT4** . Não há suporte para outros sistemas de arquivos, como **BTRFS** .

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

É necessário ter um computador SLES v12 SP2, SP3, SP4 ou SP5 com **pelo menos 2 GB** de memória. O sistema de arquivos deve ser **XFS** ou **EXT4** . Não há suporte para outros sistemas de arquivos, como **BTRFS** .

::: moniker-end

Para instalar o SUSE Linux Enterprise Server em seu próprio computador, acesse [https://www.suse.com/products/server](https://www.suse.com/products/server). Também é possível criar máquinas virtuais SLES no Azure. Confira [Criar e gerenciar VMs do Linux com a CLI do Azure](/azure/virtual-machines/linux/tutorial-manage-vm) e use `--image SLES` na chamada para `az vm create`.

Se você já tiver instalado uma versão CTP ou RC do SQL Server, será necessário remover primeiro o repositório antigo antes de seguir essas etapas. Para saber mais, confira [Configurar repositórios do Linux para o SQL Server 2017 e 2019](sql-server-linux-change-repo.md).

> [!NOTE]
> Neste momento, não há suporte para o [Subsistema do Windows para Linux](/windows/wsl/about) para Windows 10 como um destino de instalação.

Para obter outros requisitos do sistema, confira [Requisitos do sistema do SQL Server em Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="install-sql-server-2017"></a><a id="install"></a>Instalar o SQL Server 2017

Para configurar o SQL Server 2017 no SLES, execute os seguintes comandos em um terminal para instalar o pacote **mssql-server** :

1. Baixe o arquivo de configuração do repositório SLES do Microsoft SQL Server 2017:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!TIP]
   > Se quiser instalar o SQL Server 2019, você precisará registrar o repositório do SQL Server 2019. Use o seguinte comando para a instalações do SQL Server 2019:
   >
   > ```bash
   > sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   > ```

2. Atualize seus repositórios.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
   Para garantir que a chave de assinatura do pacote da Microsoft esteja instalada em seu sistema, importe-a usando o seguinte comando: 
   
   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```
   
3. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo zypper install -y mssql-server
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
   systemctl status mssql-server
   ```

6. Se planeja se conectar remotamente, talvez seja preciso abrir a porta TCP do SQL Server (padrão 1433) em seu firewall. Se estiver usando o firewall SuSE, será necessário editar o arquivo de configuração **/etc/sysconfig/SuSEfirewall2** . Modifique a entrada **FW_SERVICES_EXT_TCP** para incluir o número da porta do SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

Neste momento, o SQL Server está em execução no seu computador SLES e está pronto para uso!

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="install-sql-server-2019"></a><a id="install"></a>Instalar o SQL Server 2019

Para configurar o SQL Server 2019 no SLES, execute os seguintes comandos em um terminal para instalar o pacote **mssql-server** :

1. Baixe o arquivo de configuração do repositório SLES do Microsoft SQL Server 2019:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   ```

2. Atualize seus repositórios.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```

   Para garantir que a chave de assinatura do pacote da Microsoft esteja instalada no sistema, use o seguinte comando para importar a chave: 

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```
   
3. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo zypper install -y mssql-server
   ```

4. Após a conclusão da instalação do pacote, execute a **instalação de mssql-conf** e siga os prompts para definir a senha SA e escolher sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Especifique uma senha forte para a conta SA (comprimento mínimo de 8 caracteres, incluindo letras maiúsculas e minúsculas, 10 dígitos básicos e/ou símbolos não alfanuméricos).

5. Após concluir a configuração, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```

6. Se planeja se conectar remotamente, talvez seja preciso abrir a porta TCP do SQL Server (padrão 1433) em seu firewall. Se estiver usando o firewall SuSE, será necessário editar o arquivo de configuração **/etc/sysconfig/SuSEfirewall2** . Modifique a entrada **FW_SERVICES_EXT_TCP** para incluir o número da porta do SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

Neste momento, o SQL Server 2019 está em execução no seu computador SLES e está pronto para uso!

::: moniker-end


## <a name="install-the-sql-server-command-line-tools"></a><a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

Para criar um banco de dados, é necessário conectar-se a uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As seguintes etapas instalam as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

1. Adicione o repositório do Microsoft SQL Server ao Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Instale o **mssql-tools** com o pacote do desenvolvedor unixODBC. Para obter mais informações, confira [Instalar o Microsoft ODBC Driver for SQL Server (Linux)](../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. Para sua conveniência, adicione `/opt/mssql-tools/bin/` à sua variável de ambiente **PATH** . Isso permite que você execute as ferramentas sem especificar o caminho completo. Execute os seguintes comandos para modificar o **PATH** para sessões de logon e sessões interativas/que não são de logon:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]