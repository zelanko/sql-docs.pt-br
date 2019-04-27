---
title: Diretrizes para níveis de isolamento da transação com tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e365e9ca-c34b-44ae-840c-10e599fa614f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26f0193d40a01858bc3fe651a23b389a4ffcb6ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779151"
---
# <a name="guidelines-for-transaction-isolation-levels-with-memory-optimized-tables"></a>Diretrizes para níveis de isolamento da transação com tabelas com otimização de memória
  Em vários cenários, você deve especificar o nível de isolamento da transação. O isolamento da transação para tabelas com otimização de memória difere das tabelas baseadas em disco.  
  
 Requisitos para especificação do nível de isolamento da transação:  
  
-   TRANSACTION ISOLATION LEVEL é uma opção necessária no bloco ATOMIC que compõe o conteúdo de um procedimento armazenado compilado nativamente.  
  
-   Devido às restrições do uso em nível de isolamento nas transações entre contêineres, os usos das tabelas com otimização de memória no [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado devem sempre ser acompanhados por uma dica de tabela que especifique o nível de isolamento usado para acessar a tabela. Para obter mais informações sobre dicas de nível de isolamento e transações entre contêineres, consulte [níveis de isolamento da transação](../../2014/database-engine/transaction-isolation-levels.md).  
  
-   O nível de isolamento da transação desejado deve ser explicitamente declarado. Não é possível usar dicas de bloqueio (como XLOCK) para garantir o isolamento de determinadas linhas ou tabelas na transação.  
  
-   O aplicativo que acessa o banco de dados deve implementar a lógica de repetição para tratar erros resultantes de conflitos decretados por transação, de falhas de validação e de falhas de dependência de confirmação. Observe que as falhas de dependência de confirmação podem ocorrer até mesmo com transações somente leitura.  
  
-   As transações de longa execução devem ser evitadas com tabelas com otimização de memória. Essas transações aumentam a probabilidade de conflitos e subsequentes encerramentos de transações. Uma transação de execução longa também adia a coleta de lixo. Quanto mais demorada for a transação, mais o OLTP na memória manterá versões de linhas excluídas recentemente, o que pode diminuir o desempenho da pesquisa de novas transações.  
  
 As tabelas baseadas em disco normalmente se baseiam no bloqueio do isolamento da transação. As tabelas com otimização de memória contam com o controle de várias versões e detecção de conflito para garantir o isolamento. Para obter detalhes, consulte a seção sobre detecção de conflito, validação e verificações de dependência de confirmação em [transações em tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 As tabelas baseadas em disco permitem o controle de várias versões nos níveis de isolamento SNAPSHOT e READ_COMMITTED_SNAPSHOT. Nas tabelas com otimização de memória, todos os níveis de isolamento baseiam-se no controle de várias versões, incluindo REPEATABLE READ e SERIALIZABLE.  
  
## <a name="types-of-transactions"></a>Tipos de transações  
 Cada consulta no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é executada no contexto de uma transação.  
  
 Há três tipos de transações no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Transações de confirmação automática. Se não houver nenhum contexto de transação ativo e as transações implícitas não estiverem definidas como ON na sessão, cada consulta terá seu próprio contexto de transação. A transação inicia quando a instrução começa a execução e termina quando a instrução é concluída.  
  
-   Transações explícitas. O usuário inicia a transação através de uma instrução BEGIN TRAN ou BEGIN ATOMIC explícita. A transação é concluída após as instruções COMMIT e ROLLBACK correspondentes ou END (no caso de um bloco atômico).  
  
-   Transações implícitas. Quando a opção IMPLICIT_TRANSACTIONS é definida como ON, uma transação é iniciada implicitamente sempre que o usuário executa uma instrução e não há nenhum contexto de transação ativo. A transação é concluída através de uma instrução COMMIT e ROLLBACK explícita.  
  
## <a name="baseline-read-committed-isolation"></a>Isolamento READ COMMITTED de linha de base  
 READ COMMITTED é o nível de isolamento padrão no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 O nível de isolamento READ COMMITTED garante que as transações não encontrem dados não confirmados de alterações fora da transação atual. Ou seja, a transação lê apenas os dados que foram confirmados para o banco de dados, ou que foram alterados pela transação atual.  
  
 Todos os níveis de isolamento com suporte para tabelas com otimização de memória fornecem a garantia de leitura confirmada. Portanto, se a transação não exigir garantias mais fortes, você pode usar qualquer nível de isolamento com suporte para tabelas com otimização de memória. O nível de isolamento SNAPSHOT usa o menor número possível de recursos do sistema, comparados com outros níveis de isolamento.  
  
 A garantia fornecida pelo nível de isolamento SNAPSHOT (o nível inferior de isolamento com suporte para tabelas com otimização de memória) inclui as garantias de READ COMMITTED. Cada instrução da transação lê a mesma versão consistente do banco de dados. Não somente todas as linhas são lidas pela transação confirmada no banco de dados, como também todas as operações de leitura veem o conjunto de alterações feito pelo mesmo conjunto de transações.  
  
 **Diretriz**: Se apenas a garantia de isolamento READ COMMITTED for necessária, use o isolamento SNAPSHOT com procedimentos armazenados compilados nativamente e para acessar tabelas com otimização de memória por meio de interpretado [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
 Para transações de confirmação automática, o nível de isolamento READ COMMITTED é mapeado implicitamente para SNAPSHOT nas tabelas com otimização de memória. Portanto, se a configuração de sessão TRANSACTION ISOLATION LEVEL for definida como READ COMMITTED, não será necessário especificar o nível de isolamento através de uma dica de tabela ao acessar tabelas com otimização de memória.  
  
 O exemplo de transação de confirmação automática a seguir mostra uma junção entre uma tabela com otimização de memória Customers e uma tabela normal [Order History], como parte de um lote ad hoc:  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
SELECT *   
FROM dbo.Customers AS c   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id = oh.customer_id;  
```  
  
 O seguinte exemplo de transações explícitas ou implícitas mostra a mesma junção, mas dessa vez em uma transação de usuário explícita. A tabela com otimização de memória Customers é acessada no isolamento de instantâneo, conforme indicado através da dica de tabela WITH (SNAPSHOT), e a tabela [Order History] normal é acessada no isolamento de leitura confirmada:  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
GO  
BEGIN TRAN  
SELECT * FROM dbo.Customers c with (SNAPSHOT)   
LEFT JOIN dbo.[Order History] oh   
    ON c.customer_id=oh.customer_id  
...  
COMMIT  
```  
  
### <a name="operational-differences"></a>Diferenças operacionais  
 Além da garantia de leitura confirmada, também há dois detalhes de implementação fundamentais que os aplicativos que usam tabelas baseadas em disco podem usar. Lembre-se do seguinte ao converter uma tabela baseada em disco acessada por meio do isolamento READ COMMITTED em tabela com otimização de memória acessada por meio do isolamento SNAPSHOT:  
  
-   A implementação do nível de isolamento READ COMMITTED das tabelas baseadas em disco (pressupondo que READ_COMMITTED_SNAPSHOT esteja desativado) usa bloqueios para evitar conflitos entre leitores e gravadores. Quando um gravador inicia a atualização de uma linha, ele usa um bloqueio e o libera apenas depois que a transação é confirmada. Todas as operações de leitura são bloqueadas e esperarão a transação de gravação ser confirmada.  
  
     Alguns aplicativos podem assumir que os leitores sempre esperarão a confirmação dos gravadores, especialmente se houver alguma sincronização entre as duas transações na camada de aplicativos.  
  
     **Diretriz:** Aplicativos não podem confiar no comportamento de bloqueio. Se um aplicativo precisar de sincronização entre transações simultâneas, tal lógica pode ser implementada na camada de aplicativo ou na camada de banco de dados, por meio [sp_getapplock &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getapplock-transact-sql).  
  
-   Em transações que usam o isolamento READ COMMITTED, cada instrução considera a versão mais recente das linhas no banco de dados. Portanto, as instruções subsequentes veem as alterações no estado do banco de dados.  
  
     A sondagem de uma tabela através de um loop WHILE até uma nova linha ser encontrada é um exemplo de um padrão de aplicativo que usa essa suposição. Com cada iteração do loop, a consulta considerará as atualizações mais recentes no banco de dados.  
  
     **Diretriz:** Se um aplicativo precisar sondar uma tabela com otimização de memória para obter as linhas mais recentes gravadas na tabela, mova o loop de sondagem fora do escopo da transação.  
  
     Este é um padrão de aplicativo de exemplo que usa essa suposição. Sondando uma tabela através de um loop WHILE até que uma nova linha seja encontrada. Em cada iteração de loop, a consulta acessará as atualizações mais recentes no banco de dados.  
  
 O exemplo de script a seguir sonda uma tabela t1 até que ela tenha uma linha. Em seguida, ele remove a linha única da tabela para processamento posterior.  
  
 Observe que a lógica de sondagem precisa estar fora do escopo da transação, pois ela está usando o isolamento de instantâneo para acessar a tabela t1. O uso da lógica de sondagem no escopo de uma transação criará uma transação demorada, que é uma prática incorreta.  
  
```sql  
-- poll table  
WHILE NOT EXISTS (SELECT 1 FROM dbo.t1)  
BEGIN   
  -- if empty, wait and poll again  
  WAITFOR DELAY '00:00:01'  
END  
  
BEGIN TRANSACTION  
  DECLARE @id int  
  SELECT TOP 1 @id=id FROM dbo.t1 WITH (SNAPSHOT)  
  DELETE FROM dbo.t1 WITH (SNAPSHOT) WHERE id=@id  
  
  -- insert processing based on @id  
COMMIT  
```  
  
## <a name="locking-table-hints"></a>Dicas de bloqueio de tabela  
 Dicas de bloqueio ([dicas de tabela &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)), como HOLDLOCK e XLOCK podem ser usadas com tabelas baseadas em disco para ter [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] levar mais bloqueios do que são necessários para o nível de isolamento especificado.  
  
 As tabelas com otimização de memória não usam bloqueios. Os níveis de isolamento superiores, como REPEATABLE READ e SERIALIZABLE, podem ser usados para declarar as garantias desejadas.  
  
 Não há suporte para as dicas de bloqueio. Em vez disso, declare as garantias exigidas através dos níveis de isolamento de transação. (NOLOCK tem suporte porque o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não usa bloqueios em tabelas com otimização de memória. Observe que, em contraste com tabelas baseadas em disco, NOLOCK não implica o comportamento READ UNCOMMITTED para tabelas com otimização de memória.)  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre transações em tabelas com otimização de memória](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Diretrizes para lógica de repetição das transações em tabelas com otimização de memória](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)   
 [Níveis de isolamento da transação](../../2014/database-engine/transaction-isolation-levels.md)  
  
  
