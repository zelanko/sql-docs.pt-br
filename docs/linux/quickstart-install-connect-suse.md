---
title: "Introdução ao SQL Server 2017 no SUSE Linux Enterprise Server | Microsoft Docs"
description: "Este tutorial de início rápido mostra como instalar o SQL Server 2017 no SUSE Linux Enterprise Server e, em seguida, criar e consultar um banco de dados com sqlcmd."
author: sabotta
ms.author: carlasab
manager: craigg
ms.date: 07/24/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 21a482de29640b217f1cf6afe1e7b0eeff0ccf85
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Instalar o SQL Server e criar um banco de dados no SUSE Linux Enterprise Server

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

Neste tutorial de início rápido, você deve primeiro instalar 2017 RC2 do SQL Server no SUSE Linux Enterprise Server (SLES) v12 SP2. Conecte-se com **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

> [!TIP]
> Este tutorial requer entrada do usuário e uma conexão de internet. Se você estiver interessado no [autônoma](sql-server-linux-setup.md#unattended) ou [offline](sql-server-linux-setup.md#offline) procedimentos de instalação, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Pré-requisitos

Você deve ter um computador do SLES v12 SP2 com **pelo menos 3,25 GB** de memória. O sistema de arquivos deve ser **XFS** ou **EXT4**. Outros sistemas de arquivos, como **BTRFS**, não têm suporte.

Para instalar o SUSE Linux Enterprise Server na sua própria máquina, vá para [https://www.suse.com/products/server](https://www.suse.com/products/server). Você também pode criar máquinas virtuais SLES no Azure. Consulte [criar e gerenciar máquinas virtuais Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)e usar `--image SLES` na chamada para `az vm create`.

Para outros requisitos de sistema, consulte [requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Instalar o SQL Server

Para configurar o SQL Server em SLES, execute os seguintes comandos em um terminal para instalar o **mssql server** pacote:

1. Baixe o arquivo de configuração do Microsoft SQL Server SLES repositório:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo zypper install -y mssql-server
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
> **Sqlcmd** é apenas uma ferramenta para se conectar ao SQL Server para executar consultas e executar tarefas de gerenciamento e desenvolvimento. Outras ferramentas incluem [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md) e [código do Visual Studio](sql-server-linux-develop-use-vscode.md).

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
