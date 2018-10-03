---
title: Reciclar logs de erros do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72c3b0ee6af23f38871cc319e700c1680b5e134f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074967"
---
# <a name="recycle-sql-server-agent-error-logs"></a>Reciclar logs de erros do SQL Server Agent
  Use essa página para reciclar os logs de erros do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A reciclagem do log encerra o log de erros atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e inicia um novo log de erros sem reiniciar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém os nove logs de erros mais recentes. Se já houver nove logs de erros presentes, a reciclagem do log de erros faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent remova o log de erros mais antigo.  
  
## <a name="see-also"></a>Consulte também  
 [Log de erros do SQL Server Agent](sql-server-agent-error-log.md)  
  
  
