---
title: MSSQLSERVER_41368 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
robots: noindex,nofollow
ms.openlocfilehash: f635eecdbaab6cbcb078fa59992928a66315a736
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323087"
---
# <a name="mssqlserver41368"></a>MSSQLSERVER_41368
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
O acesso às tabelas com otimização de memória usando o nível de isolamento READ COMMITTED tem suporte somente para transações de confirmação automática. Para obter mais informações, consulte [Transações com tabelas e procedimentos na memória](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md).  
  
Ao acessar uma tabela com otimização de memória de uma transação explícita que é iniciada com BEGIN TRANSACTION, ou de uma transação implícita, se IMPLICIT_TRANSACTIONS estiver definido como ON, o nível de isolamento READ COMMITTED não terá suporte.  
  
## <a name="user-action"></a>Ação do usuário  
Ao acessar uma tabela com otimização de memória de uma transação READ COMMITTED explícita ou implícita, use SNAPSHOT para acessar a tabela. Isso pode ser obtido usando a dica de tabela WITH (SNAPSHOT) (para obter mais informações, consulte [Transações com tabelas e procedimentos na memória](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)) ou definindo a opção de banco de dados MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT como ON (para obter mais informações, consulte [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql.md)).  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
