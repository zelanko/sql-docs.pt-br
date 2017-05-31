---
title: Criar um alerta de banco de dados do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database performance [SQL Server], alerts
- alerts [SQL Server], creating
- thresholds [SQL Server]
- database alerts [SQL Server]
- tuning databases [SQL Server], alerts
- monitoring performance [SQL Server], alerts
- monitoring server performance [SQL Server], alerts
- database monitoring [SQL Server], alerts
- server performance [SQL Server], alerts
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 67aaf5ab44e5584fc50851dd797ad7cbc62f3ffc
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-sql-server-database-alert"></a>Criar um alerta de banco de dados do SQL Server
  É possível usar o Monitor do Sistema para criar um alerta a ser emitido quando um valor limite de um contador do Monitor do Sistema for atingido. Em resposta ao alerta, o Monitor do Sistema inicia um aplicativo, tal como um aplicativo cliente escrito para manipular a condição de alerta. Por exemplo, você pode criar um alerta a ser emitido quando o número de deadlocks exceder um valor específico.  
  
 Também podem ser definidos alertas por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações, consulte [Alertas](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef).  
  
 Para obter mais informações sobre como usar o Monitor do Sistema para configurar um alerta de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Configurar um alerta de banco de dados do SQL Server &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md).  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  
