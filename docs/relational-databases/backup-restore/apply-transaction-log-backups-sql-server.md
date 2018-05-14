---
title: Aplicar backups do log de transações (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/13/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], log backups
- transaction log backups [SQL Server], applying backups
- online restores [SQL Server], log backups
- transaction log backups [SQL Server], quantity needed for restore sequence
- backups [SQL Server], log backups
ms.assetid: 9b12be51-5469-46f9-8e86-e938e10aa3a1
caps.latest.revision: 38
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b1b8fff95c58785e48199bd3ce4bc65d3c87f293
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="apply-transaction-log-backups-sql-server"></a>Aplicar backups de log de transações (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O tópico só é relevante para o modelo de recuperação completa ou modelo de recuperação bulk-logged.  
  
 Este tópico descreve a aplicação de backups de log de transações como parte da restauração de um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
 
  
##  <a name="Requirements"></a> Requisitos para restaurar backups de log de transação  
 Para aplicar um backup de log de transações, devem ser atendidos os seguintes requisitos:  
  
-   **Backups de log suficientes para uma sequência de restauração:** você deverá ter backups de registros de log suficientes para concluir uma sequência de restauração. Os backups de log necessários, incluindo o [backup da parte final do log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) , quando necessário, devem estar disponíveis antes do início da sequência de restauração.  
  
-   **Ordem de restauração correta:**  o backup de banco de dados completo imediatamente anterior ou backup de banco de dados diferencial deve ser restaurado primeiro. Em seguida, todos os logs de transações criados após o backup de banco de dados completo ou diferencial devem ser restaurados em ordem cronológica. Se um backup de log de transações nessa cadeia de logs for perdido ou danificado, você poderá restaurar apenas os logs de transações anteriores ao log ausente.  
  
-   **Banco de dados ainda não recuperado:**  o banco de dados não poderá ser recuperado até que o log de transações final seja aplicado. Se você recuperar o banco de dados depois de restaurar um dos backups de log de transações intermediários antes do final da cadeia de logs, não poderá restaurar o banco de dados além desse ponto sem restaurar a sequência completa, começando com o backup de banco de dados completo.  
  
    > **DICA!** Uma prática recomendada é restaurar todos os backups de log (RESTORE LOG *database_name* WITH NORECOVERY). Em seguida, depois de restaurar o último backup de log, recupere o banco de dados em uma operação separada (RESTORE DATABASE *database_name* WITH RECOVERY).  
  
##  <a name="RecoveryAndTlogs"></a> Recuperação e logs de transações  
 Ao concluir a operação de restauração e recuperar o banco de dados, a recuperação reverte todas as transações incompletas. Isso é conhecido como o *fase Desfazer*. A reversão é necessária para restaurar a integridade do banco de dados. Depois da reversão, o banco de dados fica online e mais nenhum backup de log de transações pode ser aplicado ao banco de dados.  
  
 Por exemplo, uma série de backups de log de transações contém uma transação de execução longa. O início da transação é registrado no primeiro backup de log de transações, mas o término da transação é registrado no segundo backup de log de transações. Não há registro de uma operação de confirmação ou reversão no primeiro backup de log de transações. Se uma operação de recuperação for executada quando o primeiro backup de log de transações for aplicado, a transação de longa execução será tratada como incompleta e as modificações de dados registradas no primeiro backup de log de transações serão revertidas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite que o segundo backup de log de transação seja aplicado depois deste ponto.  
  
> **OBSERVAÇÃO:** em algumas circunstâncias, você pode adicionar um arquivo explicitamente durante a restauração do log.  
  
##  <a name="PITrestore"></a> Usar backups de log para restaurar até o ponto de falha  
 Considere a seguinte sequência de eventos.  
  
|Hora|Evento|  
|----------|-----------|  
|8:00h|Faça um backup do banco de dados para criar um backup completo do banco de dados.|  
|Meio-dia|Backup de log de transações.|  
|16:00h|Backup de log de transações.|  
|18:00h|Faça um backup do banco de dados para criar um backup completo do banco de dados.|  
|20:00h|Backup de log de transações.|  
|21h45|Ocorre falha.|  
  
> **OBSERVAÇÃO:** para obter uma explicação dessa sequência de exemplo de backups, consulte [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 Para restaurar o banco de dados a seu estado às 21h45 (o ponto de falha), um dos seguintes procedimentos alternativos pode ser usado.  
  
 **Alternativa 1: Restaure o banco de dados usando o backup de banco de dados completo mais recente**  
  
1.  Crie um backup do final do log de transações atualmente ativo a partir do ponto de falha.  
  
2.  Não restaure o backup de banco de dados completo das 8h 18h. Restaure o backup de banco de dados completo mais recente das 18h e aplique o backup de log das 20h e o backup da parte final do log.  
  
 **Alternativa 2: Restaure o banco de dados usando o backup de banco de dados completo mais antigo**  
  
> **OBSERVAÇÃO:** esse processo alternativo será útil se um problema impedir o uso do backup às 18h. 18h. Esse processo leva mais muito tempo do que restaurar o backup de banco de dados completo das 18h.  
  
1.  Crie um backup do final do log de transações atualmente ativo a partir do ponto de falha.  
  
2.  Restaure o backup de banco de dados completo das 8h e, depois, restaure todos os quatro backups de log de transações em sequência. Isso efetua roll forward de todas as transações completas até 21h45.  
  
     Essa alternativa mostra a segurança redundante oferecida pela manutenção de uma cadeia de backups de log de transações em uma série de backups de banco de dados completos.  
  
> **OBSERVAÇÃO:** em alguns casos, você também pode usar logs de transações para restaurar um banco de dados até um ponto específico. Para obter mais informações, veja [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para aplicar um backup de log de transações**  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
 **Para restaurar até seu ponto de recuperação**  
  
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
-   [Recuperação de bancos de dados relacionados que contêm transação marcada](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [Recuperar para um número de sequência de log &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)  
  
 **Para recuperar um banco de dados depois de restaurar backups usando WITH NORECOVERY**  
  
-   [Recuperar um banco de dados sem restaurar dados &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
## <a name="see-also"></a>Confira também  
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
