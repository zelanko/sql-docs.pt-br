---
title: Reciclar logs de erros do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0654dcc83e757751ac055192775c0ee958f26e9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62753063"
---
# <a name="recycle-sql-server-agent-error-logs"></a>Reciclar logs de erros do SQL Server Agent
  Use esta página para reciclar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os logs de erros do Agent. A reciclagem do log encerra o log de erros atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e inicia um novo log de erros sem reiniciar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém os nove logs de erros mais recentes. Se já houver nove logs de erros presentes, a reciclagem do log de erros faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent remova o log de erros mais antigo.  
  
## <a name="see-also"></a>Consulte Também  
 [Log de erros do SQL Server Agent](sql-server-agent-error-log.md)  
  
  
