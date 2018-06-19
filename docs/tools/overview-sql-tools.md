---
title: SQL ferramentas e utilitários para o SQL Server, o banco de dados SQL do Azure e o Azure SQL Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: misc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 0
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: be35a6b708e2f8a5430a796b466705f222d9748d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34709024"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>SQL ferramentas e utilitários para o SQL Server, o banco de dados SQL do Azure e o Azure SQL Data Warehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Para gerenciar (consulta, monitor, etc.) o banco de dados que você precisa de uma ferramenta. Há várias ferramentas de banco de dados disponíveis. Enquanto os bancos de dados podem ser executados na nuvem, no Windows ou em [Linux](../linux/sql-server-linux-overview.md), a ferramenta não precisa ser executado na mesma plataforma como o banco de dados. 

Este artigo fornece informações sobre as ferramentas disponíveis para trabalhar com bancos de dados SQL. 


## <a name="tools-to-run-queries-and-manage-databases"></a>Ferramentas para executar consultas e gerenciar bancos de dados  

| Ferramenta | Descrição |
|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] é uma ferramenta gratuita, leve, para gerenciar bancos de dados onde quer que estejam em execução. Esta versão de visualização fornece recursos de gerenciamento de banco de dados, incluindo um editor de Transact-SQL estendido e personalizáveis ideias sobre o estado operacional dos bancos de dados. **[!INCLUDE[name-sos](../includes/name-sos-short.md)] executa no Linux, Windows e macOS**.|
| [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) | Use o SQL Server Management Studio (SSMS) para consultar, criar e gerenciar o SQL Server, o banco de dados do SQL Azure e o Azure SQL Data Warehouse. **SSMS é executado no Windows**.|
| [SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) | Ative o Visual Studio em um ambiente de desenvolvimento sofisticado para SQL Server, o banco de dados do SQL Azure e o Azure SQL Data Warehouse. **O SSDT é executado no Windows**.|
|[MSSQL cli](mssql-cli.md)|MSSQL cli é uma ferramenta de linha de comando interativa para consultar o SQL Server. **MSSQL cli executa no Linux, Windows e macOS**|
| [Visual Studio Code](https://code.visualstudio.com/)| Após instalar o código do Visual Studio, o [mssql extensão](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) para o desenvolvimento do Microsoft SQL Server, banco de dados do SQL Azure e SQL Data Warehouse. **Código do Visual Studio é executado no Linux, Windows e macOS**.|

## <a name="which-tool-should-i-choose"></a>Qual ferramenta devo escolher?

- Você deseja gerenciar uma instância do SQL Server ou banco de dados em um editor leve no Windows, Linux ou Mac? Escolha [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- Você deseja gerenciar uma instância do SQL Server ou banco de dados no Windows com suporte total a interface gráfica do usuário? Escolha [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)
- Você deseja criar ou manter o código de banco de dados, incluindo a validação em tempo de compilação, designer e refatoração suportam no Windows? Escolha [SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md)
- Você deseja consultar o SQL Server com uma ferramenta de linha de comando que recursos do IntelliSense, iluminação-alta de sintaxe, e muito mais? Escolha [mssql cli](mssql-cli.md)
- Você deseja gravar scripts T-SQL em um editor de leve no Windows, Linux ou Mac? Escolha [código do Visual Studio](https://code.visualstudio.com/) e [mssql extensão](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="additional-tools"></a>Ferramentas adicionais

| Ferramenta | Descrição |
|:--|:--|
| [Configuration Manager](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Use o SQL Server Configuration Manager para configurar os serviços do SQL Server e configurar a conectividade de rede. Gerenciador de configuração é executado no Windows|
|[MSSQL conf](../linux/sql-server-linux-configure-mssql-conf.md)|Use mssql conf para configurar o SQL Server em execução no Linux.|
| [Assistente de Migração do SQL Server](../ssma/sql-server-migration-assistant.md) | Use o Assistente de Migração do SQL Server para automatizar a migração do banco de dados do Microsoft Access, do DB2, do MySQL, do Oracle e do Sybase para o SQL Server.|
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Use o recurso Distributed Replay para ajudá-lo a avaliar o impacto de atualizações futuras do SQL Server. Use também o Distributed Replay para ajudar a avaliar o impacto de hardware e atualizações do sistema operacional e ajuste do SQL Server. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | O utilitário ssbdiagnose relata problemas em conversas do Service Broker ou a configuração de serviços do Service Broker. |


## <a name="command-line-utilities"></a>Utilitários de linha de comando

  Os utilitários de linha de comando permitem executar scripts de operações do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A tabela a seguir contém uma lista de utilitários de prompt de comando que integram o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|**Utilitário**|**Descrição**|**Instalado no**|  
|-----------------|---------------------|----------------------|  
|[Utilitário bcp](../tools/bcp-utility.md)|Usado para copiar dados entre uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e um arquivo de dados em formato especificado pelo usuário.|\<*unidade*:>\Arquivos de Programas\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
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
|[Aplicativo sqlagent90](../tools/sqlagent90-application.md)|Usado para iniciar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent a partir de um prompt de comando.|\<unidade>:\Arquivos de Programas\Microsoft SQL Server\\<*instance_name*>\MSSQL\Binn|  
|[Utilitário sqlcmd](../tools/sqlcmd-utility.md)|Permite a inserção de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] , procedimentos do sistema e arquivos de script no prompt de comando.|\<*unidade*:>\Arquivos de Programas\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[Utilitário SQLdiag](../tools/sqldiag-utility.md)|Usado para coletar informações de diagnóstico para o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../includes/msconame-md.md)] .|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqllogship](../tools/sqllogship-application.md)|Usado pelos aplicativos para executar as operações de backup, cópia e restauração, além das tarefas associadas de limpeza da configuração de envio de logs sem execução dos trabalhos de backup, cópia e restauração.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário SqlLocalDB](../tools/sqllocaldb-utility.md)|Um modo de execução do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] destinado a desenvolvedores de programas.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\|  
|[Utilitário sqlmaint](../tools/sqlmaint-utility.md)|Usado para executar planos de manutenção de banco de dados criados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|\<unidade>:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[Utilitário sqlps](../tools/sqlps-utility.md)|Usado para executar comandos e scripts PowerShell. Carrega e registra o provedor e os cmdlets do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr](../tools/sqlservr-application.md)|Usado para iniciar e parar uma instância de [!INCLUDE[ssDE](../includes/ssde-md.md)] no prompt de comando para solução de problemas.|\<unidade>:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[Utilitário de Ssms](../tools/sql-server-management-studio/ssms-utility.md)|Usado para iniciar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] em um prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[Utilitário tablediff](../tools/tablediff-utility.md)|Usado para comparar os dados em duas tabelas para não convergência, que é útil na solução de problemas de topologia de replicação.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="sql-command-prompt-utilities-syntax-conventions"></a>Convenções de sintaxe de utilitários do prompt de comando SQL  
  
|**Convenção**|**Usado para**|  
|--------------------|------------------|  
|UPPERCASE|Instruções e termos usados no sistema operacional.|  
|`monospace`|Comandos de exemplo e código de programa.|  
|*italic*|Parâmetros fornecidos pelo usuário.|  
|**bold**|Comandos, parâmetros e outra sintaxe que precisam ser digitados exatamente conforme mostrado.|  



