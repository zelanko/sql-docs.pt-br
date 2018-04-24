---
title: Opção de configuração de servidor SMO and DMO XPs | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6922050ae1ff3451c6484319fced5973a416a460
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>Opção de configuração de servidor XPs SMO e DMO
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção SMO e DMO XPs para habilitar os procedimentos armazenados estendidos do SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object) neste servidor.  
  
 Observe que começando pelo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o DMO foi removido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os possíveis valores são descritos na tabela seguinte:  
  
|Valor|Significado|  
|-----------|-------------|  
|0|Os SMO XPs não estão disponíveis.|  
|1|Os SMO XPs estão disponíveis. Esse é o padrão.|  
  
 A configuração é efetuada imediatamente.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir habilita os procedimentos armazenados estendidos do SMO.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Guia de Programação do SMO &#40;SQL Server Management Objects&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
