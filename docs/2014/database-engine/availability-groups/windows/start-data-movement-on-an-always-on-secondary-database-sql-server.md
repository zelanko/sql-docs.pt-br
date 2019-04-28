---
title: Iniciar movimentação de dados em um banco de dados secundário AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], databases
ms.assetid: 498eb3fb-6a43-434d-ad95-68a754232c45
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b0626ce7dee34ed21aad3e902e3c3f555f27ab97
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813549"
---
# <a name="start-data-movement-on-an-alwayson-secondary-database-sql-server"></a>Iniciar movimentação de dados em um banco de dados secundário AlwaysOn (SQL Server)
  Este tópico contém informações sobre como iniciar a sincronização de dados depois que você adiciona um banco de dados a um grupo de disponibilidade AlwaysOn. Para cada nova réplica primária, bancos de dados secundários devem ser preparados nas instâncias do servidor que hospedam as réplicas secundárias. Em seguida, cada um destes bancos de dados secundários deve ser unido manualmente ao grupo de disponibilidade.  
  
> [!NOTE]  
>  Se os caminhos de arquivos forem idênticos em cada instância do servidor que hospeda uma réplica de disponibilidade para um grupo de disponibilidade, o [Assistente de Novo Grupo de Disponibilidade](use-the-availability-group-wizard-sql-server-management-studio.md), [Assistente para Adicionar Réplica ao Grupo de Disponibilidade](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)ou [Assistente para Adicionar Banco de dados ao Grupo de Disponibilidade](availability-group-add-database-to-group-wizard.md) poderá iniciar a sincronização de dados automaticamente para você.  
  
 Para iniciar a sincronização de dados manualmente, você precisa conectar-se a cada instância de servidor, uma por vez, que está hospedando uma réplica secundária para o grupo de disponibilidade e concluir as seguintes etapas:  
  
1.  Restaure os backups atuais de cada banco de dados primário e seu log de transações (usando RESTORE WITH NORECOVERY). Você pode usar qualquer uma das seguintes abordagens alternativas:  
  
    -   Restaurar manualmente um backup recente do banco de dados primário usando RESTORE WITH NORECOVERY e, em seguida, restaurar cada backup de log subsequente usando RESTORE WITH NORECOVERY. Executar essa sequência de restauração em cada instância do servidor que hospeda uma réplica secundária para o grupo de disponibilidade.  
  
         **Para obter mais informações, consulte:**  
  
         [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
    -   Se você estiver adicionando um ou mais bancos de dados primários de envio de logs a um grupo de disponibilidade, poderá ser capaz de migrar um ou mais dos bancos de dados secundários correspondentes de envio de logs para Grupos de Disponibilidade AlwaysOn. Migrar um banco de dados secundário de envio de logs exige que se use o mesmo nome de banco de dados que o banco de dados primário e que ele resida em uma instância de servidor que esteja hospedando uma réplica secundária para o grupo de disponibilidade. Além disso, o grupo de disponibilidade deve ser configurado de forma que a réplica primária seja preferida para backups e seja um candidato para realizar backups (quer dizer, ele tem uma prioridade de backup que é >0). Quando o trabalho de backup estiver sendo executado no banco de dados primário, você precisará desabilitar o trabalho de backup e, assim que o trabalho de restauração tiver sido executado em um determinado banco de dados secundário, você precisará desabilitar o trabalho de restauração.  
  
        > [!NOTE]  
        >  Depois que você criar todos os bancos de dados secundários para o grupo de disponibilidade, se você desejar executar backups em réplicas secundárias, precisará reconfigurar a preferência de backup automatizada do grupo de disponibilidade.  
  
         **Para obter mais informações, consulte:**  
  
         [Pré-requisitos para migrar de envio de logs para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-migrating-log-shipping-to-always-on-availability-groups.md)  
  
         [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
2.  O mais rápido possível, una cada banco de dados secundário recém-preparado ao grupo de disponibilidade.  
  
     **Para obter mais informações, consulte:**  
  
     [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
##  <a name="LaunchWiz"></a> Tarefas relacionadas  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
