---
title: Utilitários de prompt de comando SQL (Mecanismo de Banco de Dados)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server]
- command prompt utilities [SQL Server], about command prompt utilities
- command prompt [SQL Server]
- utilities [SQL Server], command prompt
- command prompt [SQL Server], utilities
ms.assetid: 48364bd9-6ea7-45e9-a332-acf3d81bbfae
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: a25fcbb39b2b4edacd3d9e6ddab64a88d5888fe9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74992742"
---
# <a name="sql-command-prompt-utilities-database-engine"></a>Utilitários de prompt de comando SQL (Mecanismo de Banco de Dados)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Utilitários de prompt de comando permitem executar scripts de operações do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . A tabela a seguir contém uma lista de vários utilitários de prompt de comando que integram o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

Para obter informações sobre as *principais* GUI e ferramentas de linha de comando do SQL, confira [Visão geral das ferramentas SQL](overview-sql-tools.md).

|**Utilitário**|**Descrição**|**Instalado no**|  
|-----------------|---------------------|----------------------|  
|[Utilitário bcp](../tools/bcp-utility.md)|Usado para copiar dados entre uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e um arquivo de dados em formato especificado pelo usuário.|\<*unidade*:>\Arquivos de Programas\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[Utilitário dta](../tools/dta/dta-utility.md)|Usado para analisar uma carga de trabalho e recomendar estruturas de design físicas para otimizar o desempenho do servidor dessa carga de trabalho.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário dtexec](../integration-services/packages/dtexec-utility.md)|Usado para configurar e executar um pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . A versão da interface do usuário desse utilitário de prompt de comando é chamada **DTExecUI**e ativa o Utilitário de Execução de Pacotes.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Utilitário dtutil](../integration-services/dtutil-utility.md)|Usado para gerenciar pacotes SSIS.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Implantar soluções de modelo com o Utilitário de Implantação](https://docs.microsoft.com/analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility)|Usado para implantar projetos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em instâncias do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|   
|[Utilitário osql](../tools/osql-utility.md)|Permite a inserção de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] , procedimentos do sistema e arquivos de script no prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário Profiler](../tools/profiler-utility.md)|Usado para iniciar o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] em um prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário RS.exe &#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|Usado para executar scripts criados para gerenciar servidores de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário rsconfig &#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|Usado para configurar uma conexão de servidor de relatório.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário rskeymgmt &#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|Usado para gerenciar chaves de criptografia em um servidor de relatório.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqlagent90](../tools/sqlagent90-application.md)|Usado para iniciar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent a partir de um prompt de comando.|\<unidade>:\Arquivos de Programas\Microsoft SQL Server\\<*instance_name*>\MSSQL\Binn|  
|[Utilitário sqlcmd](../tools/sqlcmd-utility.md)|Permite a inserção de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] , procedimentos do sistema e arquivos de script no prompt de comando.|\<*unidade*:>\Arquivos de Programas\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[Utilitário SQLdiag](../tools/sqldiag-utility.md)|Usado para coletar informações de diagnóstico para o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../includes/msconame-md.md)] .|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqllogship](../tools/sqllogship-application.md)|Usado pelos aplicativos para executar as operações de backup, cópia e restauração, além das tarefas associadas de limpeza da configuração de envio de logs sem execução dos trabalhos de backup, cópia e restauração.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário SqlLocalDB](../tools/sqllocaldb-utility.md)|Um modo de execução do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] destinado a desenvolvedores de programas.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário sqlmaint](../tools/sqlmaint-utility.md)|Usado para executar planos de manutenção de banco de dados criados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|\<unidade>:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[Utilitário sqlps](../tools/sqlps-utility.md)|Usado para executar comandos e scripts PowerShell. Carrega e registra o provedor e os cmdlets do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqlservr](../tools/sqlservr-application.md)|Usado para iniciar e parar uma instância de [!INCLUDE[ssDE](../includes/ssde-md.md)] no prompt de comando para solução de problemas.|\<unidade>:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[Utilitário de Ssms](../tools/sql-server-management-studio/ssms-utility.md)|Usado para iniciar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] em um prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[Utilitário tablediff](../tools/tablediff-utility.md)|Usado para comparar os dados em duas tabelas para não convergência, que é útil na solução de problemas de topologia de replicação.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="command-prompt-utilities-syntax-conventions"></a>Convenções de sintaxe de utilitários de prompt de comando  
  
|**Convenção**|**Usadas para**|  
|--------------------|------------------|  
|LETRAS MAIÚSCULAS|Instruções e termos usados no sistema operacional.|  
|`monospace`|Comandos de exemplo e código de programa.|  
|*italic*|Parâmetros fornecidos pelo usuário.|  
|**bold**|Comandos, parâmetros e outra sintaxe que precisam ser digitados exatamente conforme mostrado.|  

## <a name="see-also"></a>Consulte Também

* [Replication Distribution Agent](../relational-databases/replication/agents/replication-distribution-agent.md)
* [Agente do Leitor de Log de Replicação](../relational-databases/replication/agents/replication-log-reader-agent.md)
* [Replication Merge Agent](../relational-databases/replication/agents/replication-merge-agent.md)
* [Agente de Leitor de Fila de Replicação](../relational-databases/replication/agents/replication-queue-reader-agent.md)
* [Replication Snapshot Agent](../relational-databases/replication/agents/replication-snapshot-agent.md)