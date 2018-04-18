---
title: sp_add_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_jobstep_TSQL
- sp_add_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobstep
ms.assetid: 97900032-523d-49d6-9865-2734fba1c755
caps.latest.revision: 80
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5f3210cc635396eb391baa30cc7aa2ab85a73bfb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spaddjobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma etapa (operação) a um trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_jobstep [ @job_id = ] job_id | [ @job_name = ] 'job_name'   
     [ , [ @step_id = ] step_id ]   
     { , [ @step_name = ] 'step_name' }   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @command = ] 'command' ]   
     [ , [ @additional_parameters = ] 'parameters' ]   
          [ , [ @cmdexec_success_code = ] code ]   
     [ , [ @on_success_action = ] success_action ]   
          [ , [ @on_success_step_id = ] success_step_id ]   
          [ , [ @on_fail_action = ] fail_action ]   
          [ , [ @on_fail_step_id = ] fail_step_id ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @database_user_name = ] 'user' ]   
     [ , [ @retry_attempts = ] retry_attempts ]   
     [ , [ @retry_interval = ] retry_interval ]   
     [ , [ @os_run_priority = ] run_priority ]   
     [ , [ @output_file_name = ] 'file_name' ]   
     [ , [ @flags = ] flags ]   
     [ , { [ @proxy_id = ] proxy_id   
         | [ @proxy_name = ] 'proxy_name' } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id =** ] *job_id*  
 O número de identificação do trabalho ao qual adicionar a etapa. *job_id* é **uniqueidentifier**, com um padrão NULL.  
  
 [  **@job_name =** ] **'***job_name***'**  
 O nome do trabalho ao qual adicionar a etapa. *job_name* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  O *job_id* ou *job_name* devem ser especificados, mas não é possível especificar ambos.  
  
 [  **@step_id =** ] *step_id*  
 O número de identificação de sequência para a etapa de trabalho. Etapa inicial de números de identificação em **1** e incremento sem espaços. Se uma etapa for inserida na sequência existente, os números da sequência serão ajustados automaticamente. Um valor é fornecido se *step_id* não for especificado. *step_id*é **int**, com um padrão NULL.  
  
 [  **@step_name =** ] **'***step_name***'**  
 O nome da etapa. *step_name*é **sysname**, sem padrão.  
  
 [  **@subsystem =** ] **'***subsistema***'**  
 O subsistema usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço de agente para executar *comando*. *subsistema* é **nvarchar (40)**, e pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|'**ACTIVESCRIPTING**'|Script ativo<br /><br /> **\*\* Importante \*\*** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|'**CMDEXEC**'|Comando do sistema operacional ou programa executável|  
|'**DISTRIBUIÇÃO**'|Trabalho do Replication Distribution Agent|  
|'**SNAPSHOT**'|Trabalho do Replication Snapshot Agent|  
|'**LOGREADER**'|Trabalho do Replication Log Reader Agent|  
|'**MESCLAR**'|Trabalho do Replication Merge Agent|  
|'**QueueReader**'|Trabalho do Replication Queue Reader Agent|  
|'**ANALYSISQUERY**'|Consulta do Analysis Services (MDX, DMX).|  
|'**ANALYSISCOMMAND**'|Comando do Analysis Services (XMLA).|  
|'**Dts**'|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] execução de pacotes|  
|'**PowerShell**'|Scripts PowerShell|  
|'**TSQL**' (padrão)|Instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]|  
  
 [  **@command=** ] **'***comando***'**  
 Os comandos a serem executados pelo **SQLServerAgent** serviço por meio de *subsistema*. *comando* é **nvarchar (max)**, com um padrão NULL. O SQL Server Agent fornece uma substituição de token que propicia a mesma flexibilidade que as variáveis ao escrever programas de software.  
  
> [!IMPORTANT]  
>  Uma macro de fuga agora deve acompanhar todos os tokens utilizados em etapas de trabalho ou elas falharão. Além disso, deve-se colocar os nomes de token entre parênteses e um sinal de cifrão (`$`) no início da sintaxe do token. Por exemplo:  
>   
>  `$(ESCAPE_`*nome de macro*`(DATE))`  
  
 Para obter mais informações sobre esses tokens e atualizar suas etapas de trabalho para usar a nova sintaxe de token, consulte [usar Tokens em etapas de trabalho](http://msdn.microsoft.com/library/105bbb66-0ade-4b46-b8e4-f849e5fc4d43).  
  
> [!IMPORTANT]  
>  Qualquer usuário Windows com permissões de gravação no Log de Eventos do Windows pode acessar etapas de trabalho ativadas pelos alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou alertas do WMI. Para evitar riscos de segurança, os tokens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que podem ser usados em trabalhos ativados por alertas encontram-se desabilitados por padrão. Os tokens são: **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG** e **WMI(***propriedade***)**. Observe que nesta versão, o uso de tokens foi estendido a todos os alertas.  
>   
>  Se tiver que usar esses tokens, garanta, primeiro, que apenas membros dos grupos de segurança confiáveis do Windows, como o grupo Administradores, tenham permissões de gravação no Log de Eventos do computador em que reside o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Depois, clique com o botão direito do mouse em **SQL Server Agent** no Pesquisador de Objetos, selecione **Propriedades**e, na página **Sistema de Alerta** , selecione **Substituir tokens de todas as respostas de trabalho aos alertas** para habilitar esses tokens.  
  
 [  **@additional_parameters=** ] **'***parâmetros***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *parâmetros* é **ntext**, com um padrão NULL.  
  
 [  **@cmdexec_success_code =** ] *código*  
 O valor retornado por uma **CmdExec** comando de subsistema para indicar que *comando* executado com êxito. *código*é **int**, com um padrão de **0**.  
  
 [  **@on_success_action=** ] *success_action*  
 A ação a ser executada se a etapa tiver êxito. *success_action*é **tinyint**, e pode ser um destes valores.  
  
|Value|Descrição (ação)|  
|-----------|----------------------------|  
|**1** (padrão)|Sair com êxito|  
|**2**|Sair com falha|  
|**3**|Ir para a próxima etapa|  
|**4**|Vá para a etapa *on_success_step_id*|  
  
 [  **@on_success_step_id =** ] *success_step_id*  
 A ID da etapa neste trabalho a ser executado se a etapa tiver êxito e *success_action*é **4**. *success_step_id*é **int**, com um padrão de **0**.  
  
 [  **@on_fail_action=** ] *fail_action*  
 A ação a ser executada se a etapa falhar. *fail_action*é **tinyint**, e pode ser um destes valores.  
  
|Value|Descrição (ação)|  
|-----------|----------------------------|  
|**1**|Sair com êxito|  
|**2** (padrão)|Sair com falha|  
|**3**|Ir para a próxima etapa|  
|**4**|Vá para a etapa *on_fail_step_id*|  
  
 [  **@on_fail_step_id=** ] *fail_step_id*  
 A ID da etapa neste trabalho a ser executada se a etapa falhar e *fail_action*é **4**. *fail_step_id*é **int**, com um padrão de **0**.  
  
 [  **@server =**] **'***server***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *servidor*é **nvarchar (30)**, com um padrão NULL.  
  
 [  **@database_name=** ] **'***banco de dados***'**  
 O nome do banco de dados no qual executar uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)]. *banco de dados* é **sysname**, com um padrão NULL, caso em que o **mestre** banco de dados é usado. Os nomes entre colchetes ([ ]) não são permitidos. Para uma etapa do ActiveX, o *banco de dados* é o nome da linguagem de script que usa a etapa.  
  
 [  **@database_user_name=** ] **'***usuário***'**  
 O nome da conta de usuário a ser usada ao executar uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)]. *usuário* é **sysname**, com um padrão NULL. Quando *usuário* for NULL, a etapa é executada no contexto de usuário do proprietário do trabalho na *banco de dados*.  O SQL Server Agent só incluirá esse parâmetro se o proprietário do trabalho for um sysadmin de SQL Server. Assim, a determinada etapa de Transact-SQL será executada no contexto do determinado nome de usuário do SQL Server. Se o proprietário do trabalho não for um sysadmin do SQL Server, a etapa de Transact-SQL sempre será executada no contexto do logon que possua esse trabalho, e o @database_user_name parâmetro será ignorado.  
  
 [  **@retry_attempts=** ] *retry_attempts*  
 O número de novas tentativas a serem usadas se esta etapa apresentar falha. *retry_attempts*é **int**, com um padrão de **0**, que não indica nenhuma repetição tentativas.  
  
 [  **@retry_interval=** ] *intervalo_de_repetição*  
 A quantidade de tempo, em minutos, entre as novas tentativas. *intervalo_de_repetição*é **int**, com um padrão de **0**, que indica um **0**-intervalo de minutos.  
  
 [  **@os_run_priority =** ] *run_priority*  
 Reservado.  
  
 [  **@output_file_name=** ] **'***file_name***'**  
 O nome do arquivo no qual a saída desta etapa é gravado. *file_name*é **nvarchar (200)**, com um padrão NULL. *file_name*pode incluir um ou mais dos tokens listados em *comando*. Este parâmetro é válido somente com comandos executados no [!INCLUDE[tsql](../../includes/tsql-md.md)], **CmdExec**, **PowerShell**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], ou [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] subsistemas.  
  
 [ **@flags=** ] *flags*  
 É uma opção que controla comportamento. *sinalizadores de* é **int**, e pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**0** (padrão)|Substitui o arquivo de saída|  
|**2**|Anexa a um arquivo de saída|  
|**4**|Grava a saída da etapa de trabalho do [!INCLUDE[tsql](../../includes/tsql-md.md)] no histórico de etapas|  
|**8**|Grava o log na tabela (substitui o histórico existente)|  
|**16**|Grava o log na tabela (anexa ao histórico existente)|  
|**32**|Grave todas as saídas no histórico do trabalho|  
|**64**|Crie um evento do Windows para usar como um sinal para o jobstep de Cmd anular|  
  
 [ **@proxy_id** =] *proxy_id*  
 O número de identificação do que a etapa de trabalho é executado como proxy. *proxy_id* é do tipo **int**, com um padrão NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* for especificado e não *user_name* for especificado, a etapa de trabalho é executado como a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
 [ **@proxy_name** =] **'***proxy_name***'**  
 O nome do proxy com o qual a etapa de trabalho é executada. *proxy_name* é do tipo **sysname**, com um padrão NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* for especificado e não *user_name* for especificado, a etapa de trabalho é executado como a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 **sp_add_jobstep** deve ser executado a partir de **msdb** banco de dados.  
  
 O SQL Server Management Studio fornece um modo gráfico fácil de gerenciar trabalhos e é o modo recomendado de criar e gerenciar a infra-estrutura de trabalho.  
  
 Uma etapa de trabalho deve especificar um proxy, a menos que o criador da etapa de trabalho é um membro do **sysadmin** função de segurança fixa.  
  
 Um proxy pode ser identificado por *proxy_name* ou *proxy_id*.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 O criador da etapa de trabalho deve ter acesso ao proxy para a etapa de trabalho. Membros de **sysadmin** função de servidor fixa têm acesso a todos os proxies. O acesso a um proxy deve ser concedido explicitamente a outros usuários.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma etapa de trabalho que altera o acesso de banco de dados para somente leitura para o banco de dados de vendas. Além disso, este exemplo especifica 5 tentativas de repetição, sendo que cada uma deve ocorrer depois de uma espera de 5 minutos.  
  
> [!NOTE]  
>  Este exemplo supõe que o `Weekly Sales Data Backup` trabalho já existe.  
  
```  
USE msdb;  
GO  
EXEC sp_add_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_name = N'Set database to read only',  
    @subsystem = N'TSQL',  
    @command = N'ALTER DATABASE SALES SET READ_ONLY',   
    @retry_attempts = 5,  
    @retry_interval = 5 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibir ou modificar trabalhos](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)   
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
