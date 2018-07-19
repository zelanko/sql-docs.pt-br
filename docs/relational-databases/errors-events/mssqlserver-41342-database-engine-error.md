---
title: MSSQLSERVER_41342 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b549fe11ced943a253ffb3d5cafd376eb87e3b01
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293326"
---
# <a name="mssqlserver41342"></a>MSSQLSERVER_41342
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41342|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_HW_NOT_SUPPORTED|  
|Texto da mensagem|O modelo do processador no sistema não dá suporte à criação de *construct*. Esse erro normalmente ocorre com processadores mais antigos.|  
  
## <a name="explanation"></a>Explicação  
As tabelas com otimização de memória exigem um modelo de processador que dá suporte a operações atômicas de comparar-e-trocar em valores de 128 bits, que exigem instrução de assembly CMPXCHG16B. Alguns modelos mais antigos de processadores AMD não dão suporte à instrução CMPXCHG16B. Além disso, alguns ambientes de virtualização não habilitam essa instrução por padrão.  
  
## <a name="user-action"></a>Ação do usuário  
Atualize o processador. Se o processador der suporte à instrução e você estiver executando o SQL Server em uma máquina virtual, altere a configuração para dar suporte à instrução CMPXCHG16B.  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
