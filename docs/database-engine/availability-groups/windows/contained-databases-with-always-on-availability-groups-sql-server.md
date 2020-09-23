---
title: Usar bancos de dados independentes com grupos de disponibilidade
description: Saiba mais sobre como usar um banco de dados independente com grupos de disponibilidade Always On no SQL Server 2019 (15.x).
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- contained database, AlwaysOnAvailabilityGroups
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 19905877e4651a2f2372c521cc09839abe938d68
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116987"
---
# <a name="use-contained-databases-with-always-on-availability-groups"></a>Usar bancos de dados independentes com Grupos de Disponibilidade AlwaysOn 
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Este tópico contém informações sobre como usar um banco de dados independente com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Antes de adicionar um banco de dados independente a um grupo de disponibilidade, verifique se a opção de servidor **autenticação de banco de dados independente** está definida como **1** em cada instância de servidor que hospeda uma réplica de disponibilidade do grupo de disponibilidade. Para obter mais informações, veja [Opção contained database authentication de configuração de servidor](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md) e [Opções de configuração do servidor &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Opções de configuração do servidor &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Bancos de dados independentes](../../../relational-databases/databases/contained-databases.md)  
  
  
