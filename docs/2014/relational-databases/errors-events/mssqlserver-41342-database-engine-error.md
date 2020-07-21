---
title: MSSQLSERVER_41342 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b67d1d9dc7d73f46e0b267d66651f1dfe1a4c8d9
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551401"
---
# <a name="mssqlserver_41342"></a>MSSQLSERVER_41342
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41342|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_HW_NOT_SUPPORTED|  
|Texto da mensagem|O modelo do processador no sistema não dá suporte à criação de *construct*. Esse erro normalmente ocorre com processadores mais antigos. Consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter informações sobre modelos com suporte.|  
  
## <a name="explanation"></a>Explicação  
 As tabelas com otimização de memória exigem um modelo de processador que dá suporte a operações atômicas de comparar-e-trocar em valores de 128 bits, que exigem instrução de assembly CMPXCHG16B. Alguns modelos mais antigos de processadores AMD não dão suporte à instrução CMPXCHG16B. Além disso, alguns ambientes de virtualização não habilitam essa instrução por padrão.  
  
## <a name="user-action"></a>Ação do usuário  
 Atualize o processador. Se o processador der suporte à instrução e você estiver executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma máquina virtual, altere a configuração para dar suporte à instrução CMPXCHG16B.  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
