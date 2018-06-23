---
title: MSSQLSERVER_41368 | Microsoft Docs
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
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 96d33fc176330efe93077c02c6abfed3c137e33c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008179"
---
# <a name="mssqlserver41368"></a>MSSQLSERVER_41368
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41368|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|Texto da mensagem|Há suporte para o acesso às tabelas com otimização de memória usando o nível de isolamento READ COMMITTED somente em transações de confirmação automática. Ele não tem suporte para transações implícitas ou explícitas. Forneça um nível de isolamento com suporte para a tabela com otimização de memória usando uma dica de tabela, como WITH (SNAPSHOT).|  
  
## <a name="explanation"></a>Explicação  
 O acesso às tabelas com otimização de memória usando o nível de isolamento READ COMMITTED tem suporte somente para transações de confirmação automática. Para obter mais informações, consulte [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md).  
  
 Ao acessar uma tabela com otimização de memória de uma transação explícita que é iniciada com BEGIN TRANSACTION, ou de uma transação implícita, se IMPLICIT_TRANSACTIONS estiver definido como ON, o nível de isolamento READ COMMITTED não terá suporte.  
  
## <a name="user-action"></a>Ação do usuário  
 Ao acessar uma tabela com otimização de memória de uma transação READ COMMITTED explícita ou implícita, use SNAPSHOT para acessar a tabela. Isso pode ser feito usando a dica de tabela WITH (SNAPSHOT) (para obter mais informações, consulte [diretrizes para níveis de isolamento de transação com tabelas com otimização de memória](../in-memory-oltp/memory-optimized-tables.md)) ou definindo o banco de dados de opção MEMORY_OPTIMIZED_ELEVATE_TO_ INSTANTÂNEO como ON (para obter mais informações, consulte [opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)).  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
