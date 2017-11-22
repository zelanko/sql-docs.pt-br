---
title: "Secundárias ativas: backup em réplicas secundárias – disponibilidade AlwaysOn | Microsoft Docs"
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 82afe51b-71d1-4d5b-b20a-b57afc002405
caps.latest.revision: "34"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 7bdc1156dc782aab3e2cd244c1ca6b318015089e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="active-secondaries-backup-on-secondary-replicas-always-on-availability-groups"></a>Secundárias ativas: backup em réplicas secundárias (Grupos de Disponibilidade AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Os recursos secundários ativos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] incluem suporte para execução de operações de backup em réplicas secundárias. As operações de backup podem colocar tensão significativa na E/S e na CPU (com compactação de backup). O descarregamento de backups em uma réplica secundária sincronizada ou em sincronização permite usar os recursos na instância do servidor que hospeda a réplica primária para suas cargas de trabalho de camada-1.  

> [!NOTE]  
>  As instruções RESTORE não são permitidas em nenhum dos bancos de dados primários ou secundários de um grupo de disponibilidade.  
  
-   [Tipos de backup com suporte](#SupportedBuTypes)  
  
-   [Configurando onde os trabalhos de backup são executados](#WhereBuJobsRun)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="SupportedBuTypes"></a> Tipos de backup com suporte nas réplicas secundárias  
  
-   **BACKUP DATABASE** dá suporte apenas a backups completos somente cópia de bancos de dados, arquivos ou grupos de arquivos quando executado nas réplicas secundárias. Observe que os backups somente cópia não afetam a cadeia de logs nem limpam o bitmap diferencial.  
  
-   Não há suporte para backups diferenciais em réplicas secundárias.  
  
-   **BACKUP LOG** dá suporte apenas a backups de log regulares (não há suporte para a opção COPY_ONLY em backups de log nas réplicas secundárias).  
  
     Uma cadeia de logs consistente é garantida em backups de log feitos em qualquer uma das réplicas (primária ou secundária), independentemente de seu modo de disponibilidade (confirmação síncrona ou de confirmação assíncrona).  
  
-   Para fazer backup de um banco de dados secundário, uma réplica secundária deve ser capaz de se comunicar com a réplica primária e ser **SYNCHRONIZED** ou **SYNCHRONIZING**.  

Em um grupo de disponibilidade distribuída, os backups podem ser executados em réplicas secundárias no mesmo grupo de disponibilidade que a réplica primária ativa ou na réplica primária de quaisquer grupos de disponibilidade secundários. Os backups não podem ser executados em uma réplica secundária em um grupo de disponibilidade secundário, porque as réplicas secundárias se comunicam somente com a réplica primária em seu próprio grupo de disponibilidade. Apenas réplicas que se comunicam diretamente com a réplica primária global podem executar operações de backup.

##  <a name="WhereBuJobsRun"></a> Configurando onde os trabalhos de backup são executados  
 A execução de backups em uma réplica secundária para descarregar a carga de trabalho do backup do servidor de produção primário é um grande benefício. No entanto, a execução de backups em réplicas secundárias introduz uma complexidade significativa no processo de determinação de onde os trabalhos de backup devem ser executados. Para resolver isto, configure onde os trabalhos de backup são executados, da seguinte maneira:  
  
1.  Configure o grupo de disponibilidade para especificar em quais réplicas de disponibilidade você prefere que os backups sejam executados. Para obter mais informações, confira os parâmetros *AUTOMATED_BACKUP_PREFERENCE* e *BACKUP_PRIORITY* em [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md) ou [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
2.  Crie trabalhos de backup com script para cada banco de dados de disponibilidade em cada instância de servidor que hospeda uma réplica de disponibilidade que é candidata a executar backups. Para obter mais informações, confira a seção “Acompanhamento: Depois de configurar o backup em réplicas secundárias” de [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar o backup em réplicas secundárias**  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 **Para determinar se a réplica atual é a réplica de backup preferencial**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
  
 **Para criar um trabalho de backup**  
  
-   [Usar o Assistente de Plano de Manutenção](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [Implementar trabalhos](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Backups somente cópia &#40;SQL Server&#41;](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
