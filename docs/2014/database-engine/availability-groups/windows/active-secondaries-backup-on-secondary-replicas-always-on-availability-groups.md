---
title: 'Secundárias ativas: Backup em réplicas secundárias (grupos de disponibilidade) Always On | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 82afe51b-71d1-4d5b-b20a-b57afc002405
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a94db154042f2cc6314459b6af4b52a43c2c9966
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186966"
---
# <a name="active-secondaries-backup-on-secondary-replicas-always-on-availability-groups"></a>Secundárias ativas: backup em réplicas secundárias (Grupos de Disponibilidade AlwaysOn)
  Os recursos secundários ativos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] incluem suporte para execução de operações de backup em réplicas secundárias. As operações de backup podem colocar tensão significativa na E/S e na CPU (com compactação de backup). O descarregamento de backups em uma réplica secundária sincronizada ou em sincronização permite usar os recursos na instância do servidor que hospeda a réplica primária para suas cargas de trabalho de camada-1.  
  
> [!NOTE]  
>  As instruções RESTORE não são permitidas em nenhum dos bancos de dados primários ou secundários de um grupo de disponibilidade.  
  
  
  
##  <a name="SupportedBuTypes"></a> Tipos de backup com suporte nas réplicas secundárias  
  
-   `BACKUP DATABASE` só oferece suporte a backups completos somente cópia de bancos de dados, de arquivos ou de grupos de arquivos quando executado em réplicas secundárias. Observe que os backups somente cópia não afetam a cadeia de logs nem limpam o bitmap diferencial.  
  
-   Não há suporte para backups diferenciais em réplicas secundárias.  
  
-   **BACKUP LOG** dá suporte apenas a backups de log regulares (não há suporte para a opção COPY_ONLY em backups de log nas réplicas secundárias).  
  
     Uma cadeia de logs consistente é garantida em backups de log feitos em qualquer uma das réplicas (primária ou secundária), independentemente de seu modo de disponibilidade (confirmação síncrona ou de confirmação assíncrona).  
  
-   Para fazer backup de um banco de dados secundário, uma réplica secundária deve ser capaz de se comunicar com a réplica primária e deve ser `SYNCHRONIZED` ou `SYNCHRONIZING`.  
  
##  <a name="WhereBuJobsRun"></a> Configurando onde os trabalhos de backup são executados  
 A execução de backups em uma réplica secundária para descarregar a carga de trabalho do backup do servidor de produção primário é um grande benefício. No entanto, a execução de backups em réplicas secundárias introduz uma complexidade significativa no processo de determinação de onde os trabalhos de backup devem ser executados. Para resolver isto, configure onde os trabalhos de backup são executados, da seguinte maneira:  
  
1.  Configure o grupo de disponibilidade para especificar em quais réplicas de disponibilidade você prefere que os backups sejam executados. Para obter mais informações, confira os parâmetros *AUTOMATED_BACKUP_PREFERENCE* e *BACKUP_PRIORITY* em [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql) ou [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql).  
  
2.  Crie trabalhos de backup com script para cada banco de dados de disponibilidade em cada instância de servidor que hospeda uma réplica de disponibilidade que é candidata a executar backups. Para obter mais informações, confira a seção “Acompanhamento: Depois de configurar o backup em réplicas secundárias” de [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar o backup em réplicas secundárias**  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
 **Para determinar se a réplica atual é a réplica de backup preferencial**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
  
 **Para criar um trabalho de backup**  
  
-   [Usar o Assistente de Plano de Manutenção](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [Implementar trabalhos](../../../ssms/agent/implement-jobs.md)  
  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Backups somente cópia &#40;SQL Server&#41;](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)  
  
  
