---
title: Gerenciar etapas de trabalho | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5f9ecad6fcec2596f26351839311cc8b647e094e
ms.lasthandoff: 04/11/2017

---
# <a name="manage-job-steps"></a>Gerenciar etapas de trabalho
Uma etapa de trabalho é uma ação que o trabalho realiza em um banco de dados ou servidor. Todo trabalho deve ter, pelo menos, uma etapa de trabalho. As etapas de trabalho podem ser:  
  
-   Programas executáveis e comandos de sistema operacional.  
  
-   [!INCLUDE[tsql](../../includes/tsql_md.md)] instruções, inclusive procedimentos armazenados e procedimentos armazenados estendidos.  
  
-   Scripts PowerShell.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Scripts ActiveX.  
  
-   Tarefas de replicação.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] tarefas.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] pacotes.  
  
Toda etapa de trabalho é executada em um contexto de segurança específico. Se a etapa de trabalho especificar um proxy, será executada no contexto de segurança da credencial para aquele proxy. Se a etapa de trabalho não especificar um proxy, ela será executada no contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Apenas membros da função de servidor fixa sysadmin podem criar trabalhos que não especifiquem um proxy explicitamente.  
  
Como as etapas de trabalho são executadas no contexto de um usuário específico do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows, esse usuário deve ter as permissões e a configuração necessárias para a execução da etapa de trabalho. Por exemplo, se você criar um trabalho que requeira uma letra de unidade ou um caminho UNC (convenção de nomenclatura universal), as etapas do trabalho poderão ser executadas em sua conta de usuário do Microsoft Windows durante o teste das tarefas. Porém, o usuário Windows da etapa de trabalho também deve ter as permissões necessárias, as configurações de letra de unidade ou o acesso à unidade necessária. Caso contrário, a etapa de trabalho falhará. Para evitar esse problema, assegure que o proxy de cada etapa de trabalho tenha as permissões necessárias para a tarefa executada pela etapa. Para obter mais informações, consulte [Segurança e proteção (Mecanismo de Banco de Dados)](http://msdn.microsoft.com/en-us/dfb39d16-722a-4734-94bb-98e61e014ee7).  
  
## <a name="job-step-logs"></a>Logs de etapas de trabalho  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent pode gravar a saída de algumas etapas de trabalho em um arquivo do sistema operacional ou na tabela sysjobstepslogs do banco de dados msdb. Os seguintes tipos de etapa de trabalho podem gravar a saída em ambos os destinos:  
  
-   Programas executáveis e comandos de sistema operacional.  
  
-   [!INCLUDE[tsql](../../includes/tsql_md.md)] .  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] tarefas.  
  
Apenas etapas de trabalho executadas por usuários membros da função de servidor fixa sysadmin podem gravar a saída de etapas de trabalho em arquivos do sistema operacional. Se as etapas de trabalho forem executadas por usuários que são membros das funções de banco de dados fixas SQLAgentUserRole, SQLAgentReaderRole ou SQLAgentOperatorRole no banco de dados msdb, a saída dessas etapas só poderá ser gravada na tabela sysjobstepslogs.  
  
Os logs de etapas de trabalho são eliminados automaticamente na exclusão de trabalhos ou de etapas de trabalho.  
  
> [!NOTE]  
> O registro de tarefas de replicação e de etapas de trabalho de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] é manipulado por seus respectivos subsistemas. Não é possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para configurar o registro desses tipos de etapa de trabalho.  
  
## <a name="executable-programs-and-operating-system-commands-as-job-steps"></a>Programas executáveis e comandos do sistema operacional como etapas de trabalho  
Programas executáveis e comandos de sistema operacional podem ser usados como etapas de trabalho. Esses arquivos podem ter as extensões .bat, .cmd, .com ou .exe.  
  
Ao usar um programa executável ou um comando de sistema operacional como etapa de trabalho, é necessário especificar:  
  
-   O código de saída do processo retornado, se o comando teve êxito.  
  
-   O comando a ser executado. Para executar um comando de sistema operacional, trata-se do próprio comando. No caso de um programa externo, é o nome do programa e os argumentos para o programa; por exemplo: **C:\Program Files\Microsoft SQL Server\100\Tools\Binn\sqlcmd.exe -e -q "sp_who"**  
  
    > [!NOTE]  
    > É necessário fornecer o caminho completo para o executável, caso este não esteja localizado em um diretório especificado no caminho de sistema ou no caminho para o usuário em cujo nome a etapa de trabalho é executada.  
  
## <a name="transact-sql-job-steps"></a>Etapas de trabalho do Transact-SQL  
Ao criar uma etapa de trabalho [!INCLUDE[tsql](../../includes/tsql_md.md)] , você deve:  
  
-   Identificar o banco de dados no qual executar o trabalho.  
  
-   Digitar a instrução [!INCLUDE[tsql](../../includes/tsql_md.md)] a executar. A instrução pode chamar um procedimento armazenado ou um procedimento armazenado estendido.  
  
Opcionalmente, você pode abrir um arquivo [!INCLUDE[tsql](../../includes/tsql_md.md)] existente na forma de um comando para a etapa de trabalho.  
  
[!INCLUDE[tsql](../../includes/tsql_md.md)] Etapas de trabalho não usam proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Em vez disso, a etapa de trabalho é executada como o seu proprietário ou como a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, caso o proprietário da etapa de trabalho seja membro da função de servidor fixa sysadmin. Os membros da função de servidor fixa sysadmin também podem especificar que as etapas de trabalho [!INCLUDE[tsql](../../includes/tsql_md.md)] sejam executadas sob o contexto de outro usuário através do parâmetro *database_user_name* do procedimento armazenado sp_add_jobstep. Para obter mais informações, consulte [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755).  
  
> [!NOTE]  
> Uma única etapa de trabalho [!INCLUDE[tsql](../../includes/tsql_md.md)] pode conter vários lotes. [!INCLUDE[tsql](../../includes/tsql_md.md)] As etapas de trabalho podem conter comandos GO inseridos.  
  
## <a name="powershell-scripting-job-steps"></a>Etapas de trabalho de scripts PowerShell  
Ao criar uma etapa de trabalho de script PowerShell, é necessário especificar uma das duas opções a seguir como comando da etapa:  
  
-   O texto de um script PowerShell.  
  
-   Um arquivo de script PowerShell existente a ser aberto.  
  
O subsistema PowerShell do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent abre uma sessão do PowerShell e carrega os snap-ins de PowerShell do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . O script PowerShell usado como o comando de etapa de trabalho pode fazer referência ao provedor de PowerShell do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e cmdlets. Para obter mais informações sobre como escrever scripts PowerShell usando os snap-ins de PowerShell do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , consulte [SQL Server PowerShell](http://msdn.microsoft.com/en-us/89b70725-bbe7-4ffe-a27d-2a40005a97e7).  
  
## <a name="activex-scripting-job-steps"></a>Etapas de trabalho de scripts ActiveX  
  
> [!IMPORTANT]  
> A etapa de trabalho de script ActiveX será removida do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent em uma futura versão do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
Ao criar uma etapa de trabalho de scripts ActiveX, você deve:  
  
-   Identificar a linguagem de script na qual a etapa de trabalho é gravada.  
  
-   Gravar o script ActiveX.  
  
Você também pode abrir um arquivo de script ActiveX existente na forma de um comando para a etapa de trabalho. Alternativamente, os comandos de script ActiveX podem ser compilados externamente (por exemplo, por meio do Microsoft Visual Basic) e executados como programas executáveis.  
  
Quando um comando de etapa de trabalho é um script ActiveX, é possível usar o objeto SQLActiveScriptHost para imprimir a saída em um log de histórico de etapas de trabalho ou criar objetos COM. SQLActiveScriptHost é um objeto global introduzido pelo sistema host do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no namespace de script. O objeto tem dois métodos (Print e CreateObject). O exemplo a seguir mostra como a criação de scripts do ActiveX funciona no Visual Basic Scripting Edition (VBScript).  
  
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
  
Quando a replicação está configurada, é possível especificar a execução de agentes de replicação de três formas: continuamente, depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é iniciado; sob demanda; ou de acordo com a agenda. Para obter mais informações sobre os agentes de replicações, consulte [Visão geral dos agentes de replicação](http://msdn.microsoft.com/en-us/a35ecd7d-f130-483c-87e3-ddc8927bb91b).  
  
## <a name="analysis-services-job-steps"></a>Etapas de trabalho do Analysis Services  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent dá suporte a dois tipos distintos de etapas de trabalho do Analysis Services, etapas de trabalho de comando e de consulta.  
  
### <a name="analysis-services-command-job-steps"></a>Etapas de trabalho de comando do Analysis Services  
Ao criar uma etapa de trabalho de comando do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] , é necessário:  
  
-   Identificar o servidor OLAP do banco de dados no qual a etapa de trabalho será executada.  
  
-   Digitar a instrução a ser executada. A instrução deve ser um XML para o método [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] **do** . A instrução talvez não tenha um envelope SOAP completo ou um XML para o método [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] **do** . Observe que, embora o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] dê suporte a envelopes SOAP completos e ao método **Discover** , as etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent não dão.  
  
### <a name="analysis-services-query-job-steps"></a>Etapas de trabalho de consulta do Analysis Services  
Ao criar uma etapa de trabalho de consulta do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] , é necessário:  
  
-   Identificar o servidor OLAP do banco de dados no qual a etapa de trabalho será executada.  
  
-   Digitar a instrução a ser executada. A instrução deve ser uma consulta de linguagem MDX.  
  
Para obter mais informações sobre o MDX, consulte [Conceitos básicos da instrução MDX](http://msdn.microsoft.com/en-us/a560383b-bb58-472e-95f5-65d03d8ea08b).  
  
## <a name="integration-services-packages"></a>Pacotes do Integration Services  
Ao criar uma etapa de trabalho de pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] , é necessário fazer o seguinte:  
  
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
  
Observe que, se você implantar o pacote no Catálogo do SSIS e especificar o **Catálogo do SSIS** como a origem do pacote, grande parte dessas informações de configuração será obtida automaticamente do pacote. Na guia **Configuração** , você pode especificar o ambiente, valores de parâmetros, valores de gerenciadores de conexões, substituições de propriedade e se o pacote é executado em um ambiente de tempo de execução de 32 bits.  
  
Para obter mais informações sobre como criar etapas de trabalho que executam pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] , consulte [Trabalhos do SQL Server Agent para pacotes](http://msdn.microsoft.com/en-us/ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|||  
|-|-|  
|**Description**|**Tópico**|  
|Descreve como criar uma etapa de trabalho com um programa executável.|[Criar uma etapa de trabalho CmdExec](../../ssms/agent/create-a-cmdexec-job-step.md)|  
|Descreve como redefinir permissões no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Configurar um usuário para criar e gerenciar trabalhos do SQL Server Agent](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)|  
|Descreve como criar uma etapa de trabalho do [!INCLUDE[tsql](../../includes/tsql_md.md)] .|[Create a Transact-SQL Job Step](../../ssms/agent/create-a-transact-sql-job-step.md)|  
|Descreve como definir opções para etapas de trabalho Transact-SQL no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Define Transact-SQL Job Step Options](../../ssms/agent/define-transact-sql-job-step-options.md)|  
|Descreve como criar e executar uma etapa de trabalho do script ActiveX.|[Create an ActiveX Script Job Step](../../ssms/agent/create-an-activex-script-job-step.md)|  
|Descreve como criar e definir etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent que executem comandos e consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Analysis Services.|[Create an Analysis Services Job Step](../../ssms/agent/create-an-analysis-services-job-step.md)|  
|Descreve qual ação o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] deve realizar se uma falha ocorrer durante a execução do trabalho.|[Set Job Step Success or Failure Flow](../../ssms/agent/set-job-step-success-or-failure-flow.md)|  
|Descreve como exibir detalhes de etapa de trabalho na caixa de diálogo Propriedades da Etapa de Trabalho.|[Exibir informações de etapas de trabalho](../../ssms/agent/view-job-step-information.md)|  
|Descreve como excluir um log de etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Delete a Job Step Log](../../ssms/agent/delete-a-job-step-log.md)|  
  
## <a name="see-also"></a>Consulte também  
[sysjobstepslogs (Transact-SQL)](http://msdn.microsoft.com/en-us/128c25db-0b71-449d-bfb2-38b8abcf24a0)  
[Criar trabalhos](../../ssms/agent/create-jobs.md)  
[sp_add_job (Transact-SQL)](http://msdn.microsoft.com/en-us/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
  

