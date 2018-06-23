---
title: MSSQLSERVER_41332 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d871813734e6e514b30f4cf11508c2e50e07771c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006844"
---
# <a name="mssqlserver41332"></a>MSSQLSERVER_41332
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41332|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQL_SNAPSHOT_NOT_SUPPORTED|  
|Texto da mensagem|As tabelas com otimização de memória e os procedimentos armazenados compilados originalmente não poderão ser acessados ou criados quando o TRANSACTION ISOLATION LEVEL de sessão estiver definido como SNAPSHOT.|  
  
## <a name="explanation"></a>Explicação  
 A transação foi iniciada no nível de isolamento do instantâneo e tentou usar um recurso incompatível.  
  
## <a name="user-action"></a>Ação do usuário  
 Inicie a transação com um nível de isolamento diferente. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  