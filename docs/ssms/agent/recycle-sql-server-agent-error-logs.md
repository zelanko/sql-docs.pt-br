---
title: Reciclar logs de erros do SQL Server Agent | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 349ae61e3ed53912f2f25565f9db7a99f4b56b56
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="recycle-sql-server-agent-error-logs"></a>Reciclar logs de erros do SQL Server Agent
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use essa página para reciclar os logs de erros do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. A reciclagem do log encerra o log de erros atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e inicia um novo log de erros sem reiniciar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent mantém os nove logs de erros mais recentes. Se já houver nove logs de erros presentes, a reciclagem do log de erros faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent remova o log de erros mais antigo.  
  
## <a name="see-also"></a>Consulte Também  
[Log de erros do SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
