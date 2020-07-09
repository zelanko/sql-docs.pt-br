---
title: Descarregar backups para réplica de grupo de disponibilidade secundária
description: Saiba mais sobre os diferentes tipos de backup compatíveis com o descarregamento de backups em uma réplica secundária de um grupo de disponibilidade Always On.
ms.custom: seo-lt-2019
ms.date: 09/01/2017
ms.prod: sql
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
ms.openlocfilehash: 4a9f6aea0fe042752c5443d1de9b200494f57828
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895426"
---
# <a name="offload-supported-backups-to-secondary-replicas-of-an-availability-group"></a>Descarregar backups com suporte nas réplicas secundárias de um grupo de disponibilidade
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Os recursos secundários ativos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] incluem suporte para executar backups em réplicas secundárias. As operações de backup podem colocar tensão significativa na E/S e na CPU (com compactação de backup). O descarregamento de backups em uma réplica secundária sincronizada ou em sincronização permite usar os recursos na instância do servidor que hospeda a réplica primária para suas cargas de trabalho de camada-1.  

> [!NOTE]  
>  As instruções RESTORE não são permitidas em nenhum dos bancos de dados primários ou secundários de um grupo de disponibilidade.  
  
 
##  <a name="backup-types-supported-on-secondary-replicas"></a><a name="SupportedBuTypes"></a> Tipos de backup com suporte nas réplicas secundárias  
  
-   O **BACKUP DATABASE** é compatível apenas com backups completos somente cópia de bancos de dados, arquivos ou grupos de arquivos quando executado nas réplicas secundárias. Backups somente cópia não afetam a cadeia de logs nem limpam o bitmap diferencial.  
  
-   Não há suporte para backups diferenciais em réplicas secundárias.

-   Atualmente, não há suporte para backups simultâneos, como a execução de um backup de log de transações na réplica primária, enquanto um backup de banco de dados completo está em execução na réplica secundária. 
  
-   **BACKUP LOG** dá suporte apenas a backups de log regulares (não há suporte para a opção COPY_ONLY em backups de log nas réplicas secundárias).  
  
     Uma cadeia de logs consistente é garantida em backups de log feitos em qualquer uma das réplicas (primária ou secundária), independentemente de seu modo de disponibilidade (confirmação síncrona ou de confirmação assíncrona).  
  
-   Para fazer backup de um banco de dados secundário, uma réplica secundária deve ser capaz de se comunicar com a réplica primária e ser **SYNCHRONIZED** ou **SYNCHRONIZING**.  

Em um grupo de disponibilidade distribuída, os backups podem ser executados em réplicas secundárias no mesmo grupo de disponibilidade que a réplica primária ativa ou na réplica primária de quaisquer grupos de disponibilidade secundários. Os backups não podem ser executados em uma réplica secundária em um grupo de disponibilidade secundário, porque as réplicas secundárias se comunicam somente com a réplica primária em seu próprio grupo de disponibilidade. Apenas réplicas que se comunicam diretamente com a réplica primária global podem executar operações de backup.

##  <a name="configuring-where-backup-jobs-run"></a><a name="WhereBuJobsRun"></a> Configurando onde os trabalhos de backup são executados  
 A execução de backups em uma réplica secundária para descarregar a carga de trabalho do backup do servidor de produção primário é um grande benefício. No entanto, a execução de backups em réplicas secundárias introduz uma complexidade significativa no processo de determinação de onde os trabalhos de backup devem ser executados. Para resolver isto, configure onde os trabalhos de backup são executados, da seguinte maneira:  
  
1.  Configure o grupo de disponibilidade para especificar em quais réplicas de disponibilidade você prefere que os backups sejam executados. Para obter mais informações, confira os parâmetros *AUTOMATED_BACKUP_PREFERENCE* e *BACKUP_PRIORITY* em [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md) ou [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
2.  Crie trabalhos de backup com script para cada banco de dados de disponibilidade em cada instância de servidor que hospeda uma réplica de disponibilidade que é candidata a executar backups. Para obter mais informações, confira a seção “Acompanhamento: Depois de configurar o backup em réplicas secundárias” de [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar o backup em réplicas secundárias**  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 **Para determinar se a réplica atual é a réplica de backup preferencial**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
  
 **Para criar um trabalho de backup**  
  
-   [Usar o Assistente de Plano de Manutenção](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [Implementar trabalhos](../../../ssms/agent/implement-jobs.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Backups somente cópia &#40;SQL Server&#41;](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
