---
title: "Introdução ao SQL Server 2017 no Ubuntu | Microsoft Docs"
description: "Este tutorial de início rápido mostra como instalar o SQL Server 2017 no Ubuntu e, em seguida, criar e consultar um banco de dados com sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/24/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 052a2f0a7618c5e160d3c17a3a1efd7d7a4b3fd6
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-and-create-a-database-on-ubuntu"></a>Instalar o SQL Server e criar um banco de dados no Ubuntu

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

Neste tutorial de início rápido, você deve primeiro instalar SQL Server 2017 RC2 no Ubuntu 16.04. Conecte-se com **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

> [!TIP]
> Este tutorial requer entrada do usuário e uma conexão de internet. Se você estiver interessado no [autônoma](sql-server-linux-setup.md#unattended) ou [offline](sql-server-linux-setup.md#offline) procedimentos de instalação, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Pré-requisitos

Você deve ter uma máquina Ubuntu com **pelo menos 3,25 GB** de memória.

Para instalar o Ubuntu em seu próprio computador, vá para [http://www.ubuntu.com/download/server](http://www.ubuntu.com/download/server). Você também pode criar máquinas virtuais de Ubuntu no Azure. Consulte [criar e gerenciar VMs do Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

Para outros requisitos de sistema, consulte [requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server no Ubuntu, execute os seguintes comandos em um terminal para instalar o **mssql server** pacote.

1. Importe as chaves GPG repositório público:

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre o repositório do Microsoft SQL Server Ubuntu:

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list)"
   ```

1. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

1. Após a conclusão da instalação de pacote, execute **mssql conf instalação** e siga os prompts para definir a senha de SA e escolher a edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Certifique-se de especificar uma senha forte para a conta SA (mínimo 8 caracteres, incluindo letras maiusculas e minúsculas, dígitos de base 10 e/ou símbolos não alfanuméricos).

   > [!TIP]
   > Ao instalar o RC2, não há licenças adquiridas devem tentar qualquer uma das edições. Como é um versão release candidate, a seguinte mensagem aparece independentemente da edição que você selecione:
   >
   > `This is an evaluation version.  There are [175] days left in the evaluation period.`
   >
   > Esta mensagem não reflete a edição que você selecionou. Ele se relaciona com o período de visualização para RC2.

1. Quando a configuração estiver concluída, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```

1. Se você planeja se conectar remotamente, você precisará também abrir a porta TCP do SQL Server (padrão 1433) em seu firewall.

Neste ponto, o SQL Server está em execução no seu computador Ubuntu e está pronto para uso!

## <a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

Para criar um banco de dados, você precisa se conectar com uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As etapas a seguir instalar as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

1. Importe as chaves GPG repositório público:

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre o repositório Microsoft Ubuntu:

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
   ```

1. Atualizar a lista de fontes e execute o comando de instalação com o pacote do desenvolvedor unixODBC:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-tools unixodbc-dev
   ```

1. Para sua conveniência, adicionar `/opt/mssql-tools/bin/` para sua **caminho** variável de ambiente. Isso permite que você execute as ferramentas sem especificar o caminho completo. Execute os comandos a seguir para modificar o **caminho** para sessões de logon e sessões/não-logon interativo:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd** é apenas uma ferramenta para se conectar ao SQL Server para executar consultas e executar tarefas de gerenciamento e desenvolvimento. Outras ferramentas incluem [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md) e [código do Visual Studio](sql-server-linux-develop-use-vscode.md).

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
