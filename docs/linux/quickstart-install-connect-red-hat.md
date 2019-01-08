---
title: Introdução ao SQL Server no Red Hat Enterprise Linux
titleSuffix: SQL Server
description: Neste início rápido mostra como instalar o SQL Server 2017 ou 2019 do SQL Server no Red Hat Enterprise Linux e, em seguida, criar e consultar um banco de dados com sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.custom: sql-linux, seodec18
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: 794d241773addc5584869eaa2e05cfa316908ce1
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160474"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>Guia de início rápido: Instalar o SQL Server e criar um banco de dados no Red Hat

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Neste início rápido, você instala o SQL Server 2017 ou 2019 do SQL Server no Red Hat Enterprise Linux (RHEL) 7.3 +. Você se conectar com **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Neste início rápido, você instalar a visualização de 2019 do SQL Server no Red Hat Enterprise Linux (RHEL) 7.3 +. Você se conectar com **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

::: moniker-end

> [!TIP]
> Este tutorial requer entrada do usuário e uma conexão de internet. Se você estiver interessado na [autônoma](sql-server-linux-setup.md#unattended) ou [offline](sql-server-linux-setup.md#offline) procedimentos de instalação, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

Você deve ter um RHEL 7.3 ou 7.4 máquina com **pelo menos 2 GB** de memória.

Para instalar o Red Hat Enterprise Linux em seu próprio computador, vá para [ https://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation). Você também pode criar máquinas virtuais RHEL no Azure. Ver [criar e gerenciar VMs do Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)e use `--image RHEL` na chamada para `az vm create`.

Se você já tiver instalado um CTP ou a versão RC do SQL Server 2017, remova primeiro o repositório antigo antes de seguir estas etapas. Para obter mais informações, consulte [repositórios de configurar o Linux para SQL Server 2017 e 2019 ](sql-server-linux-change-repo.md).

Para outros requisitos do sistema, consulte [requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server no RHEL, execute os seguintes comandos em um terminal para instalar o **mssql-server** pacote:

1. Baixe o arquivo de configuração de repositório do Microsoft SQL Server 2017 Red Hat:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > Se você quiser experimentar o SQL Server 2019, em vez disso, você deve registrar o **versão prévia (2019)** repositório. Use o seguinte comando para instalações do SQL Server 2019:
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   > ```

2. Execute os seguintes comandos para instalar o SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Após a conclusão da instalação de pacote, execute **mssql-conf setup** e siga os prompts para definir a senha de SA e escolha sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > As seguintes edições do SQL Server 2017 são licenciadas gratuitamente: Evaluation, Developer e Express.

   > [!NOTE]
   > Certifique-se de especificar uma senha forte para a conta SA (mínimo comprimento 8 caracteres, incluindo letras maiusculas e minúsculas, dígitos de base 10 e/ou símbolos não alfanuméricos).

4. Quando a configuração estiver concluída, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```

5. Para permitir conexões remotas, abra a porta do SQL Server no firewall no RHEL. Porta do SQL Server padrão é TCP 1433. Se você estiver usando **FirewallD** do seu firewall, você pode usar os comandos a seguir:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

Neste ponto, o SQL Server está em execução no seu computador RHEL e está pronto para uso!

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server no RHEL, execute os seguintes comandos em um terminal para instalar o **mssql-server** pacote:

1. Baixe a versão de preview do Microsoft SQL Server 2019 arquivo de configuração de repositório do Red Hat:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   ```

2. Execute os seguintes comandos para instalar o SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Após a conclusão da instalação de pacote, execute **mssql-conf setup** e siga os prompts para definir a senha de SA e escolha sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Certifique-se de especificar uma senha forte para a conta SA (mínimo comprimento 8 caracteres, incluindo letras maiusculas e minúsculas, dígitos de base 10 e/ou símbolos não alfanuméricos).

4. Quando a configuração estiver concluída, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```

5. Para permitir conexões remotas, abra a porta do SQL Server no firewall no RHEL. Porta do SQL Server padrão é TCP 1433. Se você estiver usando **FirewallD** do seu firewall, você pode usar os comandos a seguir:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

Neste ponto, a visualização de 2019 do SQL Server está em execução no seu computador RHEL e está pronta para uso!

::: moniker-end

## <a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

Para criar um banco de dados, você precisa para se conectar com uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As etapas a seguir instalam as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

1. Baixe o arquivo de configuração do repositório Microsoft Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. Se você tiver uma versão anterior do **mssql-tools** instalado, remova quaisquer pacotes mais antigos do unixODBC.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Execute os seguintes comandos para instalar **mssql-tools** com o pacote de desenvolvedor do unixODBC.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. Para sua conveniência, adicione `/opt/mssql-tools/bin/` para seu **caminho** variável de ambiente. Isso permite que você execute as ferramentas sem especificar o caminho completo. Execute os comandos a seguir para modificar a **caminho** para sessões de logon e sessões interativas/não logon:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
