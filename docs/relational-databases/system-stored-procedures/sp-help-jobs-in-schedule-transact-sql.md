---
title: sp_help_jobs_in_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_jobs_in_schedule_TSQL
- sp_help_jobs_in_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobs_in_schedule
ms.assetid: 1168aa2c-136b-4ba3-b18e-9070d95a26fa
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 78bffc1432bb650d5c1a7f37c0a712c34236dca1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260056"
---
# <a name="sphelpjobsinschedule-transact-sql"></a>sp_help_jobs_in_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre os trabalhos para os quais uma agenda específica é anexada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_jobs_in_schedule   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@schedule_id =** ] *schedule_id*  
 O identificador da agenda para o qual listar informações. *schedule_id* é **int**, sem padrão. O *schedule_id* ou *schedule_name* pode ser especificado.  
  
 [  **@schedule_name =** ] **'***schedule_name***'**  
 O nome da agenda para a qual listar informações. *schedule_name* é **sysname**, sem padrão. O *schedule_id* ou *schedule_name* pode ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna o seguinte conjunto de resultados:  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|A ID exclusiva do trabalho.|  
|**originating_server**|**nvarchar(30)**|Nome do servidor do qual o trabalho originou.|  
|**name**|**sysname**|Nome do trabalho.|  
|**Habilitado**|**tinyint**|Indica se o trabalho está habilitado para ser executado.|  
|**Descrição**|**nvarchar(512)**|Descrição do trabalho.|  
|**start_step_id**|**Int**|ID da etapa do trabalho em que a execução deve começar.|  
|**category**|**sysname**|Categoria do trabalho.|  
|**proprietário**|**sysname**|Proprietário do trabalho.|  
|**notify_level_eventlog**|**Int**|Bitmask que indica sob quais circunstâncias um evento de notificação deve ser registrado no log de aplicativos do Microsoft Windows. Pode ser um destes valores:<br /><br /> **0** = nunca<br /><br /> **1** = quando um trabalho for bem-sucedido<br /><br /> **2** = quando o trabalho falhar<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_level_email**|**Int**|Bitmask que indica sob quais circunstâncias um email de notificação deve ser enviado quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**notify_level_netsend**|**Int**|Bitmask que indica sob quais circunstâncias uma mensagem de rede deve ser enviada quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**notify_level_page**|**Int**|Bitmask que indica sob quais circunstâncias uma página deve ser enviada quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**notify_email_operator**|**sysname**|Nome de email do operador a ser notificado.|  
|**notify_netsend_operator**|**sysname**|Nome do computador ou usuário usado ao enviar mensagens de rede.|  
|**notify_page_operator**|**sysname**|Nome do computador ou usuário usado ao enviar uma página.|  
|**delete_level**|**Int**|Bitmask que indica sob quais circunstâncias o trabalho deve ser excluído quando for concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**date_created**|**datetime**|Data em que o trabalho foi criado.|  
|**date_modified**|**datetime**|Data em que o trabalho foi modificado pela última vez.|  
|**version_number**|**Int**|Versão do trabalho (atualizada automaticamente sempre que o trabalho é modificado).|  
|**last_run_date**|**Int**|Data da última execução do trabalho.|  
|**last_run_time**|**Int**|Hora da última execução do trabalho.|  
|**last_run_outcome**|**Int**|Resultado do trabalho na última vez em que foi executado:<br /><br /> **0** = falha<br /><br /> **1** = foi bem-sucedida<br /><br /> **3** = cancelada<br /><br /> **5** = desconhecido|  
|**next_run_date**|**Int**|Próxima data em que o trabalho foi agendado para ser executado.|  
|**next_run_time**|**Int**|Próxima hora em que o trabalho foi agendado para ser executado.|  
|**next_run_schedule_id**|**Int**|Número de identificação do próximo agendamento de execução.|  
|**current_execution_status**|**Int**|Status de execução atual.|  
|**current_execution_step**|**sysname**|Etapa de execução atual no trabalho.|  
|**current_retry_attempt**|**Int**|Se o trabalho estiver em execução e a etapa foi repetida, esta é a tentativa de repetição atual.|  
|**has_step**|**Int**|Número de etapas que o trabalho possui.|  
|**has_schedule**|**Int**|Número de agendamentos que o trabalho possui.|  
|**has_target**|**Int**|Número de servidores de destino que o trabalho possui.|  
|**type**|**Int**|Tipo do trabalho:<br /><br /> **1** = trabalho local.<br /><br /> **2** = trabalho multisservidor.<br /><br /> **0** = trabalho não tem nenhum servidor de destino.|  
  
## <a name="remarks"></a>Remarks  
 Este procedimento lista informações sobre trabalhos anexados à agenda especificada.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Membros de **SQLAgentUserRole** só podem exibir o status dos trabalhos que possuem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lista os trabalhos anexados à agenda `NightlyJobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobs_in_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
