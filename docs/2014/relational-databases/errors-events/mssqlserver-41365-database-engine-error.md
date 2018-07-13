---
title: MSSQLSERVER_41365 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7464be4dbdbd9df089c9219d79bede920f22891
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37418285"
---
# <a name="mssqlserver41365"></a>MSSQLSERVER_41365
    
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
 Forneça um melhor intervalo de transações para mesclagem/espera antes de emitir a mesma solicitação novamente. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
