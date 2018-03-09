---
title: MSSQLSERVER_41301 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41301 (Database Engine error)
ms.assetid: c6127e1e-2846-4ee9-bc42-2d896ea9730e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac85372b238cb049398979a710cde0d4c75f41c0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver41301"></a>MSSQLSERVER_41301
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41301|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|COMMIT_DEPENDENCY_FAILURE|  
|Texto da mensagem|Uma transação anterior na qual a transação atual obteve uma dependência foi anulada, e a transação atual não pode mais ser confirmada.|  
  
## <a name="explanation"></a>Explicação  
A transação encontrou uma falha de dependência e agora está condenada.  
  
Esse erro também pode ser causado por transações dependentes demais. Qualquer transação de gravação pode ter um número limitado de transações dependentes. Por exemplo, esse erro pode ocorrer se muitas transações de leitura tentarem executar uma dependência na transação de atualização.  
  
## <a name="user-action"></a>Ação do usuário  
Não execute nenhum trabalho na transação. Chame ROLLBACK TRAN para reverter a transação. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte também  
[Habilitar e desabilitar grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
