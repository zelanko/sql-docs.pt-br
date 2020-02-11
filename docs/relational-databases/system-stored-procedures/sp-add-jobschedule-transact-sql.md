---
title: sp_add_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 06dbee74cfb3e2d5e697ea9594d46c98557de8ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70810499"
---
# <a name="sp_add_jobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Cria uma agenda para um trabalho do SQL Agent.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`Número de identificação do trabalho para o qual o agendamento é adicionado. *job_id* é **uniqueidentifier**, sem padrão.  
  
`[ @job_name = ] 'job_name'`Nome do trabalho ao qual o agendamento é adicionado. *job_name* é **nvarchar (128)**, sem padrão.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @name = ] 'name'`Nome da agenda. *nome* é **nvarchar (128)**, sem padrão.  
  
`[ @enabled = ] enabled_flag`Indica o status atual da agenda. *enabled_flag* é **tinyint**, com um padrão de **1** (habilitado). Se for **0**, o agendamento não será habilitado. Se a agenda estiver desabilitada, o trabalho não será executado.  
  
`[ @freq_type = ] frequency_type`Valor que indica quando o trabalho deve ser executado. *frequency_type* é **int**, com um padrão de **0**, e pode ser um dos seguintes valores:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**quatro**|Diário|  
|**8**|Semanalmente|  
|**16**|Mensal|  
|**32**|Mensalmente, em relação a *frequency_interval.*|  
|**64**|Executar ao iniciar o serviço do Agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**128**|Executar quando o computador estiver ocioso.|  
  
`[ @freq_interval = ] frequency_interval`Dia em que o trabalho é executado. *frequency_interval* é **int**, com um padrão de 0, e depende do valor de *frequency_type* conforme indicado na tabela a seguir:  
  
|Valor|Efeito|  
|-----------|------------|  
|**1** (uma vez)|*frequency_interval* não é usado.|  
|**4** (diário)|A cada *frequency_interval* dias.|  
|**8** (semanal)|*frequency_interval* é um ou mais dos seguintes (combinados com um operador lógico OR):<br /><br /> 1 = Domingo<br /><br /> 2 = Segunda-feira<br /><br /> 4 = terça-feira<br /><br /> 8 = quarta-feira<br /><br /> 16 = quinta-feira<br /><br /> 32 = sexta-feira<br /><br /> 64 = sábado|  
|**16** (mensal)|No *frequency_interval* dia do mês.|  
|**32** (relativo mensal)|*frequency_interval* é um dos seguintes:<br /><br /> 1 = Domingo<br /><br /> 2 = Segunda-feira<br /><br /> 3 = Terça-feira<br /><br /> 4 = Quarta-feira<br /><br /> 5 = Quinta-feira<br /><br /> 6 = Sexta-feira<br /><br /> 7 = Sábado<br /><br /> 8 = Dia<br /><br /> 9 = Dia útil<br /><br /> 10 = Dia de fim de semana|  
|**64** (quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço do agente é iniciado)|*frequency_interval* não é usado.|  
|**128**|*frequency_interval* não é usado.|  
  
`[ @freq_subday_type = ] frequency_subday_type`Especifica as unidades para *frequency_subday_interval*. *frequency_subday_type* é **int**, sem padrão, e pode ser um dos seguintes valores:  
  
|Valor|Descrição (unidade)|  
|-----------|--------------------------|  
|**0x1**|Na hora especificada|  
|**0x4**|minutos|  
|**0x8**|Horas|  
  
`[ @freq_subday_interval = ] frequency_subday_interval`Número de períodos de *frequency_subday_type* a ocorrer entre cada execução do trabalho. *frequency_subday_interval* é **int**, com um padrão de 0.  
  
`[ @freq_relative_interval = ] frequency_relative_interval`Além disso, define o *frequency_interval* quando *frequency_type* é definido como **32** (relativo mensal).  
  
 *frequency_relative_interval* é **int**, sem padrão, e pode ser um dos seguintes valores:  
  
|Valor|Descrição (unidade)|  
|-----------|--------------------------|  
|**1**|Primeiro|  
|**2**|Segundo|  
|**quatro**|Terceiro|  
|**8**|Quarto|  
|**16**|Último|  
  
 *frequency_relative_interval* indica a ocorrência do intervalo. Por exemplo, se *frequency_relative_interval* for definido como **2**, *frequency_type* será definido como **32**e *frequency_interval* será definido como **3**, o trabalho agendado ocorrerá na segunda terça-feira de cada mês.  
  
`[ @freq_recurrence_factor = ] frequency_recurrence_factor`Número de semanas ou meses entre a execução agendada do trabalho. *frequency_recurrence_factor* será usado somente se *frequency_type* estiver definido como **8**, **16**ou **32**. *frequency_recurrence_factor* é **int**, com um padrão de 0.  
  
`[ @active_start_date = ] active_start_date`Data em que a execução do trabalho pode começar. *active_start_date* é **int**, sem padrão. A data é formatada como DDMMAAAA. Se *active_start_date* for definido, a data deverá ser maior ou igual a 19900101.  
  
 Depois que a agenda estiver criada, reveja a data de início e confirme se essa é a data correta. Para obter mais informações, consulte a seção "data de início do agendamento" em [criar e anexar agendas a trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
`[ @active_end_date = ] active_end_date`Data em que a execução do trabalho pode parar. *active_end_date* é **int**, sem padrão. A data é formatada como DDMMAAAA.  
  
`[ @active_start_time = ] active_start_time`Hora em qualquer dia entre *active_start_date* e *active_end_date* para iniciar a execução do trabalho. *active_start_time* é **int**, sem padrão. A hora é formatada como HHMMSS em um relógio de 24 horas.  
  
`[ @active_end_time = active_end_time_`Hora em qualquer dia entre *active_start_date* e *active_end_date* para encerrar a execução do trabalho. *active_end_time* é **int**, sem padrão. A hora é formatada como HHMMSS em um relógio de 24 horas.  
  
`[ @schedule_id = schedule_idOUTPUT`Número de identificação de agendamento atribuído à agenda se ele for criado com êxito. *schedule_id* é uma variável de saída do tipo **int**, sem padrão.  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT`Um identificador exclusivo para a agenda. *schedule_uid* é uma variável do tipo **uniqueidentifier**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 As agendas de trabalho podem ser gerenciadas independentemente dos trabalhos. Para adicionar um agendamento a um trabalho, use **sp_add_schedule** para criar a agenda e **sp_attach_schedule** para anexar a agenda a um trabalho.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar esse procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
 
 ## <a name="example"></a>Exemplo
 O exemplo a seguir atribui um plano de trabalho para `SaturdayReports` o qual será executado todos os sábados às 2:00.
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>Consulte Também  
 [Criar e anexar agendas a trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [Agendar um trabalho](../../ssms/agent/schedule-a-job.md)   
 [Criar uma agenda](../../ssms/agent/create-a-schedule.md)   
 [SQL Server Agent procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_schedule](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_schedule](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_schedule](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_schedule](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_attach_schedule](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
