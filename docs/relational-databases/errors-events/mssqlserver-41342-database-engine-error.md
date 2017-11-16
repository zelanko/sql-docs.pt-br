---
title: MSSQLSERVER_41342 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 8af7be1ae4b0a1cbba1b56bd9644d6b33cbdd8bf
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver41342"></a>MSSQLSERVER_41342
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41342|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_HW_NOT_SUPPORTED|  
|Texto da mensagem|O modelo do processador no sistema não dá suporte à criação de *construct*. Esse erro normalmente ocorre com processadores mais antigos. Consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter informações sobre modelos com suporte.|  
  
## <a name="explanation"></a>Explicação  
As tabelas com otimização de memória exigem um modelo de processador que dá suporte a operações atômicas de comparar-e-trocar em valores de 128 bits, que exigem instrução de assembly CMPXCHG16B. Alguns modelos mais antigos de processadores AMD não dão suporte à instrução CMPXCHG16B. Além disso, alguns ambientes de virtualização não habilitam essa instrução por padrão.  
  
## <a name="user-action"></a>Ação do usuário  
Atualize o processador. Se o processador der suporte à instrução e você estiver executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma máquina virtual, altere a configuração para dar suporte à instrução CMPXCHG16B.  
  
## <a name="see-also"></a>Consulte também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
