---
title: MSSQLSERVER_41307 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41307 (Database Engine error)
ms.assetid: 56f56410-b07d-4379-b01c-702c95761070
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa0bf9ea69f6e38b06eb5723cc6c9058265ada50
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868034"
---
# <a name="mssqlserver41307"></a>MSSQLSERVER_41307
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41307|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_HEKATON_ROW_LIMIT|  
|Texto da mensagem|O limite de tamanho de linha de *number* bytes para tabelas com otimização de memória foi excedido. Simplifique a definição da tabela.|  
  
## <a name="explanation"></a>Explicação  
 O limite de tamanho de linha para tabelas com otimização de memória é 8.060 bytes. Para obter mais informações, consulte [Tamanho da tabela e da linha em tabelas com otimização de memória](../in-memory-oltp/memory-optimized-tables.md). Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
