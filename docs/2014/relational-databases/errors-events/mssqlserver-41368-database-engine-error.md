---
title: MSSQLSERVER_41368 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 18b9ccb8a91d1fa8df1d6f39bf9c47636ae33d4e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551352"
---
# <a name="mssqlserver_41368"></a>MSSQLSERVER_41368
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41368|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|Texto da mensagem|Há suporte para o acesso às tabelas com otimização de memória usando o nível de isolamento READ COMMITTED somente em transações de confirmação automática. Ele não tem suporte para transações implícitas ou explícitas. Forneça um nível de isolamento com suporte para a tabela com otimização de memória usando uma dica de tabela, como WITH (SNAPSHOT).|  
  
## <a name="explanation"></a>Explicação  
 O acesso às tabelas com otimização de memória usando o nível de isolamento READ COMMITTED tem suporte somente para transações de confirmação automática. Para obter mais informações, consulte [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md).  
  
 Ao acessar uma tabela com otimização de memória de uma transação explícita que é iniciada com BEGIN TRANSACTION, ou de uma transação implícita, se IMPLICIT_TRANSACTIONS estiver definido como ON, o nível de isolamento READ COMMITTED não terá suporte.  
  
## <a name="user-action"></a>Ação do usuário  
 Ao acessar uma tabela com otimização de memória de uma transação READ COMMITTED explícita ou implícita, use SNAPSHOT para acessar a tabela. Isso pode ser feito usando a dica de tabela com (instantâneo) (para obter mais informações, consulte [diretrizes para níveis de isolamento de transação com tabelas com otimização de memória](../in-memory-oltp/memory-optimized-tables.md)) ou definindo a opção de banco de dados MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT como on (para obter mais informações, consulte [Opções ALTER database SET &#40;&#41;Transact-SQL ](/sql/t-sql/statements/alter-database-transact-sql-set-options)).  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
