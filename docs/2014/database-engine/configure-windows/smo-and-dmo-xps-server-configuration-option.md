---
title: Opção de configuração de servidor SMO and DMO XPs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f56e4f6a6c1be7d5072a8532229a9e78660e70ed
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325036"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>Opção de configuração de servidor XPs SMO e DMO
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
  
## <a name="see-also"></a>Consulte também  
 [Guia de Programação do SMO &#40;SQL Server Management Objects&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
