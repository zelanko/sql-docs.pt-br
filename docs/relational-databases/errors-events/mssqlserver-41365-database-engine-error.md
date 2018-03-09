---
title: MSSQLSERVER_41365 | Microsoft Docs
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
- 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69d2164c5031f2dcf123d14056e4c9e37b7ccc6a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver41365"></a>MSSQLSERVER_41365
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41365|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_MERGE_SCHEDULE_ERROR|  
|Texto da mensagem|A solicitação de mesclagem para o intervalo de transações [%ld, %ld] no banco de dados %.*ls não foi agendada. Os arquivos de ponto de verificação que representam o intervalo não estão disponíveis para mesclagem ou parte de uma mesclagem contínua.|  
  
## <a name="explanation"></a>Explicação  
Os arquivos de ponto de verificação que representam o intervalo não estão disponíveis para mesclagem ou parte de uma mesclagem contínua.  
  
## <a name="user-action"></a>Ação do usuário  
Forneça um melhor intervalo de transações para mesclagem/espera antes de emitir a mesma solicitação novamente. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
