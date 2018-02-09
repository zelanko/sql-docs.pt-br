---
title: "Introdução ao SQL Server 2017 no SUSE Linux Enterprise Server | Microsoft Docs"
description: "Este guia de início rápido mostra como instalar o SQL Server 2017 no SUSE Linux Enterprise Server e, em seguida, criar e consultar um banco de dados com sqlcmd."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.workload: On Demand
ms.openlocfilehash: 068cf3c1bb3bad2a42f5673f17d0067b0bd019f2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Instalar o SQL Server e criar um banco de dados no SUSE Linux Enterprise Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Neste guia de início rápido, você deve primeiro instalar 2017 do SQL Server no SUSE Linux Enterprise Server (SLES) v12 SP2. Conecte-se com **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

> [!TIP]
> Este tutorial requer entrada do usuário e uma conexão de internet. Se você estiver interessado no [autônoma](sql-server-linux-setup.md#unattended) ou [offline](sql-server-linux-setup.md#offline) procedimentos de instalação, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

Você deve ter um computador do SLES v12 SP2 com **pelo menos 2 GB** de memória. O sistema de arquivos deve ser **XFS** ou **EXT4**. Outros sistemas de arquivos, como **BTRFS**, não têm suporte.

Para instalar o SUSE Linux Enterprise Server na sua própria máquina, vá para [https://www.suse.com/products/server](https://www.suse.com/products/server). Você também pode criar máquinas virtuais SLES no Azure. Consulte [criar e gerenciar máquinas virtuais Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)e usar `--image SLES` na chamada para `az vm create`.

> [!NOTE]
> Neste momento, o [subsistema do Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 não é suportado como um destino de instalação.

Para outros requisitos de sistema, consulte [requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server em SLES, execute os seguintes comandos em um terminal para instalar o **mssql server** pacote:

> [!IMPORTANT]
> Se você instalou anteriormente um CTP ou a versão RC do SQL Server 2017, remova primeiro o repositório antigo antes de registrar um dos repositórios GA. Para obter mais informações, consulte [alterar os repositórios do repositório de visualização no repositório de GA](sql-server-linux-change-repo.md).

1. Baixe o arquivo de configuração do Microsoft SQL Server SLES repositório:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   sudo zypper --gpg-auto-import-keys refresh
   ```

   > [!NOTE]
   > Este é o repositório de atualização cumulativa (CU). Para obter mais informações sobre as opções de repositório e suas diferenças, consulte [configurar repositórios para o SQL Server no Linux](sql-server-linux-change-repo.md).

1. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo zypper install -y mssql-server
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

1. Se você planeja se conectar remotamente, você precisará também abrir a porta TCP do SQL Server (padrão 1433) em seu firewall. Se você estiver usando o firewall do SuSE, você precisa editar o **/etc/sysconfig/SuSEfirewall2** arquivo de configuração. Modificar o **FW_SERVICES_EXT_TCP** entrada para incluir o número da porta do SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

Neste ponto, o SQL Server está em execução no seu computador SLES e está pronto para uso!

## <a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

Para criar um banco de dados, você precisa se conectar com uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As etapas a seguir instalar as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

1. Adicione repositório do Microsoft SQL Server para Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Instalar **mssql ferramentas** com o pacote do desenvolvedor unixODBC.

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
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
> * [Studio de operações do SQL Server (visualização)](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)
> * [Código do Visual Studio](sql-server-linux-develop-use-vscode.md).
> * [mssql-cli (Preview)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
