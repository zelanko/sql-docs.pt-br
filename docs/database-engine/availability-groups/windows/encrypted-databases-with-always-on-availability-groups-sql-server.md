---
title: Adicionar um banco de dados criptografado a um grupo de disponibilidade
description: Conheça as etapas necessárias para adicionar um banco de dados criptografado (ou recentemente descriptografado) a um grupo de disponibilidade Always On.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Transparent Data Encryption, AlwaysOn Availability Groups
- TDE, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 09eb6ebc-3051-4fff-86a5-93524507b1fc
author: cawrites
ms.author: chadam
ms.openlocfilehash: 2569f44e4642df714c8108b6540b81d013d30b82
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584288"
---
# <a name="add-an-encrypted-database-to-an-always-on-availability-group"></a>Adicionar um banco de dados criptografado em um grupo de disponibilidade Always On
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Este tópico contém informações sobre como o usar bancos de dados atualmente criptografados ou recentemente descriptografados com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 
##  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Se um banco de dados estiver criptografado ou contiver até mesmo uma DEK (chave de criptografia de banco de dados), você não poderá usar o [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] nem o [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] para adicionar um grupo de disponibilidade. Mesmo se um banco de dados criptografado for descriptografado, seus backups de log poderão conter dados criptografados. Nesse caso, a total sincronização inicial de dados poderia falhar no banco de dados. Isso é porque a operação de log de restauração pode exigir o certificado que foi usado pelas DEKs (chaves de criptografia de banco de dados), e esse certificado pode não estar disponível.  
  
     Para tornar um banco de dados descriptografado elegível para adição a um grupo de disponibilidade usando o assistente:  
  
    1.  Crie um backup de log do banco de dados primário.  
  
    2.  Crie um backup completo do banco de dados primário.  
  
    3.  Restaure o backup do banco de dados na instância de servidor que hospeda a réplica secundária.  
  
    4.  Crie um novo backup de log a partir do banco de dados primário.  
  
    5.  Restaure esse backup de log no banco de dados secundário.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [TDE &#40;Transparent Data Encryption&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
