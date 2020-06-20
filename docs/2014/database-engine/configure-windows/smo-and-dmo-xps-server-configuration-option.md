---
title: Opção de configuração de servidor SMO and DMO XPs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 64eb0087a9261502900c1b1f29d6ce5d2a0cd976
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934827"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>Opção de configuração de servidor XPs SMO e DMO
  Use a opção SMO e DMO XPs para habilitar os procedimentos armazenados estendidos do SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object) neste servidor.  
  
 Observe que começando pelo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o DMO foi removido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os possíveis valores são descritos na tabela seguinte:  
  
|Valor|Significado|  
|-----------|-------------|  
|0|Os SMO XPs não estão disponíveis.|  
|1|Os SMO XPs estão disponíveis. Esse é o padrão.|  
  
 A configuração entra em vigor imediatamente.  
  
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
  
  
