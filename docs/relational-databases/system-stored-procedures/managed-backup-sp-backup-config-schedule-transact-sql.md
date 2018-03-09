---
title: managed_backup.sp_backup_config_schedule (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_backup_config_schedule_TSQL
- managed_backup.sp_backup_config_schedule
- managed_backup.sp_backup_config_schedule_TSQL
- sp_backup_config_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_schedule
- sp_backup_config_schedule
ms.assetid: 82541160-d1df-4061-91a5-6868dd85743a
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3ba08667f9eebe37cc5493903b714ee1bf0d67f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="managedbackupspbackupconfigschedule-transact-sql"></a>managed_backup.sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura as opções de agendamento automatizadas ou personalizadas para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'    ,[@scheduling_option = ] {'Custom' | 'System'}  
    ,[@full_backup_freq_type = ] {'Daily' | 'Weekly'}  
    ,[@days_of_week = ] 'days_of_the_week'  
    ,[@backup_begin_time = ] 'begin time of the backup window'  
    ,[@backup_duration = ] 'backup window length'  
    ,[@log_backup_freq = ] 'frequency of log backup'  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @database_name  
 O nome do banco de dados para habilitar o backup gerenciado em um banco de dados específico. Se for NULL ou *, em seguida, esse backup gerenciado se aplica a todos os bancos de dados no servidor.  
  
 @scheduling_option  
 Especifique 'System' controladas pelo sistema de agendamento de backup. Especifique 'Custom' para um agendamento personalizado definido pela outros paratmeters.  
  
 @full_backup_freq_type  
 O tipo de frequência para a operação de backup gerenciado, que pode ser definida como 'Diário' ou 'Semanalmente'.  
  
 @days_of_week  
 Os dias da semana para os backups quando @full_backup_freq_type está definido para semanal. Especifica nomes de cadeia de caracteres completa como '"segunda-feira.  Você também pode especificar mais de um nome de um dia, separado por vírgulas. Por exemplo "segunda-feira, quarta-feira, sexta-feira'.  
  
 @backup_begin_time  
 A hora de início da janela de backup. Os backups não serão iniciados fora do período de tempo, que é definido por uma combinação de @backup_begin_time e @backup_duration.  
  
 @backup_duration  
 A duração da janela de tempo de backup. Observe que não há nenhuma garantia de que os backups serão concluídos durante a janela de tempo definida pelo @backup_begin_time e @backup_duration. Operações de backup que são iniciadas nesta janela de tempo, mas excedem a duração da janela não serão canceladas.  
  
 @log_backup_freq  
 Isso determina a frequência dos backups de log de transações. Esses backups ocorrem em intervalos regulares, em vez de no agendamento especificado para os backups de banco de dados. @log_backup_freqpode ser em minutos ou horas e 0 é válido, que não indica que nenhum backup de log. Desabilitar backups de log só podem ser adequada para bancos de dados com um modelo de recuperação simples.  
  
> [!NOTE]  
>  Se o modelo de recuperação for alterado de simple para full, você precisa reconfigurar o log_backup_freq de 0 para um valor diferente de zero.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a participação no **db_backupoperator** função, do banco de dados com **ALTER ANY CREDENTIAL** permissões, e **EXECUTE** permissões **sp_delete _ backuphistory** procedimento armazenado.  
  
## <a name="see-also"></a>Consulte também  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
