---
title: MSSQLSERVER_41342 | Microsoft Docs
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
- 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c3040f4222d9c790f42566ae4971d8f1caa189be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36021162"
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
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  