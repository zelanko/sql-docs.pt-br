---
description: MSSQLSERVER_41333
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
ms.openlocfilehash: 0e3d0cb81362aacc4e3c60e83b077cf77e919f37
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428678"
---
# <a name="mssqlserver_41333"></a>MSSQLSERVER_41333
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41333|  
|Origem do Evento|MSSQLSERVER|  
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
  
