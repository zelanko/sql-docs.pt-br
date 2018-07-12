---
title: MSSQLSERVER_41325 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41325 (Database Engine error)
ms.assetid: 97c6a8bb-139a-44f3-9ed5-f46d047e8ed3
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 449993925048d902a1c04a78b2bab88c1ab939a7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424435"
---
# <a name="mssqlserver41325"></a>MSSQLSERVER_41325
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41325|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_TX_COMMIT_SR_VALIDATION|  
|Texto da mensagem|A transação atual não foi confirmada devido a uma falha de validação serializável.|  
  
## <a name="explanation"></a>Explicação  
 A transação encontrou uma falha de validação e agora está condenada.  
  
## <a name="user-action"></a>Ação do usuário  
 Repita a transação com falha. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
