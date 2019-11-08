---
title: Tabelas com otimização de memória de níveis de isolamento de transação | Microsoft Docs
ms.custom: seo-dt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 8a6a82bf-273c-40ab-a101-46bd3615db8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eea34b8ad278447d9e9085d99acb8500d14d5e7a
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637783"
---
# <a name="transaction-isolation-levels-in-memory-optimized-tables"></a>Níveis de isolamento da transação em tabelas com otimização de memória

  Os níveis de isolamento a seguir têm suporte para transações que acessam tabelas com otimização de memória.  
  
-   SNAPSHOT  
  
-   REPEATABLE READ  
  
-   SERIALIZABLE  
  
-   READ COMMITTED  
  
 O nível de isolamento da transação pode ser especificado como parte do bloco atômico de um procedimento armazenado originalmente compilado. Para obter mais informações, consulte [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql). Ao acessar tabelas com otimização de memória do [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado, o nível de isolamento pode ser especificado usando as dicas no nível de tabela.  
  
 Você deve especificar o nível de isolamento da transação quando definir um procedimento armazenado compilado nativamente. Você deve especificar o nível de isolamento nas dicas de tabela ao acessar tabelas com otimização de memória de transações do usuário no [!INCLUDE[tsql](../includes/tsql-md.md)]interpretado. Para obter mais informações, consulte [diretrizes para níveis de isolamento de transação com tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 O nível de isolamento READ COMMITTED tem suporte em tabelas com otimização de memória com transações de confirmação automática. READ COMMITTED é inválido em transações de usuário ou em um bloco atômico. READ COMMITTED não tem suporte com transações de usuário implícitas ou explícitas. Há suporte para o nível de isolamento READ_COMMITTED_SNAPSHOT nas tabelas com otimização de memória com transações de confirmação automática e somente se a consulta não acessar nenhuma tabela baseada em disco. Além disso, as transações que são iniciadas usando o [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado com isolamento SNAPSHOT não podem acessar as tabelas com otimização de memória. As transações que usam o [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado, seja com o isolamento REPEATABLE READ ou SERIALIZABLE, devem acessar as tabelas com otimização de memória usando o isolamento SNAPSHOT. Para obter mais informações sobre esse cenário, consulte [Transações de contêiner cruzado](cross-container-transactions.md).  
  
 READ COMMITTED é o nível de isolamento padrão no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando o nível de isolamento da sessão for READ COMMITTED (ou inferior), siga um destes procedimentos:  
  
-   Use explicitamente uma dica de nível de isolamento mais alto para o acesso à tabela com otimização de memória (por exemplo, WITH (SNAPSHOT)).  
  
-   Especifique a opção set `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT`, que definirá o nível de isolamento de tabelas com otimização de memória para SNAPSHOT (como se você tivesse incluído dicas WITH(SNAPSHOT) em cada tabela com otimização de memória). Para obter mais informações sobre `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT`, consulte [opções &#40;ALTER DATABASE SET Transact-&#41;SQL](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 Como alternativa, se o nível de isolamento da sessão é READ COMMITTED, você pode usar transações de confirmação automática.  
  
 As transações SNAPSHOT iniciadas em [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado não podem acessar as tabelas com otimização de memória.  
  
 Os níveis de isolamento da transação com suporte em tabelas com otimização de memória fornecem as mesmas garantias lógicas que as tabelas baseadas em disco. O mecanismo usado para fornecer garantias do nível de isolamento é diferente.  
  
 Para tabelas baseadas em disco, a maioria das garantias do nível de isolamento é implementada usando o bloqueio, o que evita conflitos pelo bloqueio. Para tabelas com otimização de memória, as garantias são impostas usando um mecanismo de detecção de conflito, que evita a necessidade de aplicar bloqueios. A exceção é o isolamento SNAPSHOT em tabelas baseadas em disco. Ele é implementado de maneira semelhante ao isolamento SNAPSHOT em tabelas com otimização de memória usando um mecanismo de detecção de conflito.  
  
 SNAPSHOT  
 Esse nível de isolamento especifica que os dados lidos por qualquer instrução em uma transação serão a versão transacionalmente consistente dos dados que existiam no início da transação. A transação pode reconhecer apenas modificações de dados que estavam confirmadas antes do início da transação. Modificações de dados efetuadas por outras transações após o início da transação atual não são visíveis para as instruções em execução na transação atual. As instruções em uma transação obtêm um instantâneo dos dados confirmados conforme existiam no início da transação.  
  
 As operações de gravação (atualizações, inserções e exclusões) são sempre completamente isoladas de outras transações. Consequentemente, as operações de gravação em uma transação SNAPSHOT podem entrar em conflito com operações de gravação por outras transações. Quando a transação atual tentar atualizar ou excluir uma linha que foi atualizada ou excluída por outra transação que foi confirmada depois que a transação atual foi iniciada, a transação é encerrada com a mensagem de erro a seguir.  
  
 Erro 41302. A transação atual tentou atualizar um registro na tabela X que foi atualizado desde que esta transação foi iniciada. A transação foi anulada.  
  
 Quando a transação atual tentar inserir uma linha com o mesmo valor de chave primária de uma linha que foi inserida por outra transação que foi confirmada antes da transação atual, haverá uma falha na confirmação com a mensagem de erro a seguir.  
  
 Erro 41325. A transação atual não foi confirmada devido a uma falha de validação serializável.  
  
 Se uma transação for gravada em uma tabela que foi descartada antes da confirmação da transação, a transação será encerrada com a seguinte mensagem de erro:  
  
 Erro 41305. A transação atual não foi confirmada devido a uma falha de validação de leitura repetida.  
  
 REPEATABLE READ  
 Esse nível de isolamento inclui as garantias fornecidas pelo nível de isolamento SNAPSHOT. Além disso, REPEATABLE READ garante para qualquer linha que seja lida pela transação, no momento em que a transação é confirmada, que a linha não foi alterada por nenhuma outra transação. Cada operação de leitura na transação é repetida até o fim de transação.  
  
 Se a transação atual tiver lido qualquer linha que tenha sido atualizada por outra transação que tenha sido confirmada antes da transação atual, a confirmação falhará apresentando a mensagem de erro a seguir.  
  
 Erro 41305. A transação atual não foi confirmada devido a uma falha de validação de leitura repetida.  
  
 SERIALIZABLE  
 Esse nível de isolamento inclui as garantias fornecidas por REPEATABLE READ. Nenhuma linha fantasma apareceu entre o instantâneo e o término da transação. As linhas fantasmas correspondem à condição de filtro de uma seleção, atualização ou exclusão.  
  
 A transação é executada como se não houvesse transações simultâneas. Todas as ações ocorrem praticamente em um único ponto de serialização (hora da confirmação).  
  
 Se qualquer uma dessas garantias for violada, a transação não é confirmada e apresenta a seguinte mensagem de erro:  
  
 Erro 41325. A transação atual não foi confirmada devido a uma falha de validação serializável.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre transações em tabelas com otimização de memória](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Diretrizes para níveis de isolamento de transação com tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Diretrizes para lógica de repetição das transações em tabelas com otimização de memória](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
