---
title: Gerenciar etapas de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server replication]
- job steps [SQL Server Agent]
- jobs [SQL Server Agent], Integration Services package step
- executable programs as job steps
- operating systems [SQL Server], job steps
- Transact-SQL job step
- job steps [Transact-SQL]
- Integration Services packages, job steps
- replication job steps [SQL Server]
- logs [SQL Server], jobs
- SQL Server Agent jobs, job steps
- ActiveX scripting jobs [SQL Server]
- job steps [Analysis Services]
ms.assetid: 51352afc-a0a4-428b-8985-f9e58bb57c31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 27dfa9f596d63021eb5f22b2e0b25a306e7fa2b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798224"
---
# <a name="manage-job-steps"></a>Gerenciar etapas de trabalho
  Uma etapa de trabalho é uma ação que o trabalho realiza em um banco de dados ou servidor. Todo trabalho deve ter, pelo menos, uma etapa de trabalho. As etapas de trabalho podem ser:  
  
-   Programas executáveis e comandos de sistema operacional.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções, inclusive procedimentos armazenados e procedimentos armazenados estendidos.  
  
-   Scripts PowerShell.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Scripts ActiveX.  
  
-   Tarefas de replicação.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tarefas.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes.  
  
 Toda etapa de trabalho é executada em um contexto de segurança específico. Se a etapa de trabalho especificar um proxy, será executada no contexto de segurança da credencial para aquele proxy. Se a etapa de trabalho não especificar um proxy, ela será executada no contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Apenas membros da função de servidor fixa sysadmin podem criar trabalhos que não especifiquem um proxy explicitamente.  
  
 Como as etapas de trabalho são executadas no contexto de um usuário específico do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, esse usuário deve ter as permissões e a configuração necessárias para a execução da etapa de trabalho. Por exemplo, se você criar um trabalho que requeira uma letra de unidade ou um caminho UNC (convenção de nomenclatura universal), as etapas do trabalho poderão ser executadas em sua conta de usuário do Microsoft Windows durante o teste das tarefas. Porém, o usuário Windows da etapa de trabalho também deve ter as permissões necessárias, as configurações de letra de unidade ou o acesso à unidade necessária. Caso contrário, a etapa de trabalho falhará. Para evitar esse problema, assegure que o proxy de cada etapa de trabalho tenha as permissões necessárias para a tarefa executada pela etapa. Para obter mais informações, consulte [central de segurança para SQL Server mecanismo de banco de dados e banco de dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).  
  
## <a name="job-step-logs"></a>Logs de etapas de trabalho  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent pode gravar a saída de algumas etapas de trabalho em um arquivo do sistema operacional ou na tabela sysjobstepslogs do banco de dados msdb. Os seguintes tipos de etapa de trabalho podem gravar a saída em ambos os destinos:  
  
-   Programas executáveis e comandos de sistema operacional.  
  
-   Instruções[!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tarefas.  
  
 Apenas etapas de trabalho executadas por usuários membros da função de servidor fixa sysadmin podem gravar a saída de etapas de trabalho em arquivos do sistema operacional. Se as etapas de trabalho forem executadas por usuários que são membros das funções de banco de dados fixas SQLAgentUserRole, SQLAgentReaderRole ou SQLAgentOperatorRole no banco de dados msdb, a saída dessas etapas só poderá ser gravada na tabela sysjobstepslogs.  
  
 Os logs de etapas de trabalho são eliminados automaticamente na exclusão de trabalhos ou de etapas de trabalho.  
  
> [!NOTE]  
>  O registro de tarefas de replicação e de etapas de trabalho de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é manipulado por seus respectivos subsistemas. Não é possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para configurar o registro desses tipos de etapa de trabalho.  
  
## <a name="executable-programs-and-operating-system-commands-as-job-steps"></a>Programas executáveis e comandos do sistema operacional como etapas de trabalho  
 Programas executáveis e comandos de sistema operacional podem ser usados como etapas de trabalho. Esses arquivos podem ter as extensões .bat, .cmd, .com ou .exe.  
  
 Ao usar um programa executável ou um comando de sistema operacional como etapa de trabalho, é necessário especificar:  
  
-   O código de saída do processo retornado, se o comando teve êxito.  
  
-   O comando a ser executado. Para executar um comando de sistema operacional, trata-se do próprio comando. No caso de um programa externo, é o nome do programa e os argumentos para o programa; por exemplo: **C:\Program Files\Microsoft SQL Server\100\Tools\Binn\sqlcmd.exe -e -q "sp_who"**  
  
    > [!NOTE]  
    >  É necessário fornecer o caminho completo para o executável, caso este não esteja localizado em um diretório especificado no caminho de sistema ou no caminho para o usuário em cujo nome a etapa de trabalho é executada.  
  
## <a name="transact-sql-job-steps"></a>Etapas de trabalho do Transact-SQL  
 Ao criar uma etapa de trabalho [!INCLUDE[tsql](../../includes/tsql-md.md)] , você deve:  
  
-   Identificar o banco de dados no qual executar o trabalho.  
  
-   Digitar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a executar. A instrução pode chamar um procedimento armazenado ou um procedimento armazenado estendido.  
  
 Opcionalmente, você pode abrir um arquivo [!INCLUDE[tsql](../../includes/tsql-md.md)] existente na forma de um comando para a etapa de trabalho.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] Etapas de trabalho não usam proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Em vez disso, a etapa de trabalho é executada como o seu proprietário ou como a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, caso o proprietário da etapa de trabalho seja membro da função de servidor fixa sysadmin. Os membros da função de servidor fixa sysadmin também podem especificar que as etapas de trabalho [!INCLUDE[tsql](../../includes/tsql-md.md)] sejam executadas sob o contexto de outro usuário através do parâmetro *database_user_name* do procedimento armazenado sp_add_jobstep. Para obter mais informações, consulte [sp_add_jobstep &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql).  
  
> [!NOTE]  
>  Uma única etapa de trabalho [!INCLUDE[tsql](../../includes/tsql-md.md)] pode conter vários lotes. [!INCLUDE[tsql](../../includes/tsql-md.md)] As etapas de trabalho podem conter comandos GO inseridos.  
  
## <a name="powershell-scripting-job-steps"></a>Etapas de trabalho de scripts PowerShell  
 Ao criar uma etapa de trabalho de script PowerShell, é necessário especificar uma das duas opções a seguir como comando da etapa:  
  
-   O texto de um script PowerShell.  
  
-   Um arquivo de script PowerShell existente a ser aberto.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subsistema PowerShell do agente abre uma sessão do PowerShell e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carrega os snap-ins do PowerShell. O script do PowerShell usado como o comando de etapa de trabalho [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode fazer referência ao provedor e aos cmdlets do PowerShell. Para obter mais informações sobre como escrever scripts PowerShell usando os snap-ins de PowerShell do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [SQL Server PowerShell](../../powershell/sql-server-powershell.md).  
  
## <a name="activex-scripting-job-steps"></a>Etapas de trabalho de scripts ActiveX  
  
> [!IMPORTANT]  
>  A etapa de trabalho de script ActiveX será removida do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma futura versão do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
 Ao criar uma etapa de trabalho de scripts ActiveX, você deve:  
  
-   Identificar a linguagem de script na qual a etapa de trabalho é gravada.  
  
-   Gravar o script ActiveX.  
  
 Você também pode abrir um arquivo de script ActiveX existente na forma de um comando para a etapa de trabalho. Alternativamente, os comandos de script ActiveX podem ser compilados externamente (por exemplo, por meio do Microsoft Visual Basic) e executados como programas executáveis.  
  
 Quando um comando de etapa de trabalho é um script ActiveX, é possível usar o objeto SQLActiveScriptHost para imprimir a saída em um log de histórico de etapas de trabalho ou criar objetos COM. SQLActiveScriptHost é um objeto global introduzido pelo sistema host do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no namespace de script. O objeto tem dois métodos (Print e CreateObject). O exemplo a seguir mostra como a criação de scripts do ActiveX funciona no Visual Basic Scripting Edition (VBScript).  
  
```  
' VBScript example for ActiveX Scripting job step  
' Create a Dmo.Server object. The object connects to the  
' server on which the script is running.  
  
Set oServer = CreateObject("SQLDmo.SqlServer")  
oServer.LoginSecure = True  
oServer.Connect "(local)"  
'Disconnect and destroy the server object  
oServer.DisConnect  
Set oServer = nothing
```  
  
## <a name="replication-job-steps"></a>Etapas de trabalho de replicação  
 Quando você cria publicações e assinaturas que usam replicação, são criados trabalhos de replicação por padrão. O tipo de trabalho criado é determinado pelo tipo de replicação (de instantâneo, transacional ou de mesclagem) e pelas opções usadas.  
  
 Etapas de trabalho de replicação ativam um destes agentes de replicação:  
  
-   Snapshot Agent (trabalho Snapshot)  
  
-   Log Reader Agent (trabalho LogReader)  
  
-   Distribution Agent (trabalho Distribution)  
  
-   Merge Agent (trabalho Merge)  
  
-   Queue Reader Agent (trabalho QueueReader)  
  
 Quando a replicação está configurada, é possível especificar a execução de agentes de replicação de três formas: continuamente, depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é iniciado; sob demanda; ou de acordo com a agenda. Para obter mais informações sobre os agentes de replicações, consulte [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md).  
  
## <a name="analysis-services-job-steps"></a>Etapas de trabalho do Analysis Services  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent dá suporte a dois tipos distintos de etapas de trabalho do Analysis Services, etapas de trabalho de comando e de consulta.  
  
### <a name="analysis-services-command-job-steps"></a>Etapas de trabalho de comando do Analysis Services  
 Ao criar uma etapa de trabalho de comando do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , é necessário:  
  
-   Identificar o servidor OLAP do banco de dados no qual a etapa de trabalho será executada.  
  
-   Digitar a instrução a ser executada. A instrução deve ser um XML para o método [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Execute**. A instrução talvez não tenha um envelope SOAP completo ou um XML para o método [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Discover**. Observe que, embora o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dê suporte a envelopes SOAP completos e ao método **Discover** , as etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não dão.  
  
### <a name="analysis-services-query-job-steps"></a>Etapas de trabalho de consulta do Analysis Services  
 Ao criar uma etapa de trabalho de consulta do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , é necessário:  
  
-   Identificar o servidor OLAP do banco de dados no qual a etapa de trabalho será executada.  
  
-   Digitar a instrução a ser executada. A instrução deve ser uma consulta de linguagem MDX.  
  
 Para obter mais informações sobre MDX, consulte [conceitos básicos de consulta mdx &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services).  
  
## <a name="integration-services-packages"></a>Pacotes do Integration Services  
 Ao criar uma etapa de trabalho de pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , é necessário fazer o seguinte:  
  
-   Identificar a origem do pacote.  
  
-   Identificar o local do pacote.  
  
-   Se arquivos de configuração forem necessários para o pacote, identificar os arquivos de configuração.  
  
-   Se arquivos de comando forem necessários para o pacote, identificar os arquivos de comando.  
  
-   Identificar a verificação a ser usada para o pacote. Por exemplo, você pode especificar que o pacote deve estar assinado ou ter um ID de pacote específico.  
  
-   Identificar as fontes de dados do pacote.  
  
-   Identificar os provedores de log do pacote.  
  
-   Especificar variáveis e valores a serem definidos antes da execução do pacote.  
  
-   Identificar opções de execução.  
  
-   Adicionar ou modificar opções de linha de comando.  
  
 Observe que, se você implantar o pacote no Catálogo do SSIS e especificar o **Catálogo do SSIS** como a origem do pacote, grande parte dessas informações de configuração será obtida automaticamente do pacote. Na guia **Configuração** , você pode especificar o ambiente, valores de parâmetros, valores de gerenciadores de conexões, substituições de propriedade e se o pacote é executado em um ambiente de runtime de 32 bits.  
  
 Para obter mais informações sobre como criar etapas de trabalho que executam pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , consulte [Trabalhos do SQL Server Agent para pacotes](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Descreve como criar uma etapa de trabalho com um programa executável.|[Create a CmdExec Job Step](create-a-cmdexec-job-step.md)|  
|Descreve como redefinir permissões no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Configure a User to Create and Manage SQL Server Agent Jobs](configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)|  
|Descreve como criar uma etapa de trabalho do [!INCLUDE[tsql](../../includes/tsql-md.md)] .|[Create a Transact-SQL Job Step](create-a-transact-sql-job-step.md)|  
|Descreve como definir opções para etapas de trabalho Transact-SQL no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Define Transact-SQL Job Step Options](define-transact-sql-job-step-options.md)|  
|Descreve como criar e executar uma etapa de trabalho do script ActiveX.|[Create an ActiveX Script Job Step](create-an-activex-script-job-step.md)|  
|Descreve como criar e definir etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executem comandos e consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Analysis Services.|[Create an Analysis Services Job Step](create-an-analysis-services-job-step.md)|  
|Descreve qual ação o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve realizar se uma falha ocorrer durante a execução do trabalho.|[Set Job Step Success or Failure Flow](set-job-step-success-or-failure-flow.md)|  
|Descreve como exibir detalhes de etapa de trabalho na caixa de diálogo Propriedades da Etapa de Trabalho.|[View Job Step Information](view-job-step-information.md)|  
|Descreve como excluir um log de etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Delete a Job Step Log](delete-a-job-step-log.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [dbo. sysjobstepslogs &#40;&#41;Transact-SQL](/sql/relational-databases/system-tables/dbo-sysjobstepslogs-transact-sql)   
 [Criar trabalhos](create-jobs.md)   
 [sp_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
