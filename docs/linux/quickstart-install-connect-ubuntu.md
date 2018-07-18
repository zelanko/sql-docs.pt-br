---
title: Introdução ao SQL Server 2017 no Ubuntu | Microsoft Docs
description: Neste início rápido mostra como instalar o SQL Server 2017 no Ubuntu e, em seguida, criar e consultar um banco de dados com sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: ebe7da1e1024cefc14c52d0a02e0517b764c8d07
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057314"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>Guia de início rápido: Instalar o SQL Server e criar um banco de dados no Ubuntu

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Neste início rápido, você deve primeiro instalar o SQL Server 2017 no Ubuntu 16.04. Em seguida, você se conectará à ferramenta **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

> [!TIP]
> Este tutorial requer entrada do usuário e uma conexão de internet. Se você estiver interessado na [autônoma](sql-server-linux-setup.md#unattended) ou [offline](sql-server-linux-setup.md#offline) procedimentos de instalação, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

Você deve ter um computador Ubuntu 16.04 com **pelo menos 2 GB** de memória.

Para instalar o Ubuntu em seu próprio computador, vá para [ http://www.ubuntu.com/download/server ](http://www.ubuntu.com/download/server). Você também pode criar máquinas virtuais do Ubuntu no Azure. Ver [criar e gerenciar VMs do Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> Neste momento, o [subsistema do Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) para Windows 10 não tem suporte como um destino de instalação.

Para outros requisitos do sistema, consulte [requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server no Ubuntu, execute os seguintes comandos em um terminal para instalar o **mssql-server** pacote.

> [!IMPORTANT]
> Se você já tiver instalado um CTP ou a versão RC do SQL Server 2017, remova primeiro o repositório antigo antes de registrar um dos repositórios de GA. Para obter mais informações, consulte [altere repositórios a partir do repositório de versão prévia para o repositório de GA](sql-server-linux-change-repo.md).

1. Importe as chaves GPG repositório público:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre o repositório do Microsoft SQL Server Ubuntu:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!NOTE]
   > Este é o repositório de atualização cumulativa (CU). Para obter mais informações sobre as opções de repositório e suas diferenças, consulte [configurar repositórios para o SQL Server no Linux](sql-server-linux-change-repo.md).

1. Execute os seguintes comandos para instalar o SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

1. Após a conclusão da instalação de pacote, execute **mssql-conf setup** e siga os prompts para definir a senha de SA e escolha sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Se você estiver experimentando o SQL Server 2017 neste tutorial, as seguintes edições são licenciadas gratuitamente: Evaluation, Developer e Express.

   > [!NOTE]
   > Certifique-se de especificar uma senha forte para a conta SA (mínimo comprimento 8 caracteres, incluindo letras maiusculas e minúsculas, dígitos de base 10 e/ou símbolos não alfanuméricos).

1. Quando a configuração estiver concluída, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```

1. Se você planeja se conectar remotamente, você precisará também abrir a porta TCP do SQL Server (padrão 1433) no firewall.

Neste ponto, o SQL Server está em execução no seu computador Ubuntu e está pronto para uso!

## <a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

Para criar um banco de dados, você precisa para se conectar com uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As etapas a seguir instalam as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

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

> [!TIP]
> **Sqlcmd** é apenas uma ferramenta para conectar-se ao SQL Server para executar consultas e realizar tarefas de gerenciamento e desenvolvimento. Outras ferramentas incluem:
>
> * [SQL Server Operations Studio (versão prévia)](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-manage-ssms.md)
> * [Visual Studio Code](sql-server-linux-develop-use-vscode.md).
> * [mssql-cli (Preview)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
