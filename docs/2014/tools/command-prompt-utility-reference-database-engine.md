---
title: Referência de utilitários de Prompt de comando (mecanismo de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server]
- command prompt utilities [SQL Server], about command prompt utilities
- command prompt [SQL Server]
- utilities [SQL Server], command prompt
- command prompt [SQL Server], utilities
ms.assetid: 48364bd9-6ea7-45e9-a332-acf3d81bbfae
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab9eca571a9cf9381e7c6a18207155ddf86ce272
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823550"
---
# <a name="command-prompt-utility-reference-database-engine"></a>Referência de utilitários de prompt de comando (Mecanismo de Banco de Dados)
  Utilitários de prompt de comando permitem executar scripts de operações do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . A tabela a seguir contém uma lista de utilitários de prompt de comando que integram o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|**Utilitário**|**Descrição**|**Instalado no**|  
|-----------------|---------------------|----------------------|  
|[Utilitário bcp](bcp-utility.md)|Usado para copiar dados entre uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e um arquivo de dados em formato especificado pelo usuário.|\<*unidade*:>\Arquivos de Programas\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[Utilitário dta](dta/dta-utility.md)|Usado para analisar uma carga de trabalho e recomendar estruturas de design físicas para otimizar o desempenho do servidor dessa carga de trabalho.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário dtexec](../integration-services/packages/dtexec-utility.md)|Usado para configurar e executar um pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . A versão da interface do usuário desse utilitário de prompt de comando é chamada **DTExecUI**e ativa o Utilitário de Execução de Pacotes.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Utilitário dtutil](../integration-services/dtutil-utility.md)|Usado para gerenciar pacotes SSIS.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Implantar soluções modelo com o Utilitário de Implantação](../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|Usado para implantar projetos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em instâncias do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[Utilitário osql](osql-utility.md)|Permite a inserção de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] , procedimentos do sistema e arquivos de script no prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário Profiler](profiler-utility.md)|Usado para iniciar o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] em um prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário RS.exe &#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|Usado para executar scripts criados para gerenciar servidores de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário rsconfig &#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|Usado para configurar uma conexão de servidor de relatório.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário rskeymgmt &#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|Usado para gerenciar chaves de criptografia em um servidor de relatório.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqlagent90](sqlagent90-application.md)|Usado para iniciar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent a partir de um prompt de comando.|\<unidade>:\Arquivos de Programas\Microsoft SQL Server\\<*instance_name*>\MSSQL\Binn|  
|[Utilitário sqlcmd](sqlcmd-utility.md)|Permite a inserção de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] , procedimentos do sistema e arquivos de script no prompt de comando.|\<*unidade*:>\Arquivos de Programas\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[Utilitário SQLdiag](sqldiag-utility.md)|Usado para coletar informações de diagnóstico para o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../includes/msconame-md.md)] .|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Aplicativo sqllogship](sqllogship-application.md)|Usado pelos aplicativos para executar as operações de backup, cópia e restauração, além das tarefas associadas de limpeza da configuração de envio de logs sem execução dos trabalhos de backup, cópia e restauração.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilitário SqlLocalDB](sqllocaldb-utility.md)|Um modo de execução do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] destinado a desenvolvedores de programas.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\|  
|[Utilitário sqlmaint](sqlmaint-utility.md)|Usado para executar planos de manutenção de banco de dados criados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|\<unidade >: \Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn|  
|[Utilitário sqlps](sqlps-utility.md)|Usado para executar comandos e scripts PowerShell. Carrega e registra o provedor e os cmdlets do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr](sqlservr-application.md)|Usado para iniciar e parar uma instância de [!INCLUDE[ssDE](../includes/ssde-md.md)] no prompt de comando para solução de problemas.|\<unidade >: \Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn|  
|[Utilitário de Ssms](../ssms/ssms-utility.md)|Usado para iniciar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] em um prompt de comando.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[Utilitário tablediff](tablediff-utility.md)|Usado para comparar os dados em duas tabelas para não convergência, que é útil na solução de problemas de topologia de replicação.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  
  
 **Para acessar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager usando o [!INCLUDE[win8](../includes/win8-md.md)]**  
  
 Como o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (MMC) e não um programa autônomo, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo ao executar o [!INCLUDE[win8](../includes/win8-md.md)]. Para abrir o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar** , em **Aplicativos**, digite **SQLServerManager12.msc** (para [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]) ou **SQLServerManager11.msc** (para[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]) e pressione **Enter**.  
  
## <a name="command-prompt-utilities-syntax-conventions"></a>Convenções de sintaxe de utilitários de prompt de comando  
  
|**Convenção**|**Usado para**|  
|--------------------|------------------|  
|UPPERCASE|Instruções e termos usados no sistema operacional.|  
|`monospace`|Comandos de exemplo e código de programa.|  
|*italic*|Parâmetros fornecidos pelo usuário.|  
|**bold**|Comandos, parâmetros e outra sintaxe que precisam ser digitados exatamente conforme mostrado.|  
  
## <a name="see-also"></a>Consulte também  
 [Agente de Distribuição de Replicação](../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente do Leitor de Log de Replicação](../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de Mesclagem de Replicação](../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de Leitor de Fila de Replicação](../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
