---
title: MSSQLSERVER_41333 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f137d859fa6f6233e14bc34c6bf50797a4360a98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123288"
---
# <a name="mssqlserver41333"></a>MSSQLSERVER_41333
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41333|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|CROSS_CONTAINER_ISOLATION_FAILURE|  
|Texto da mensagem|As transações a seguir devem acessar tabelas com otimização de memória e procedimentos armazenados em compilados nativamente em isolamento de instantâneo: Transações RepeatableRead, transações Serializable e transações que acessam tabelas não otimizadas para memória em isolamento RepeatableRead ou Serializable.|  
  
## <a name="explanation"></a>Explicação  
Há restrições relacionadas ao usuário dos níveis de isolamento mais altos entre transações baseadas em disco e transações XTP.  
  
## <a name="user-action"></a>Ação do usuário  
Não tente operações de alto nível de isolamento em tabelas com otimização de memória (e em procedimentos originalmente compilados) e tabelas baseadas em disco.  
  
Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
