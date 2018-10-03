---
title: Aplicar backups do log de transações (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], log backups
- transaction log backups [SQL Server], applying backups
- online restores [SQL Server], log backups
- transaction log backups [SQL Server], quantity needed for restore sequence
- backups [SQL Server], log backups
ms.assetid: 9b12be51-5469-46f9-8e86-e938e10aa3a1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7532f2a6f2c50f53e5af01c2cec979170b493147
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169386"
---
# <a name="apply-transaction-log-backups-sql-server"></a>Aplicar backups de log de transações (SQL Server)
  O tópico só é relevante para o modelo de recuperação completa ou modelo de recuperação bulk-logged.  
  
 Este tópico descreve a aplicação de backups de log de transações como parte da restauração de um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Neste tópico:**  
  
-   [Requisitos para restaurar os Backups de Log de transações](#Requirements)  
  
-   [Recuperação e Logs de transações](#RecoveryAndTlogs)  
  
-   [Usando Backups de Log para restaurar até o ponto de falha](#PITrestore)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="Requirements"></a> Requisitos para restaurar os Backups de Log de transações  
 Para aplicar um backup de log de transações, devem ser atendidos os seguintes requisitos:  
  
-   **Backups de log suficientes para uma sequência de restauração:** você deverá ter backups de registros de log suficientes para concluir uma sequência de restauração. Os backups de log necessários, incluindo o [backup da parte final do log](tail-log-backups-sql-server.md) , quando necessário, devem estar disponíveis antes do início da sequência de restauração.  
  
-   **Ordem de restauração correta:**  o backup de banco de dados completo imediatamente anterior ou backup de banco de dados diferencial deve ser restaurado primeiro. Em seguida, todos os logs de transações criados após o backup de banco de dados completo ou diferencial devem ser restaurados em ordem cronológica. Se um backup de log de transações nessa cadeia de logs for perdido ou danificado, você poderá restaurar apenas os logs de transações anteriores ao log ausente.  
  
-   **Banco de dados ainda não recuperado:**  o banco de dados não poderá ser recuperado até que o log de transações final seja aplicado. Se você recuperar o banco de dados depois de restaurar um dos backups de log de transações intermediários antes do final da cadeia de logs, não poderá restaurar o banco de dados além desse ponto sem restaurar a sequência completa, começando com o backup de banco de dados completo.  
  
    > [!TIP]  
    >  Uma prática recomendada é restaurar todos os backups de log (RESTORE LOG *database_name* WITH NORECOVERY). Em seguida, depois de restaurar o último backup de log, recupere o banco de dados em uma operação separada (RESTORE DATABASE *database_name* WITH RECOVERY).  
  
##  <a name="RecoveryAndTlogs"></a> Recuperação e Logs de transações  
 Ao concluir a operação de restauração e recuperar o banco de dados, a recuperação reverte todas as transações incompletas. Isso é conhecido como o *fase Desfazer*. A reversão é necessária para restaurar a integridade do banco de dados. Depois da reversão, o banco de dados fica online e mais nenhum backup de log de transações pode ser aplicado ao banco de dados.  
  
 Por exemplo, uma série de backups de log de transações contém uma transação de execução longa. O início da transação é registrado no primeiro backup de log de transações, mas o término da transação é registrado no segundo backup de log de transações. Não há registro de uma operação de confirmação ou reversão no primeiro backup de log de transações. Se uma operação de recuperação for executada quando o primeiro backup de log de transações for aplicado, a transação de longa execução será tratada como incompleta e as modificações de dados registradas no primeiro backup de log de transações serão revertidas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite que o segundo backup de log de transação seja aplicado depois deste ponto.  
  
> [!NOTE]  
>  Em algumas circunstâncias, você pode adicionar um arquivo explicitamente durante a restauração do log.  
  
##  <a name="PITrestore"></a> Usando Backups de Log para restaurar até o ponto de falha  
 Considere a seguinte sequência de eventos.  
  
|Hora|Evento|  
|----------|-----------|  
|8:00h|Faça um backup do banco de dados para criar um backup completo do banco de dados.|  
|Meio-dia|Backup de log de transações.|  
|16:00h|Backup de log de transações.|  
|18:00h|Faça um backup do banco de dados para criar um backup completo do banco de dados.|  
|20:00h|Backup de log de transações.|  
|21h45|Ocorre falha.|  
  
> [!NOTE]  
>  Para obter uma explicação dessa sequência de exemplo de backups, veja [Backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md).  
  
 Para restaurar o banco de dados a seu estado às 21h45 (o ponto de falha), um dos seguintes procedimentos alternativos pode ser usado.  
  
 **Alternativa 1: Restaure o banco de dados usando o backup de banco de dados completo mais recente**  
  
1.  Crie um backup do final do log de transações atualmente ativo a partir do ponto de falha.  
  
2.  Não restaure o backup de banco de dados completo das 8h 18h. Restaure o backup de banco de dados completo mais recente das 18h e aplique o backup de log das 20h e o backup da parte final do log.  
  
 **Alternativa 2: Restaure o banco de dados usando o backup de banco de dados completo mais antigo**  
  
> [!NOTE]  
>  Esse processo alternativo será útil se um problema impedir o uso do backup de banco de dados completo 18h. Esse processo leva mais muito tempo do que restaurar o backup de banco de dados completo das 18h.  
  
1.  Crie um backup do final do log de transações atualmente ativo a partir do ponto de falha.  
  
2.  Restaure o backup de banco de dados completo das 8h e, depois, restaure todos os quatro backups de log de transações em sequência. Isso efetua roll forward de todas as transações completas até 21h45.  
  
     Essa alternativa mostra a segurança redundante oferecida pela manutenção de uma cadeia de backups de log de transações em uma série de backups de banco de dados completos.  
  
> [!NOTE]  
>  Em alguns casos, você pode usar também logs de transações para restaurar um banco de dados até um point-in-time específico. Para obter mais informações, veja [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para aplicar um backup de log de transações**  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
 **Para restaurar até seu ponto de recuperação**  
  
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
-   [Recuperação de bancos de dados relacionados que contêm transação marcada](recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [Recuperar para um número de sequência de log &#40;SQL Server&#41;](recover-to-a-log-sequence-number-sql-server.md)  
  
 **Para recuperar um banco de dados depois de restaurar backups usando WITH NORECOVERY**  
  
-   [Recuperar um banco de dados sem restaurar dados &#40;Transact-SQL&#41;](recover-a-database-without-restoring-data-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [O log de transações &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)  
  
  
