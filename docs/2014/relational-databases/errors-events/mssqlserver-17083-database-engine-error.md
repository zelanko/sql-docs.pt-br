---
title: MSSQLSERVER_17083 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17083 (Database Engine error)
ms.assetid: 6c83737d-0531-4fd9-88f6-2da5a150532d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f4caebbc63664539603d816473069c72200540af
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967927"
---
# <a name="mssqlserver_17083"></a>MSSQLSERVER_17083
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|17083|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|P3_HEKATON_NOT_ATOMIC|  
|Texto da mensagem|O corpo de um procedimento armazenado originalmente compilado deve ser um bloco ATOMIC.|  
  
## <a name="explanation"></a>Explicação  
 O corpo de um procedimento armazenado originalmente compilado não tinha um bloco ATOMIC.  
  
## <a name="user-action"></a>Ação do usuário  
 Um procedimento armazenado originalmente compilado deve conter um bloco ATOMIC. Por exemplo:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
