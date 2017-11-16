---
title: "Backups do log de transações (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server[
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
caps.latest.revision: "52"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 22d43525383511ac5af79b9b356c280478c79d28
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="transaction-log-backups-sql-server"></a>Backups de log de transações (SQL Server)
  Este tópico é relevante apenas para bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estejam usando modelos de recuperação completa ou bulk-logged. Este tópico descreve o backup do log de transações de um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Você deve ter pelo menos criado um backup completo antes de criar qualquer backup de log. Depois disso, o backup do log de transações pode ser feito a qualquer momento, exceto durante outro backup de log. 
 
Recomendamos que você faça backups de log com frequência para minimizar exposição à perda de trabalho e para truncar o log de transações. 
 
Em geral, um administrador de banco de dados cria um backup completo de banco de dados ocasionalmente, como semanalmente, e, como opção, cria uma série de backups de banco de dados diferencial em um intervalo mais curto, como diariamente. Independentemente dos backups de banco de dados, o administrador de banco de dados faz backup do log de transações em intervalos frequentes, como a cada 10 minutos. Para determinado tipo de backup, o intervalo ideal entre backups depende de fatores como importância dos dados, tamanho do banco de dados e carga de trabalho do servidor.  
   
##  <a name="LogBackupSequence"></a> Como funciona uma sequência de backups de log  
 A sequência de backups de log de transações *log chain* é independente dos backups de dados. Por exemplo, suponha a sequência de eventos a seguir.  
  
|Hora|Evento|  
|----------|-----------|  
|8:00h|Backup do banco de dados.|  
|Meio-dia|Backup de log de transações.|  
|16:00h|Backup de log de transações.|  
|18:00h|Backup do banco de dados.|  
|20:00h|Backup de log de transações.|  
  
 O backup do log de transações criado às 20h contém registros de logs de transações de 16h até 20h, abrangendo a hora de conclusão do backup completo do banco de dados criado às 18h. A sequência de backups de logs de transações é a continuação do backup completo de banco de dados inicial criado às 8h até o último backup do log de transações criado às 20h. Para obter informações sobre como aplicar esses backups de log, veja o exemplo [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
##  <a name="Recommendations"></a> Recomendações  
  
-   Se um log de transações estiver danificado, o trabalho executado desde o backup válido mais recente será perdido. Portanto, recomendamos enfaticamente que você coloque seus arquivos de log em um armazenamento tolerante a falhas.  
  
-   Se um banco de dados for danificado ou se você estiver a ponto de restaurar o banco de dados, recomendamos que você crie um [backup da parte final do log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) para permitir a restauração do banco de dados até o momento atual.  
  
-   Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup do log com muita frequência, essas mensagens de êxito se acumularão muito rapidamente, resultando em logs de erros imensos que podem dificultar a localização de outras mensagens. Em tais situações, você pode suprimir essas entradas de log usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para criar um backup de log de transações**  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 Para agendar trabalhos de backup, consulte [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  

## <a name="see-also"></a>Consulte também  
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
