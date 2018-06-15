---
title: Backups do log de transações (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server]
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
caps.latest.revision: 52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 36142710470ed5fab6721d4fba8075dd056960fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32920161"
---
# <a name="transaction-log-backups-sql-server"></a>Backups de log de transações (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico é relevante apenas para bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estejam usando modelos de recuperação completa ou bulk-logged. Este tópico descreve o backup do log de transações de um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Você deve ter pelo menos criado um backup completo antes de criar qualquer backup de log. Depois disso, o backup do log de transações pode ser feito a qualquer momento, exceto durante outro backup de log. 
 
Recomendamos que você faça backups de log com frequência para minimizar exposição à perda de trabalho e para truncar o log de transações. 
 
Em geral, um administrador de banco de dados cria um backup completo de banco de dados ocasionalmente, como semanalmente, e, como opção, cria uma série de backups de banco de dados diferencial em um intervalo mais curto, como diariamente. Independentemente dos backups de banco de dados, o administrador de banco de dados faz backup do log de transações em intervalos frequentes. Para determinado tipo de backup, o intervalo ideal entre backups depende de fatores como importância dos dados, tamanho do banco de dados e carga de trabalho do servidor. Para obter mais informações sobre como implementar uma boa estratégia, consulte [Recomendações](#Recommendations) neste tópico. 
   
##  <a name="LogBackupSequence"></a> Como funciona uma sequência de backups de log  
 A sequência de backups de log de transações *log chain* é independente dos backups de dados. Por exemplo, suponha a sequência de eventos a seguir.  
  
|Hora|Evento|  
|----------|-----------|  
|8h|Backup do banco de dados.|  
|Meio-dia|Backup de log de transações.|  
|16h|Backup de log de transações.|  
|18h|Backup do banco de dados.|  
|20h|Backup de log de transações.|  
  
 O backup de log de transações criado às 20h contém registros do log de transações das 16h às 20h, abrangendo o tempo em que o backup completo de banco de dados foi criado às 18h. A sequência de backups de log de transações é contínua desde o backup completo de banco de dados inicial criado às 8h até o último backup de log de transações criado às 20h. Para obter informações sobre como aplicar esses backups de log, veja o exemplo [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
##  <a name="Recommendations"></a> Recomendações  
  
-   Se um log de transações estiver danificado, o trabalho executado desde o backup válido mais recente será perdido. Portanto, recomendamos enfaticamente que você coloque seus arquivos de log em um armazenamento tolerante a falhas.  
  
-   Se um banco de dados for danificado ou se você estiver a ponto de restaurar o banco de dados, recomendamos que você crie um [backup da parte final do log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) para permitir a restauração do banco de dados até o momento atual.  
  
-   Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup do log com muita frequência, essas mensagens de êxito se acumularão muito rapidamente, resultando em logs de erros imensos que podem dificultar a localização de outras mensagens. Em tais situações, você pode suprimir essas entradas de log usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  

-   Faça backups de log com frequência suficiente para dar suporte a seus requisitos empresariais, especificamente, a tolerância à perda de trabalho, que pode ser causada por um armazenamento de logs danificado. 
   -   A frequência apropriada para fazer backups de log depende de tolerância à exposição à perda de trabalho, equilibrada por quantos backups de log é possível armazenar, administrar e, potencialmente, restaurar. Pense no [RTO](http://wikipedia.org/wiki/Recovery_time_objective) e [RPO](http://wikipedia.org/wiki/Recovery_point_objective) necessários ao implementar sua estratégia de recuperação e, especificamente, na cadência de backup de log.
   -   Fazer um backup de log a cada 15 a 30 minutos deve ser o bastante. Se o seu negócio requer que você reduza ao mínimo a exposição à perda de trabalho, considere fazer backups de log com mais frequência. Backups de log mais frequentes têm a vantagem adicional de aumentar a frequência de truncamentos de log, resultando em arquivos de log menores.  
  
> [!IMPORTANT]
> Para limitar o número de backups de log que você precisa restaurar, é essencial fazer backup dos dados com frequência. Por exemplo, convém programar um backup de banco de dados completo por semana e backups de diferenciais de banco de dados diariamente.  
> Mais uma vez, pense no [RTO](http://wikipedia.org/wiki/Recovery_time_objective) e [RPO](http://wikipedia.org/wiki/Recovery_point_objective) necessários ao implementar sua estratégia de recuperação e, especificamente, na cadência de backup completo e diferencial de banco de dados.
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para criar um backup de log de transações**  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 Para agendar trabalhos de backup, consulte [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  

## <a name="see-also"></a>Consulte Também  
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Guia de gerenciamento e arquitetura de backups de log de transações no log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)     
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
