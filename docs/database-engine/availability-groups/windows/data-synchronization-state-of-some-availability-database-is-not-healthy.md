---
title: O estado de sincronização de dados de um banco de dados de disponibilidade não está íntegro | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.drp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 89f95d15-33c6-4768-bccd-9dbf8c4f49a9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f9260f9de24d282b3b6ce5c4e46b4572e01aafa9
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604447"
---
# <a name="data-synchronization-state-of-some-availability-database-is-not-healthy"></a>O estado de sincronização de dados de algum banco de dados de disponibilidade não é íntegro
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Sincronização de Dados de Réplicas de Disponibilidade|  
|**Problema**|O estado de sincronização de dados de algum banco de dados de disponibilidade não é íntegro.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Réplica de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Esta política verifica o estado de sincronização de dados do banco de dados de disponibilidade (também conhecido como "réplica de banco de dados"). A política está em um estado não íntegro quando o estado de sincronização dos dados é NOT SYNCHRONIZING ou o estado da réplica de banco de dados de confirmação síncrona não é SYNCHRONIZED.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [O estado de sincronização de dados do banco de dados de disponibilidade não é íntegro](https://go.microsoft.com/fwlink/p/?LinkId=220863) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Causas possíveis  
 Pelo menos um banco de dados de disponibilidade na réplica está em estado de sincronização de dados não íntegro. Se essa for uma réplica de disponibilidade de confirmação de sincronização, todos os bancos de dados de disponibilidade devem estar no estado SYNCHRONIZING. Se for uma réplica de disponibilidade da confirmação síncrona, todos os bancos de dados de disponibilidade deverão estar no estado SYNCHRONIZED. Esse problema pode ter sido causado pelo seguinte:  
  
-   A réplica de disponibilidade pode estar desconectada.  
  
-   A movimentação de dados pode estar suspensa.  
  
-   O banco de dados pode não estar acessível.  
  
-   Pode haver um problema de atraso temporário devido à latência de rede ou à carga na réplica primária ou secundária.  
  
## <a name="possible-solution"></a>Solução possível  
 Resolva os problemas de suspensão de conexão ou movimentação de dados. Verifique os eventos desse problema usando o SQL Server Management Studio e localize o erro do banco de dados. Siga as etapas de solução de problemas do erro específico.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
