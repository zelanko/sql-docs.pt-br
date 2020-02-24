---
title: managed_backup. sp_backup_config_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/20/2020
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e7bb477901dee22c70bb47cd0eaf7da5eb163b7f
ms.sourcegitcommit: 87b932dc4b603a35a19f16e2c681b6a8d4df1fec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77507526"
---
# <a name="managed_backupsp_backup_config_schedule-transact-sql"></a>managed_backup. sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura opções de agendamento automatizadas ou personalizadas para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]o.  
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 O nome do banco de dados para habilitar o backup gerenciado em um banco de dados específico. Se for NULL ou *, esse backup gerenciado se aplicará a todos os bancos de dados no servidor.  
  
 @scheduling_option  
 Especifique "sistema" para agendamento de backup controlado pelo sistema. Especifique ' Custom ' para uma agenda personalizada definida por outros paratmeters.  
  
 @full_backup_freq_type  
 O tipo de frequência para a operação de backup gerenciado, que pode ser definida como ' Daily ' ou ' Weekly '.  
  
 @days_of_week  
 Os dias da semana para os backups quando @full_backup_freq_type é definido como semanal. Especifique nomes de cadeia de caracteres completos, como ' segunda-feira '.  Você também pode especificar mais de um nome de dia, separados por pipe. Por exemplo, N'Monday | Quarta-feira | Sexta-feira.  
  
 @backup_begin_time  
 A hora de início da janela de backup. Os backups não serão iniciados fora da janela de tempo, que é definida por uma @backup_begin_time combinação @backup_durationde e.  
  
 @backup_duration  
 A duração da janela de tempo de backup. Observe que não há nenhuma garantia de que os backups serão concluídos durante a janela @backup_begin_time de @backup_durationtempo definida por e. As operações de backup iniciadas nesta janela de tempo, mas excederem a duração da janela, não serão canceladas.  
  
 @log_backup_freq  
 Isso determina a frequência dos backups de log de transações. Esses backups ocorrem em intervalos regulares, e não no agendamento especificado para os backups de banco de dados. @log_backup_freqpode ser em minutos ou horas e `0:00` é válido, o que indica que não há backups de log. Desabilitar backups de log só seria apropriado para bancos de dados com um modelo de recuperação simples.  
  
> [!NOTE]  
>  Se o modelo de recuperação mudar de simples para completo, você precisará reconfigurar o log_backup_freq `0:00` de para um valor diferente de zero.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados **db_backupoperator** , com permissões **ALTER ANY Credential** e permissões **Execute** em **sp_delete_backuphistory** procedimento armazenado.  
  
## <a name="see-also"></a>Consulte Também  
 [managed_backup. sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
