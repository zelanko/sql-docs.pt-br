---
title: Ferramentas do SQL e utilitários para o SQL Server, o banco de dados SQL do Azure e o Azure SQL Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0a0a46fb27c8695ead3cc68e17677ccdcf7cb6fc
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51292972"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>Ferramentas do SQL e utilitários para o SQL Server, o banco de dados SQL do Azure e o Azure SQL Data Warehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Para gerenciar (consulta, monitor, etc.) o banco de dados que você precisa de uma ferramenta. Enquanto os bancos de dados podem estar em execução na nuvem, no Windows ou em [Linux](../linux/sql-server-linux-overview.md), sua ferramenta não precisa ser executado na mesma plataforma de banco de dados. 

Há muitas ferramentas de banco de dados disponíveis, portanto, este artigo fornece descrições e indicadores para algumas das ferramentas disponíveis para trabalhar com bancos de dados SQL. Se precisar de ajuda para decidir qual ferramenta você precisa, consulte [qual ferramenta devo usar?](#which-tool-should-i-choose).


## <a name="gui-tools-to-manage-databases"></a>Ferramentas de GUI para gerenciar bancos de dados  

Estas são as ferramentas de GUI (interface) gráfica do usuário principal:

| Ferramenta | Descrição | É executado em |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] é uma ferramenta gratuita, leve, para gerenciar bancos de dados, independentemente de onde elas estão em execução. Esta versão de visualização fornece recursos de gerenciamento de banco de dados, incluindo um editor Transact-SQL estendido e personalizáveis percepções sobre o estado operacional dos seus bancos de dados. | **[!INCLUDE[name-sos](../includes/name-sos-short.md)] é executado no Windows, macOS e Linux**.|
| [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) | Use o SQL Server Management Studio (SSMS) para consultar, criar e gerenciar seu SQL Server, o banco de dados SQL e o Azure SQL Data Warehouse. | **O SSMS é executado no Windows**.|
| [SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) | Transforme o Visual Studio em um ambiente de desenvolvimento avançado para o SQL Server, banco de dados SQL e Azure SQL Data Warehouse.| **O SSDT é executado no Windows**.|
| [Visual Studio Code](https://code.visualstudio.com/)| Após instalar o Visual Studio Code, o [extensão mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) para o desenvolvimento do Microsoft SQL Server, banco de dados SQL e SQL Data Warehouse.| **Visual Studio Code é executado no Windows, macOS e Linux**.|


## <a name="command-line-tools-to-manage-databases"></a>Ferramentas de linha de comando para gerenciar bancos de dados

Estas são as principais ferramentas de linha de comando:

| Ferramenta | Descrição | É executado em |
|:--|:--|:--|
|[**mssql-cli (versão prévia)**](mssql-cli.md)|**MSSQL-cli** é uma ferramenta de linha de comando interativa para consultar o SQL Server. | Windows, macOS e Linux|
| [**sqlpackage**](sqlpackage.md) |**sqlpackage** é um utilitário de linha de comando que automatiza várias tarefas de desenvolvimento de banco de dados. macOS e Linux em versões do sqlpackage está atualmente em visualização. | Windows, macOS e Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** fornece cmdlets para trabalhar com SQL| Windows, macOS e Linux|
| [**sqlcmd**](sqlcmd-utility.md) |**Sqlcmd** utilitário permite que você insira instruções Transact-SQL, procedimentos do sistema e arquivos de script no prompt de comando. | Windows, macOS e Linux|
|[**bcp**](../2014/tools/bcp-utility.md)|O utilitário **bcp** (**b**ulk **c**opy **p**rogram) copia dados em massa entre uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e um arquivo de dados em um formato especificado pelo usuário.|Windows, macOS e Linux|
|[**MSSQL-scripter (visualização)**](https://github.com/Microsoft/mssql-scripter)|**MSSQL scripter** é uma experiência de linha de comando multiplataforma para scripts de bancos de dados do SQL Server|Windows, macOS e Linux|
|[**MSSQL-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**MSSQL-conf** configura o SQL Server em execução no Linux.|Linux|



## <a name="which-tool-should-i-choose"></a>Qual ferramenta devo escolher?

- Você deseja gerenciar uma instância do SQL Server ou banco de dados em um editor leve no Windows, Linux ou Mac? Escolha [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- Você deseja gerenciar uma instância do SQL Server ou banco de dados no Windows com suporte total da interface gráfica do usuário? Escolha [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)
- Você deseja criar ou manter o código de banco de dados, incluindo a validação em tempo de compilação, designer e refatoração suportam no Windows? Escolha [SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md)
- Você deseja consultar o SQL Server com uma ferramenta de linha de comando que apresenta o IntelliSense, iluminação-alta de sintaxe, e muito mais? Escolha [mssql-cli](mssql-cli.md)
- Você deseja gravar scripts T-SQL em um editor leve no Windows, Linux ou Mac? Escolher [Visual Studio Code](https://code.visualstudio.com/) e o [extensão mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)



## <a name="additional-tools"></a>Ferramentas adicionais

| Ferramenta | Descrição |
|:--|:--|
| [Configuration Manager](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Use o SQL Server Configuration Manager para configurar os serviços do SQL Server e configurar a conectividade de rede. Configuration Manager é executado no Windows|
| [Assistente de Migração do SQL Server](../ssma/sql-server-migration-assistant.md) | Use o Assistente de Migração do SQL Server para automatizar a migração do banco de dados do Microsoft Access, do DB2, do MySQL, do Oracle e do Sybase para o SQL Server.|
| [Assistente para Experimentos de Banco de Dados](../dea/database-experimentation-assistant-overview.md) | Use o Assistente de experimentação do banco de dados para avaliar uma versão de destino do SQL para uma determinada carga de trabalho. |
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Use o recurso Distributed Replay para ajudá-lo a avaliar o impacto de atualizações futuras do SQL Server. Também use o Distributed Replay para ajudar a avaliar o impacto de hardware e atualizações do sistema operacional e ajuste do SQL Server. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | O utilitário ssbdiagnose relata problemas em conversas do Service Broker ou a configuração de serviços do Service Broker. |

Se você estiver procurando por ferramentas adicionais que não são mencionadas nesta página, consulte [utilitários de Prompt de comando do SQL](command-prompt-utility-reference-database-engine.md).

