---
title: O estado de sincronização de dados de um banco de dados de disponibilidade não está íntegro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.drp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 89f95d15-33c6-4768-bccd-9dbf8c4f49a9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 45f1479d96838ce69a7bde35cd2a2fbd9c7e684d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62814244"
---
# <a name="data-synchronization-state-of-some-availability-database-is-not-healthy"></a>O estado de sincronização de dados de algum banco de dados de disponibilidade não é íntegro
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Sincronização de Dados de Réplicas de Disponibilidade|  
|**Problema**|O estado de sincronização de dados de algum banco de dados de disponibilidade não é íntegro.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Réplica de disponibilidade|  
  
## <a name="description"></a>DESCRIÇÃO  
 Esta política verifica o estado de sincronização de dados do banco de dados de disponibilidade (também conhecido como "réplica de banco de dados"). A política está em um estado não íntegro quando o estado de sincronização dos dados é NOT SYNCHRONIZING ou o estado da réplica de banco de dados de confirmação síncrona não é SYNCHRONIZED.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [O estado de sincronização de dados do banco de dados de disponibilidade não é íntegro](https://go.microsoft.com/fwlink/p/?LinkId=220863) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Possíveis causas  
 Pelo menos um banco de dados de disponibilidade na réplica está em estado de sincronização de dados não íntegro. Se essa for uma réplica de disponibilidade de confirmação de sincronização, todos os bancos de dados de disponibilidade devem estar no estado SYNCHRONIZING. Se for uma réplica de disponibilidade da confirmação síncrona, todos os bancos de dados de disponibilidade deverão estar no estado SYNCHRONIZED. Esse problema pode ter sido causado pelo seguinte:  
  
-   A réplica de disponibilidade pode estar desconectada.  
  
-   A movimentação de dados pode estar suspensa.  
  
-   O banco de dados pode não estar acessível.  
  
-   Pode haver um problema de atraso temporário devido à latência de rede ou à carga na réplica primária ou secundária.  
  
## <a name="possible-solution"></a>Solução possível  
 Resolva os problemas de suspensão de conexão ou movimentação de dados. Verifique os eventos desse problema usando o SQL Server Management Studio e localize o erro do banco de dados. Siga as etapas de solução de problemas do erro específico.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Use o painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
