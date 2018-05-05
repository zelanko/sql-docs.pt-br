---
title: Introdução ao SQL Server 2017 no Red Hat Enterprise Linux | Microsoft Docs
description: Este guia de início rápido mostra como instalar o SQL Server 2017 no Red Hat Enterprise Linux e, em seguida, criar e consultar um banco de dados com sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: 9d23843466886a70d18038988d00c7152075ff07
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>Início rápido: Instalar o SQL Server e criar um banco de dados no Red Hat

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este guia de início rápido, você primeiro instala 2017 do SQL Server no Red Hat Enterprise Linux (RHEL) 7.3 +. Em seguida, você se conectará à ferramenta **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

> [!TIP]
> Este tutorial requer entrada do usuário e uma conexão de internet. Se você estiver interessado no [autônoma](sql-server-linux-setup.md#unattended) ou [offline](sql-server-linux-setup.md#offline) procedimentos de instalação, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

Você deve ter um 7.3 RHEL ou máquina 7.4 com **pelo menos 2 GB** de memória.

Para instalar o Red Hat Enterprise Linux em seu próprio computador, vá para [ http://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation). Você também pode criar máquinas virtuais RHEL no Azure. Consulte [criar e gerenciar máquinas virtuais Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)e usar `--image RHEL` na chamada para `az vm create`.

Para outros requisitos de sistema, consulte [requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server em RHEL, execute os seguintes comandos em um terminal para instalar o **mssql server** pacote:

> [!IMPORTANT]
> Se você instalou anteriormente um CTP ou a versão RC do SQL Server 2017, remova primeiro o repositório antigo antes de registrar um dos repositórios GA. Para obter mais informações, consulte [alterar os repositórios do repositório de visualização no repositório de GA](sql-server-linux-change-repo.md).

1. Baixe o arquivo de configuração do Microsoft SQL Server Red Hat repositório:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!NOTE]
   > Este é o repositório de atualização cumulativa (CU). Para obter mais informações sobre as opções de repositório e suas diferenças, consulte [configurar repositórios para o SQL Server no Linux](sql-server-linux-change-repo.md).

1. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

1. Após a conclusão da instalação de pacote, execute **mssql conf instalação** e siga os prompts para definir a senha de SA e escolha sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```
   > [!TIP]
   > Se você estiver tentando 2017 do SQL Server neste tutorial, as seguintes edições são licenciadas livremente: Evaluation, Developer e Express.

   > [!NOTE]
   > Certifique-se de especificar uma senha forte para a conta SA (mínimo 8 caracteres, incluindo letras maiusculas e minúsculas, dígitos de base 10 e/ou símbolos não alfanuméricos).

1. Quando a configuração estiver concluída, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```
   
1. Para permitir conexões remotas, abra a porta do SQL Server no firewall em RHEL. A porta do SQL Server padrão é TCP 1433. Se você estiver usando **FirewallD** para seu firewall, você pode usar os seguintes comandos:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

Neste ponto, o SQL Server está em execução no seu computador RHEL e está pronto para uso!

## <a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

Para criar um banco de dados, você precisa se conectar com uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As etapas a seguir instalar as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

1. Baixe o arquivo de configuração do repositório Microsoft Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. Se você tiver uma versão anterior do **mssql ferramentas** instalado, remova quaisquer pacotes de unixODBC mais antigos.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Execute os seguintes comandos para instalar **mssql ferramentas** com o pacote do desenvolvedor unixODBC.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. Para sua conveniência, adicionar `/opt/mssql-tools/bin/` para sua **caminho** variável de ambiente. Isso permite que você execute as ferramentas sem especificar o caminho completo. Execute os comandos a seguir para modificar o **caminho** para sessões de logon e sessões/não-logon interativo:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd** é apenas uma ferramenta para se conectar ao SQL Server para executar consultas e executar tarefas de gerenciamento e desenvolvimento. Outras ferramentas incluem:
>
> * [SQL Server Operations Studio (versão prévia)](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)
> * [Código do Visual Studio](sql-server-linux-develop-use-vscode.md).
> * [mssql-cli (Preview)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
