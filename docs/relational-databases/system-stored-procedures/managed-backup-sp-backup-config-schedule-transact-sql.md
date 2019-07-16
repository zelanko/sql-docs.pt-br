---
title: sp_backup_config_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 52df69439cecad5fddf3d38b8852a1ce86cc4dbd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942079"
---
# <a name="managedbackupspbackupconfigschedule-transact-sql"></a>managed_backup.sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura as opções de agendamento personalizadas ou automatizadas para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'
    ,[@scheduling_option = ] {'Custom' | 'System'}  
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
 Especifique 'System' controlado pelo sistema de agendamento de backup. Especifique 'Custom' para um agendamento personalizado definido pelos outros parâmetros.  
  
 @full_backup_freq_type  
 O tipo de frequência para a operação de backup gerenciado, que pode ser definida como "Semanalmente" ou "Daily".  
  
 @days_of_week  
 Os dias da semana para os backups quando @full_backup_freq_type está definido para semanal. Especifique os nomes de cadeia de caracteres completa, como '"segunda-feira.  Você também pode especificar mais de um nome de um dia, separados por Pipe. Por exemplo, N'Monday | Quarta-feira | Sexta-feira '.  
  
 @backup_begin_time  
 Hora de início da janela de backup. Backups não serão iniciados fora da janela de tempo, o que é definida por uma combinação de @backup_begin_time e @backup_duration.  
  
 @backup_duration  
 A duração da janela de tempo de backup. Observe que não há nenhuma garantia de que os backups serão concluídos durante a janela de tempo definida pela @backup_begin_time e @backup_duration. Operações de backup que são iniciadas nessa janela de tempo, mas excederem a duração da janela não serão canceladas.  
  
 @log_backup_freq  
 Isso determina a frequência dos backups de log de transação. Esses backups ocorrem em intervalos regulares, em vez de no agendamento especificado para os backups de banco de dados. @log_backup_freq pode ser em minutos ou horas, e 0 é válido, que não indica que nenhum backup de log. Desabilitando os backups de log só podem ser apropriada para bancos de dados com um modelo de recuperação simples.  
  
> [!NOTE]  
>  Se o modelo de recuperação for alterado de simple para full, você precisará reconfigurar o log_backup_freq de 0 para um valor diferente de zero.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer associação na **db_backupoperator** função de banco de dados com **ALTER ANY CREDENTIAL** permissões, e **EXECUTE** permissões em **sp_delete backuphistory** procedimento armazenado.  
  
## <a name="see-also"></a>Consulte também  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
