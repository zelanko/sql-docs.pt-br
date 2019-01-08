---
title: Introdução ao SQL Server no SUSE Linux Enterprise Server
titleSuffix: SQL Server
description: Neste início rápido mostra como instalar o SQL Server 2017 ou 2019 do SQL Server no SUSE Linux Enterprise Server e, em seguida, criar e consultar um banco de dados com sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: d73a1a3b75bbdce6604677464b6947c789bedbac
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160554"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Guia de início rápido: Instalar o SQL Server e criar um banco de dados no SUSE Linux Enterprise Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Neste início rápido, você instala o SQL Server 2017 ou visualização de 2019 do SQL Server no SUSE Linux Enterprise Server (SLES) v12 SP2. Você se conectar com **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Neste início rápido, você pode instalar visualização de 2019 do SQL Server no SUSE Linux Enterprise Server (SLES) v12 SP2. Você se conectar com **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

::: moniker-end

> [!TIP]
> Este tutorial requer entrada do usuário e uma conexão de internet. Se você estiver interessado na [autônoma](sql-server-linux-setup.md#unattended) ou [offline](sql-server-linux-setup.md#offline) procedimentos de instalação, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

Você deve ter um computador do SLES v12 SP2 com **pelo menos 2 GB** de memória. O sistema de arquivos deve ser **XFS** ou **EXT4**. Outros sistemas de arquivos, como **BTRFS**, não têm suporte.

Para instalar o SUSE Linux Enterprise Server em seu próprio computador, vá para [ https://www.suse.com/products/server ](https://www.suse.com/products/server). Você também pode criar máquinas virtuais SLES no Azure. Ver [criar e gerenciar VMs do Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)e use `--image SLES` na chamada para `az vm create`.

Se você já tiver instalado um CTP ou a versão RC do SQL Server 2017, remova primeiro o repositório antigo antes de seguir estas etapas. Para obter mais informações, consulte [repositórios de configurar o Linux para SQL Server 2017 e 2019 ](sql-server-linux-change-repo.md).

> [!NOTE]
> Neste momento, o [subsistema do Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 não tem suporte como um destino de instalação.

Para outros requisitos do sistema, consulte [requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server em SLES, execute os seguintes comandos em um terminal para instalar o **mssql-server** pacote:

1. Baixe o arquivo de configuração de repositório do Microsoft SQL Server 2017 SLES:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!TIP]
   > Se você quiser experimentar o SQL Server 2019, em vez disso, você deve registrar o **versão prévia (2019)** repositório. Use o seguinte comando para instalações do SQL Server 2019:
   >
   > ```bash
   > sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   > ```

2. Atualize seus repositórios.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. Execute os seguintes comandos para instalar o SQL Server:

   ```bash
   sudo zypper install -y mssql-server
   ```

4. Após a conclusão da instalação de pacote, execute **mssql-conf setup** e siga os prompts para definir a senha de SA e escolha sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > As seguintes edições do SQL Server 2017 são licenciadas gratuitamente: Evaluation, Developer e Express.

   > [!NOTE]
   > Certifique-se de especificar uma senha forte para a conta SA (mínimo comprimento 8 caracteres, incluindo letras maiusculas e minúsculas, dígitos de base 10 e/ou símbolos não alfanuméricos).

5. Quando a configuração estiver concluída, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```

6. Se você planeja se conectar remotamente, você precisará também abrir a porta TCP do SQL Server (padrão 1433) no firewall. Se você estiver usando o firewall do SuSE, você precisa editar o **/etc/sysconfig/SuSEfirewall2** arquivo de configuração. Modificar a **FW_SERVICES_EXT_TCP** entrada para incluir o número da porta do SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

Neste ponto, o SQL Server está em execução no seu computador SLES e está pronto para uso!

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server em SLES, execute os seguintes comandos em um terminal para instalar o **mssql-server** pacote:

1. Baixe o arquivo de configuração de repositório do Microsoft SQL Server 2019 visualização SLES:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   ```

2. Atualize seus repositórios.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. Execute os seguintes comandos para instalar o SQL Server:

   ```bash
   sudo zypper install -y mssql-server
   ```

4. Após a conclusão da instalação de pacote, execute **mssql-conf setup** e siga os prompts para definir a senha de SA e escolha sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Certifique-se de especificar uma senha forte para a conta SA (mínimo comprimento 8 caracteres, incluindo letras maiusculas e minúsculas, dígitos de base 10 e/ou símbolos não alfanuméricos).

5. Quando a configuração estiver concluída, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```

6. Se você planeja se conectar remotamente, você precisará também abrir a porta TCP do SQL Server (padrão 1433) no firewall. Se você estiver usando o firewall do SuSE, você precisa editar o **/etc/sysconfig/SuSEfirewall2** arquivo de configuração. Modificar a **FW_SERVICES_EXT_TCP** entrada para incluir o número da porta do SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

Neste ponto, a visualização de 2019 do SQL Server está em execução no seu computador SLES e está pronta para uso!

::: moniker-end


## <a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

Para criar um banco de dados, você precisa para se conectar com uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As etapas a seguir instalam as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

1. Adicione o repositório do Microsoft SQL Server para o Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Instale **mssql-tools** com o pacote de desenvolvedor do unixODBC.

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. Para sua conveniência, adicione `/opt/mssql-tools/bin/` para seu **caminho** variável de ambiente. Isso permite que você execute as ferramentas sem especificar o caminho completo. Execute os comandos a seguir para modificar a **caminho** para sessões de logon e sessões interativas/não logon:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
