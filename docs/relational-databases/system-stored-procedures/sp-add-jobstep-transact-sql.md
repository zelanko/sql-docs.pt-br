---
title: sp_add_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobstep_TSQL
- sp_add_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobstep
ms.assetid: 97900032-523d-49d6-9865-2734fba1c755
author: stevestein
ms.author: sstein
ms.openlocfilehash: c312f8798ba4ad42eed327123c9adc5feacba8a8
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412850"
---
# <a name="sp_add_jobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Adiciona uma etapa (operação) a um trabalho do SQL Agent.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > No [instância gerenciada do banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria, mas nem todos os tipos de trabalho SQL Server Agent têm suporte. Consulte [instância gerenciada do banco de dados SQL do Azure diferenças de T-SQL do SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.
  
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
`[ @job_id = ] job_id`O número de identificação do trabalho ao qual adicionar a etapa. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho ao qual adicionar a etapa. *job_name* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @step_id = ] step_id`O número de identificação da sequência para a etapa de trabalho. Os números de identificação da etapa começam em **1** e são incrementados sem lacunas. Se uma etapa for inserida na sequência existente, os números da sequência serão ajustados automaticamente. Um valor será fornecido se *step_id* não for especificado. *step_id* é **int**, com um padrão de NULL.  
  
`[ @step_name = ] 'step_name'`O nome da etapa. *step_name* é **sysname**, sem padrão.  
  
`[ @subsystem = ] 'subsystem'`O subsistema usado pelo serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para executar o *comando*. *subsistema* é **nvarchar (40)** e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|'**ACTIVESCRIPTING**'|Script ativo<br /><br /> ** \* Importante \* \* **[!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|'**CMDEXEC**'|Comando do sistema operacional ou programa executável|  
|'**Distribuição**'|Trabalho do Replication Distribution Agent|  
|'**Instantâneo**'|Trabalho do Replication Snapshot Agent|  
|'**Leitor**de ' '|Trabalho do Replication Log Reader Agent|  
|'**Mesclar**'|Trabalho do Replication Merge Agent|  
|'**QueueReader**'|Trabalho do Replication Queue Reader Agent|  
|'**ANALYSISQUERY**'|Consulta do Analysis Services (MDX, DMX).|  
|'**ANALYSISCOMMAND**'|Comando do Analysis Services (XMLA).|  
|'**DTS**'|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]execução do pacote|  
|'**PowerShell**'|Script do PowerShell|  
|'**TSQL**' (padrão)|[!INCLUDE[tsql](../../includes/tsql-md.md)]privacidade|  
  
`[ @command = ] 'command'`Os comandos a serem executados pelo serviço **SQLSERVERAGENT** por meio do *subsistema*. o *comando* é **nvarchar (max)**, com um padrão de NULL. O SQL Server Agent fornece uma substituição de token que propicia a mesma flexibilidade que as variáveis ao escrever programas de software.  
  
> [!IMPORTANT]  
>  Uma macro de fuga agora deve acompanhar todos os tokens utilizados em etapas de trabalho ou elas falharão. Além disso, deve-se colocar os nomes de token entre parênteses e um sinal de cifrão (`$`) no início da sintaxe do token. Por exemplo:  
>   
>  `$(ESCAPE_`*nome da macro*`(DATE))`  
  
 Para obter mais informações sobre esses tokens e atualizar suas etapas de trabalho para usar a nova sintaxe de token, consulte [usar tokens em etapas de trabalho](../../ssms/agent/use-tokens-in-job-steps.md).  
  
> [!IMPORTANT]  
>  Qualquer usuário Windows com permissões de gravação no Log de Eventos do Windows pode acessar etapas de trabalho ativadas pelos alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou alertas do WMI. Para evitar riscos de segurança, os tokens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que podem ser usados em trabalhos ativados por alertas encontram-se desabilitados por padrão. São eles: **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG**e **WMI(**_propriedade_**)**. Observe que nesta versão, o uso de tokens foi estendido a todos os alertas.  
>   
>  Se tiver que usar esses tokens, garanta, primeiro, que apenas membros dos grupos de segurança confiáveis do Windows, como o grupo Administradores, tenham permissões de gravação no Log de Eventos do computador em que reside o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Depois, clique com o botão direito do mouse em **SQL Server Agent** no Pesquisador de Objetos, selecione **Propriedades**e, na página **Sistema de Alerta** , selecione **Substituir tokens de todas as respostas de trabalho aos alertas** para habilitar esses tokens.  
  
`[ @additional_parameters = ] 'parameters'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] os *parâmetros* são **ntext**, com um padrão de NULL.  
  
`[ @cmdexec_success_code = ] code`O valor retornado por um comando de subsistema **CmdExec** para indicar que o *comando* foi executado com êxito. o *código* é **int**, com um padrão de **0**.  
  
`[ @on_success_action = ] success_action`A ação a ser executada se a etapa for concluída com sucesso. *success_action* é **tinyint**e pode ser um desses valores.  
  
|Valor|Descrição (ação)|  
|-----------|----------------------------|  
|**1** (padrão)|Encerrar com êxito|  
|**2**|Sair com falha|  
|**Beta**|Ir para a próxima etapa|  
|**quatro**|Ir para a etapa *on_success_step_id*|  
  
`[ @on_success_step_id = ] success_step_id`A ID da etapa neste trabalho a ser executada se a etapa for bem sucedido e *success_action* for **4**. *success_step_id* é **int**, com um padrão de **0**.  
  
`[ @on_fail_action = ] fail_action`A ação a ser executada se a etapa falhar. *fail_action* é **tinyint**e pode ser um desses valores.  
  
|Valor|Descrição (ação)|  
|-----------|----------------------------|  
|**uma**|Encerrar com êxito|  
|**2** (padrão)|Sair com falha|  
|**Beta**|Ir para a próxima etapa|  
|**quatro**|Ir para a etapa *on_fail_step_id*|  
  
`[ @on_fail_step_id = ] fail_step_id`A ID da etapa neste trabalho a ser executada se a etapa falhar e *fail_action* for **4**. *fail_step_id* é **int**, com um padrão de **0**.  
  
`[ @server = ] 'server'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] o *servidor* é **nvarchar (30)**, com um padrão de NULL.  
  
`[ @database_name = ] 'database'`O nome do banco de dados no qual executar uma [!INCLUDE[tsql](../../includes/tsql-md.md)] etapa. o *banco de dados* é **sysname**, com um padrão de NULL; nesse caso, o banco de dados **mestre** é usado. Os nomes entre colchetes ([ ]) não são permitidos. Para uma etapa de trabalho do ActiveX, o *banco de dados* é o nome da linguagem de script usada pela etapa.  
  
`[ @database_user_name = ] 'user'`O nome da conta de usuário a ser usada ao executar [!INCLUDE[tsql](../../includes/tsql-md.md)] uma etapa. o *usuário* é **sysname**, com um padrão de NULL. Quando o *usuário* é nulo, a etapa é executada no contexto de usuário do proprietário do trabalho no *banco de dados*.  O SQL Server Agent só incluirá esse parâmetro se o proprietário do trabalho for um sysadmin de SQL Server. Assim, a determinada etapa de Transact-SQL será executada no contexto do determinado nome de usuário do SQL Server. Se o proprietário do trabalho não for um SQL Server sysadmin, a etapa Transact-SQL sempre será executada no contexto do logon que possui esse trabalho, e o @database_user_name parâmetro será ignorado.  
  
`[ @retry_attempts = ] retry_attempts`O número de tentativas de repetição a serem usadas se essa etapa falhar. *retry_attempts* é **int**, com um padrão de **0**, que não indica nenhuma tentativa de repetição.  
  
`[ @retry_interval = ] retry_interval`A quantidade de tempo em minutos entre as tentativas de repetição. *retry_interval* é **int**, com um padrão de **0**, que indica um intervalo de **0**minuto.  
  
`[ @os_run_priority = ] run_priority`Reservado.  
  
`[ @output_file_name = ] 'file_name'`O nome do arquivo no qual a saída desta etapa é salva. *file_name* é **nvarchar (200)**, com um padrão de NULL. *file_name* pode incluir um ou mais dos tokens listados em *comando*. Esse parâmetro é válido somente com comandos em execução nos [!INCLUDE[tsql](../../includes/tsql-md.md)]subsistemas, **CmdExec**, **PowerShell** [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], ou [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
`[ @flags = ] flags`É uma opção que controla o comportamento. *flags* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0** (padrão)|Substitui o arquivo de saída|  
|**2**|Anexa a um arquivo de saída|  
|**quatro**|Grava a saída da etapa de trabalho do [!INCLUDE[tsql](../../includes/tsql-md.md)] no histórico de etapas|  
|**8**|Grava o log na tabela (substitui o histórico existente)|  
|**16**|Grava o log na tabela (anexa ao histórico existente)|  
|**32**|Grave todas as saídas no histórico do trabalho|  
|**64**|Crie um evento do Windows para usar como um sinal para o jobstep de Cmd anular|  
  
`[ @proxy_id = ] proxy_id`O número de ID do proxy que a etapa de trabalho executa como. *proxy_id* é do tipo **int**, com um padrão de NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* será especificado e nenhum *user_name* será especificado, a etapa de trabalho será executada como a conta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço para o Agent.  
  
`[ @proxy_name = ] 'proxy_name'`O nome do proxy que a etapa de trabalho executa como. *proxy_name* é o tipo **sysname**, com um padrão de NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* será especificado e nenhum *user_name* será especificado, a etapa de trabalho será executada como a conta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço para o Agent.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Não  
  
## <a name="remarks"></a>Comentários  
 **sp_add_jobstep** deve ser executado do banco de dados **msdb** .  
  
 O SQL Server Management Studio fornece um modo gráfico fácil de gerenciar trabalhos e é o modo recomendado de criar e gerenciar a infra-estrutura de trabalho.  
  
 Por padrão, uma etapa de trabalho será executada como a conta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço do Agent, a menos que outro proxy seja especificado. Um requisito dessa conta é ser membro da função de segurança fixa **sysadmin** .
  
 Um proxy pode ser identificado por *proxy_name* ou *proxy_id*.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar esse procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 O criador da etapa de trabalho deve ter acesso ao proxy para a etapa de trabalho. Os membros da função de servidor fixa **sysadmin** têm acesso a todos os proxies. O acesso a um proxy deve ser concedido explicitamente a outros usuários.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma etapa de trabalho que altera o acesso ao banco de dados para somente leitura para o banco de dados Sales. Além disso, este exemplo especifica 5 tentativas de repetição, sendo que cada uma deve ocorrer depois de uma espera de 5 minutos.  
  
> [!NOTE]  
>  Este exemplo supõe que o `Weekly Sales Data Backup` trabalho já existe.  
  
```sql
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
  
## <a name="see-also"></a>Consulte Também  
 [Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md)   
 [&#41;&#40;Transact-SQL de sp_add_job](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_schedule](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobstep](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_job](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_jobstep](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_jobstep](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
