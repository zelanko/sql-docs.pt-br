---
title: Ferramentas e utilitários SQL para SQL Server, banco de dados SQL do Azure e Azure SQL Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fe249e4df9c33fcbb292fc93f218e16ae111b0bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105657"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>Ferramentas e utilitários SQL para SQL Server, banco de dados SQL do Azure e Azure SQL Data Warehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Para gerenciar (consulta, monitor, etc.) seu banco de dados, você precisa de uma ferramenta. Embora seus bancos de dados possam ser executados na nuvem, no Windows ou no [Linux](../linux/sql-server-linux-overview.md), sua ferramenta não precisa ser executada na mesma plataforma que o banco de dados. 

Há muitas ferramentas de banco de dados disponíveis, portanto, este artigo fornece descrições e ponteiros para algumas das ferramentas disponíveis para trabalhar com seus bancos de dados SQL. Se você precisar de ajuda para decidir qual ferramenta precisa, consulte [qual ferramenta devo usar?](#which-tool-should-i-choose).

## <a name="gui-tools-to-manage-databases"></a>Ferramentas de GUI para gerenciar bancos de dados  

A seguir estão as principais ferramentas de GUI (interface gráfica do usuário):

| Ferramenta | Descrição | É executado em |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)]o é uma ferramenta gratuita e leve para o gerenciamento de bancos de dados onde quer que estejam em execução. Esta versão de visualização fornece recursos de gerenciamento de banco de dados, incluindo um editor Transact-SQL estendido e informações personalizáveis sobre o estado operacional de seus bancos de dados. | **é executado no Windows, no MacOS e no Linux. [!INCLUDE[name-sos](../includes/name-sos-short.md)]**|
| [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) | Use o SQL Server Management Studio (SSMS) para consultar, projetar e gerenciar seu SQL Server, o banco de dados SQL do Azure e o Azure SQL Data Warehouse. | **O SSMS é executado no Windows**.|
| [SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) | Transforme o Visual Studio em um ambiente de desenvolvimento avançado para SQL Server, banco de dados SQL do Azure e SQL Data Warehouse do Azure.| **O SSDT é executado no Windows**.|
| [Visual Studio Code](https://code.visualstudio.com/)| Depois de instalar o Visual Studio Code, instale a [extensão MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) para desenvolver Microsoft SQL Server, banco de dados SQL do Azure e SQL data warehouse.| O **Visual Studio Code é executado no Windows, no MacOS e no Linux**.|


## <a name="command-line-tools-to-manage-databases"></a>Ferramentas de linha de comando para gerenciar bancos de dados

A seguir estão as principais ferramentas de linha de comando:

| Ferramenta | Descrição | É executado em |
|:--|:--|:--|
|[**mssql-cli (versão prévia)** ](mssql-cli.md)|**MSSQL-CLI** é uma ferramenta de linha de comando interativa para consultar SQL Server. | Windows, macOS e Linux|
| [**sqlpackage**](sqlpackage.md) |**SqlPackage** é um utilitário de linha de comando que automatiza várias tarefas de desenvolvimento de banco de dados. Atualmente, as versões do pacote do macOS e do Linux estão em versão prévia. | Windows, macOS e Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** fornece cmdlets para trabalhar com o SQL| Windows, macOS e Linux|
| [**sqlcmd**](sqlcmd-utility.md) |o utilitário **sqlcmd** permite que você insira instruções TRANSACT-SQL, procedimentos do sistema e arquivos de script no prompt de comando. | Windows, macOS e Linux|
|[**bcp**](https://docs.microsoft.com/sql/tools/bcp-utility?view=sql-server-2014)|O utilitário **bcp** (**b**ulk **c**opy **p**rogram) copia dados em massa entre uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e um arquivo de dados em um formato especificado pelo usuário.|Windows, macOS e Linux|
|[**MSSQL-Scripter (visualização)** ](https://github.com/Microsoft/mssql-scripter)|**MSSQL-Scripter** é uma experiência de linha de comando de várias plataformas para criar scripts SQL Server bancos de dados|Windows, macOS e Linux|
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**MSSQL-conf** configura SQL Server em execução no Linux.|Linux|



## <a name="which-tool-should-i-choose"></a>Qual ferramenta devo escolher?

- Deseja gerenciar um banco de dados ou instância de SQL Server, em um editor leve no Windows, Linux ou Mac? Escolha [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- Deseja gerenciar uma instância de SQL Server ou um banco de dados no Windows com suporte completo a GUI? Escolha [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)
- Deseja criar ou manter o código do banco de dados, incluindo validação de tempo de compilação, refatoração e suporte de designer no Windows? Escolha [SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md)
- Deseja consultar SQL Server com uma ferramenta de linha de comando que apresenta o IntelliSense, a sintaxe de alta iluminação e muito mais? Escolha [MSSQL-CLI](mssql-cli.md)
- Deseja escrever scripts T-SQL em um editor leve no Windows, Linux ou Mac? Escolha [Visual Studio Code](https://code.visualstudio.com/) e a [extensão MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)



## <a name="additional-tools"></a>Ferramentas adicionais

| Ferramenta | Descrição |
|:--|:--|
| [Configuration Manager](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Use SQL Server Configuration Manager para configurar SQL Server serviços e configurar a conectividade de rede. Configuration Manager é executado no Windows|
| [Assistente de Migração do SQL Server](../ssma/sql-server-migration-assistant.md) | Use o Assistente de Migração do SQL Server para automatizar a migração do banco de dados do Microsoft Access, do DB2, do MySQL, do Oracle e do Sybase para o SQL Server.|
| [Assistente para Experimentos de Banco de Dados](../dea/database-experimentation-assistant-overview.md) | Use Assistente para Experimentos de Banco de Dados para avaliar uma versão de destino do SQL para uma determinada carga de trabalho. |
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Use o recurso Distributed Replay para ajudá-lo a avaliar o impacto das atualizações futuras do SQL Server. Além disso, use Distributed Replay para ajudar a avaliar o impacto de atualizações de hardware e de sistema operacional e SQL Server o ajuste. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | O utilitário ssbdiagnose relata problemas em conversas Service Broker ou na configuração de serviços de Service Broker. |

Se você estiver procurando ferramentas adicionais que não são mencionadas nesta página, consulte [utilitários de prompt de comando do SQL](command-prompt-utility-reference-database-engine.md).

