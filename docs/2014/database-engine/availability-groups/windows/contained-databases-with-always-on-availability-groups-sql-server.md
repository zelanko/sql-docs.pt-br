---
title: Bancos de dados independentes com Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- contained database [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 13dd6e87b6442b8c1b908ceb73d1e5c7f135308c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62815326"
---
# <a name="contained-databases-with-always-on-availability-groups-sql-server"></a>Bancos de dados independentes com grupos de disponibilidade AlwaysOn (SQL Server)
  Este tópico contém informações sobre como usar um banco de dados independente com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 **Neste tópico:**  
  
-   [Pré-requisitos](#Prerequisites)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Antes de adicionar um banco de dados independente a um grupo de disponibilidade, verifique se a opção de servidor `contained database authentication` está definida como `1` em cada instância de servidor que hospeda uma réplica de disponibilidade do grupo de disponibilidade. Para obter mais informações, veja [Opção contained database authentication de configuração de servidor](../../configure-windows/contained-database-authentication-server-configuration-option.md) e [Opções de configuração do servidor &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Opções de configuração do servidor &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Bancos de dados independentes](../../../relational-databases/databases/contained-databases.md)  
  
  
