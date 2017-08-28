---
title: "SQL ferramentas e utilitários para o SQL Server, o banco de dados SQL do Azure e SQL Data Warehouse | Microsoft Docs"
ms.custom: 
ms.date: 08/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 0
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: eccbe54c561e009858f6192126abc57e3399082c
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="tools-and-utilities-for-azure-sql-database-sql-server-and-sql-data-warehouse"></a>Ferramentas e utilitários para o banco de dados do SQL Azure, SQL Server e SQL Data Warehouse

[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]  

![](../includes/media/sql-database-tools.png)Este artigo fornece uma lista de ferramentas disponíveis para trabalhar com o SQL Server, banco de dados do SQL Azure, SQL Data Warehouse e aplicativos baseados em SQL Server. 

Se você deseja acessar diretamente no e começar a criar tabelas, executar consultas, basicamente projetar e gerenciar seu banco de dados, em seguida, [ **SQL Server Management Studio (SSMS)** ](../ssms/download-sql-server-management-studio-ssms.md) mais provável é que a ferramenta. SSMS é gratuito e é executado no Windows.

Se você estiver executando o Linux ou macOS, tente [código do Visual Studio](https://code.visualstudio.com/) com o [ **mssql para o código do Visual Studio** ](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) extensão. Essas ferramentas são para o desenvolvimento do Microsoft SQL Server, o banco de dados do SQL Azure e SQL Data Warehouse com um conjunto avançado de recursos e também são gratuitas. Consulte [Use código do Visual Studio para criar e executar scripts Transact-SQL para SQL Server](../linux/sql-server-linux-develop-use-vscode.md).


## <a name="sql-tools"></a>Ferramentas do SQL 
 
| Ferramenta | Description |
|:--|:--|
| [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) | Use o SQL Server Management Studio (SSMS) para consultar, criar e gerenciar o SQL Server, o banco de dados do SQL Azure e o Azure SQL Data Warehouse. |
| [SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) | Ative o Visual Studio em um ambiente de desenvolvimento sofisticado para SQL Server, o banco de dados do SQL Azure e o Azure SQL Data Warehouse. |
| [Código do Visual Studio](https://code.visualstudio.com/)| Código do Visual Studio funciona no Windows, Linux e macOS. Após instalar o código do Visual Studio, o [mssql extensão](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) para o desenvolvimento do Microsoft SQL Server, o banco de dados do SQL Azure e SQL Data Warehouse. |
| [Configuration Manager](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Use o SQL Server Configuration Manager para configurar os serviços do SQL Server e configurar a conectividade de rede.|
| [Assistente de Migração do SQL Server](../ssma/sql-server-migration-assistant.md) | Use o Assistente de migração do SQL Server para automatizar a migração de banco de dados para o SQL Server do Microsoft Access, DB2, MySQL, Oracle e Sybase.|
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Use o recurso Distributed Replay para ajudá-lo a avaliar o impacto de atualizações futuras do SQL Server. Use também o Distributed Replay para ajudar a avaliar o impacto de hardware e atualizações do sistema operacional e ajuste do SQL Server. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | O utilitário ssbdiagnose relata problemas em conversas do Service Broker ou a configuração de serviços do Service Broker. |


## <a name="sql-command-prompt-utilities"></a>Utilitários de Prompt de comando SQL

  Utilitários de prompt de comando permitem executar scripts de operações do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . A tabela a seguir contém uma lista de utilitários de prompt de comando que integram o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|**Utilitário**|**Descrição**|**Instalado no**|  
|-----------------|---------------------|----------------------|  
|[Utilitário bcp](../tools/bcp-utility.md)|Usado para copiar dados entre uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e um arquivo de dados em formato especificado pelo usuário.|\<*unidade*: > \Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[Utilitário dta](../tools/dta/dta-utility.md)|Usado para analisar uma carga de trabalho e recomendar estruturas de design físicas para otimizar o desempenho do servidor dessa carga de trabalho.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário dtexec](../integration-services/packages/dtexec-utility.md)|Usado para configurar e executar um pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . A versão da interface do usuário desse utilitário de prompt de comando é chamada **DTExecUI**e ativa o Utilitário de Execução de Pacotes.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Utilitário dtutil](../integration-services/dtutil-utility.md)|Usado para gerenciar pacotes SSIS.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Implantar soluções modelo com o Utilitário de Implantação](../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|Usado para implantar projetos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em instâncias do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[MSSQL-scripter (visualização pública)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/17/try-new-sql-server-command-line-tools-to-generate-t-sql-scripts-and-monitor-dynamic-management-views/)|Usado para gerar scripts de criação e inserção T-SQL para objetos de banco de dados no SQL Server, o banco de dados do SQL Azure e o Azure SQL Data Warehouse.|Consulte nossa [repositório GitHub](https://github.com/Microsoft/sql-xplat-cli) para download e informações de uso.| 
|[Utilitário osql](../tools/osql-utility.md)|Permite a inserção de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] , procedimentos do sistema e arquivos de script no prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário Profiler](../tools/profiler-utility.md)|Usado para iniciar o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] em um prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário RS.exe &#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|Usado para executar scripts criados para gerenciar servidores de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário rsconfig &#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|Usado para configurar uma conexão de servidor de relatório.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário rskeymgmt &#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|Usado para gerenciar chaves de criptografia em um servidor de relatório.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqlagent90](../tools/sqlagent90-application.md)|Usado para iniciar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent a partir de um prompt de comando.|\<unidade >: \Program Files\Microsoft do SQL Server\\<*instance_name*> \MSSQL\Binn|  
|[Utilitário sqlcmd](../tools/sqlcmd-utility.md)|Permite a inserção de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] , procedimentos do sistema e arquivos de script no prompt de comando.|\<*unidade*: > \Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[Utilitário SQLdiag](../tools/sqldiag-utility.md)|Usado para coletar informações de diagnóstico para o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../includes/msconame-md.md)] .|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqllogship](../tools/sqllogship-application.md)|Usado pelos aplicativos para executar as operações de backup, cópia e restauração, além das tarefas associadas de limpeza da configuração de envio de logs sem execução dos trabalhos de backup, cópia e restauração.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário SqlLocalDB](../tools/sqllocaldb-utility.md)|Um modo de execução do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] destinado a desenvolvedores de programas.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\|  
|[Utilitário sqlmaint](../tools/sqlmaint-utility.md)|Usado para executar planos de manutenção de banco de dados criados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|\<unidade >: \Program Files\Microsoft mssql13 SQL. MSSQLSERVER\MSSQL\Binn|  
|[Utilitário sqlps](../tools/sqlps-utility.md)|Usado para executar comandos e scripts PowerShell. Carrega e registra o provedor e os cmdlets do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr](../tools/sqlservr-application.md)|Usado para iniciar e parar uma instância de [!INCLUDE[ssDE](../includes/ssde-md.md)] no prompt de comando para solução de problemas.|\<unidade >: \Program Files\Microsoft mssql13 SQL. MSSQLSERVER\MSSQL\Binn|  
|[Utilitário de Ssms](../tools/sql-server-management-studio/ssms-utility.md)|Usado para iniciar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] em um prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[Utilitário tablediff](../tools/tablediff-utility.md)|Usado para comparar os dados em duas tabelas para não convergência, que é útil na solução de problemas de topologia de replicação.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="sql-command-prompt-utilities-syntax-conventions"></a>Convenções de sintaxe de utilitários de Prompt de comando do SQL  
  
|**Convenção**|**Usado para**|  
|--------------------|------------------|  
|UPPERCASE|Instruções e termos usados no sistema operacional.|  
|`monospace`|Comandos de exemplo e código de programa.|  
|*italic*|Parâmetros fornecidos pelo usuário.|  
|**bold**|Comandos, parâmetros e outra sintaxe que precisam ser digitados exatamente conforme mostrado.|  



