---
title: Monitorar o uso de disco | Microsoft Docs
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
- database monitoring [SQL Server], disk usage
- disks [SQL Server]
- monitoring performance [SQL Server], disk usage
- server performance [SQL Server], disk usage
- monitoring [SQL Server], disk activity
- excess paging [SQL Server]
- tuning databases [SQL Server], disk usage
- I/O [SQL Server], monitoring
- disks [SQL Server], monitoring activity
- isolating disk activity [SQL Server]
- database performance [SQL Server], disk usage
- monitoring server performance [SQL Server], disk usage
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5ff4acc6d6465b09c721d376b14ba6574938ef38
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="monitor-disk-usage"></a>Monitorar o uso do disco
  O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa chamadas de E/S (entrada/saída) do sistema operacional Microsoft Windows para executar operações de leitura e gravação no seu disco. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerencia quando e como a E/S de disco é executada, mas o sistema operacional Windows executa as operações de E/S subjacentes. O subsistema de E/S compreende o barramento do sistema, as placas do controlador de disco, os discos, as unidades de fita, a unidade de CD-ROM e vários outros dispositivos de E/S. E/S no disco é, muitas vezes, a causa de afunilamentos em um sistema.  
  
 Monitorar a atividade de disco envolve duas áreas de foco:  
  
-   Monitorar E/S no disco e detectar paginação excessiva  
  
-   Isolar a atividade de disco criada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Para obter mais informações, consulte [Monitorando o uso do disco](http://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx)  
  
  
