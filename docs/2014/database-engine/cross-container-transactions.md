---
title: Transações entre contêineres | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5d84b51a-ec17-4c5c-b80e-9e994fc8ae80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 290aff0bfcb01e098ae87b48cf582cdf999314c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807420"
---
# <a name="cross-container-transactions"></a>Transações entre contêineres
  As transações entre contêineres são as transações de usuário implícitas ou explícitas que incluem chamadas para procedimentos armazenados compilados nativamente ou para operações em tabelas com otimização de memória.  
  
 No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], as chamadas aos procedimentos armazenados não iniciam uma transação. As execuções de procedimentos compilados nativamente no modo de confirmação automática (não no contexto de uma transação de usuário) não são consideradas transações entre contêineres.  
  
 Qualquer consulta interpretada que faça referência a tabelas com otimização de memória é considerada uma parte de uma transação entre contêineres, seja ela executada de uma transação explícita ou implícita, ou no modo de confirmação automática.  
  
##  <a name="isolation"></a> Isolamento de operações individuais  
 Cada transação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem um nível de isolamento. O nível de isolamento padrão é Read Committed. Para usar um nível de isolamento diferente, você pode definir o nível de isolamento usando [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).  
  
 Geralmente, é necessário executar operações em tabelas com otimização de memória em um nível de isolamento diferente das operações em tabelas baseadas em disco. Em uma transação, é possível definir um nível de isolamento diferente para uma coleção de instruções ou para uma operação de leitura individual.  
  
### <a name="specifying-the-isolation-level-of-individual-operations"></a>Especificando o nível de isolamento de operações individuais  
 Para definir um nível de isolamento diferente para um conjunto de instruções em uma transação, você pode usar `SET TRANSACTION ISOLATION LEVEL`. O exemplo a seguir de uma transação usa o nível de isolamento serializável como padrão. As operações de inserção e seleção em t3, t2 e t1 são executadas sob o isolamento de leitura repetida.  
  
```sql  
set transaction isolation level serializable  
go  
  
begin transaction  
 ......  
  set transaction isolation level repeatable read  
  
  insert t3 select * from t1 join t2 on t1.id=t2.id  
  
  set transaction isolation level serializable  
 ......  
commit  
```  
  
 Para definir um nível de isolamento para operações de leitura individual que seja diferente do padrão da transação, você pode usar uma dica de tabela (por exemplo, serializável). Cada seleção corresponde a uma operação de leitura, assim como cada atualização e cada exclusão correspondem a uma leitura, pois a linha sempre precisa ser lida para poder ser atualizada ou excluída. As operações de inserção não têm um nível de isolamento, pois as gravações são sempre isoladas no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No exemplo a seguir, o nível de isolamento padrão da transação é leitura confirmada, mas a tabela t1 é acessada em serializável e t2 no isolamento de instantâneo.  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
 ......  
  
  insert t3 select * from t1 (serializable) join t2 (snapshot) on t1.id=t2.id  
  
  ......  
commit  
```  
  
### <a name="isolation-semantics-for-individual-operations"></a>Semântica de isolamento para operações individuais  
 Uma transação serializável T é executada em isolamento completo. É como se todas as outras transações tivessem sido confirmadas antes de T ter sido iniciada, ou elas foram iniciadas depois de T ter sido confirmada. Isso se torna mais complexo quando operações diferentes em uma transação têm diferentes níveis de isolamento.  
  
 A semântica geral dos níveis de isolamento de transação em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], juntamente com as implicações sobre bloqueio, é explicado na [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).  
  
 Para transações entre contêineres em que operações diferentes podem ter níveis de isolamento diferentes, você precisa entender a semântica de isolamento das operações de leitura individual. As operações de gravação sempre são isoladas. As gravações em transações diferentes não podem se afetar.  
  
 Uma operação de leitura de dados retorna um número de linhas que atendem a uma condição de filtro.  
  
 As leituras são executadas como parte de uma transação T. de níveis de isolamento para operações de leitura pode ser compreendido em termos de:  
  
 Status de confirmação  
 O status de confirmação se refere à garantia de confirmação da leitura dos dados.  
  
 (Transacional) Consistência  
 A consistência transacional para um conjunto de leituras se refere à garantia de que as versões de linha lidas incluirão atualizações precisamente do mesmo conjunto de transações.  
  
 A estabilidade garante que o sistema forneça à transação T informações sobre a leitura de dados.  
 Estabilidade se refere ao se as leituras de transação são repetidas. Isto é, se as leituras fossem repetidas, elas retornariam as mesmas linhas e versões de linha?  
  
 Determinadas garantias se referem à hora de término lógica da transação. De modo geral, a hora de término lógica é a hora em que a transação foi confirmada no banco de dados. Se as tabelas com otimização de memória são acessadas pela transação, a hora de término lógica, tecnicamente, é o início da fase de validação. (Para obter mais informações, consulte a discussão de tempo de vida de transação na [transações em tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Independentemente do nível de isolamento, uma transação (T) sempre vê suas próprias atualizações:  
  
 READ UNCOMMITTED  
 A leitura de dados não pode ser confirmada, consistente ou estável. No entanto, ela incluirá operações de gravação anteriores feitas por T.  
  
 READ COMMITTED  
 A leitura de dados será confirmada.  
  
 SNAPSHOT  
 Todas as operações de leitura executadas por T no isolamento instantâneo têm a mesma hora de leitura lógica, que é o início da transação. A leitura de dados tem a garantia de confirmação e consistência a partir da hora de leitura lógica. A repetição de uma leitura a partir da hora de leitura original é garantia de retorno do mesmo resultado.  
  
 REPEATABLE READ  
 A leitura de dados tem garantia de confirmação e estabilização até a hora de término lógica da transação.  
  
 SERIALIZABLE  
 Todas as garantias de REPEATABLE READ além de impedimento de fantasma e consistência transacional em relação a todas as operações de leitura serializáveis executadas por T. fantasma impedimento significa que a operação de verificação pode retornar apenas linhas adicionais que foram escritas por T, mas nenhum linhas que foram gravadas por outras transações.  
  
 Considere a seguinte transação:  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  -- remove all rows from t3; the related read operation is performed under read committed   
  -- isolation, as this is the default for the transaction  
  delete from t3  
  
  -- copy the contents from t1 to t3; the read on t1 is performed under the serializable   
  -- isolation level  
  insert t3 select * from t1 (serializable)  
  
  -- compare t3 and t1; note: the result set may not be empty, as rows may have been added   
  -- by other transaction before this select, due to the read committed isolation level  
  select * from t3 except t1  
  
  -- compare t1 and t3; note: the result set is empty, as no rows have been added to t1   
  -- since its contents were copied to t1, due to the serializable isolation level  
  select * from t1 except t3  
commit  
```  
  
 Essa transação exclui todas as linhas de t3 em isolamento de leitura confirmada, copia todas as linhas de t1 a t3 no isolamento serializável e então compara t1 e t3. Algumas linhas [não em t1] podem ter sido adicionadas ao t3, uma vez que a tabela estava vazia. Nenhuma linha foi adicionada à t1, pois a cópia era serializável.  
  
 Embora a leitura de t1 no fim da transação seja uma leitura confirmada sintaticamente, ela é eficazmente serializável, pois a mesma leitura foi executada anteriormente na transação no isolamento serializável: a capacidade de serialização garante que, se a leitura for executada em qualquer ponto posterior na transação, as mesmas linhas sejam retornadas.  
  
## <a name="cross-container-transactions-and-isolation-levels"></a>Transações entre contêineres e níveis de isolamento  
 Uma transação entre contêineres têm dois lados: um lado baseado em disco (para operações em tabelas baseadas em disco) e um lado com otimização de memória (para operações em tabelas com otimização de memória). Esses dois lados podem ter diferentes níveis de isolamento. Na verdade, as operações de leitura individuais em cada lado podem ter níveis de isolamento diferentes.  
  
 O lado baseado em disco de uma determinada transação T atingirá um determinado nível de isolamento X se uma das seguintes condições for atendida:  
  
-   Ele inicia em X. Ou seja, o padrão da sessão era X, seja porque você executou `SET TRANSACTION ISOLATION LEVEL`, ou é o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] padrão.  
  
-   Durante a transação, o nível de isolamento padrão foi alterado para X usando `SET TRANSACTION ISOLATION LEVEL`.  
  
-   Uma operação de leitura em uma tabela com base em disco é executada no nível de isolamento X usando a sintaxe `WITH (X)`.  
  
 O lado com otimização de memória T atingirá um nível de isolamento Y se, durante a execução de T, qualquer operação de leitura em uma tabela com otimização de memória ou qualquer procedimento armazenado compilado nativamente for executado no nível de isolamento Y.  
  
 Considere a seguinte transação como um exemplo. Aqui, t1 e t2 são tabelas baseadas em disco, e t3 e t4 são tabelas com otimização de memória.  
  
 O lado baseado em disco da transação atinge o nível de isolamento de leitura confirmada, pois ela é iniciada nesse nível. O lado baseado em disco também atinge o nível de leitura repetida, pois a primeira operação de leitura é executada nesse nível de isolamento. A exclusão no fim da transação é executada no nível de isolamento de leitura confirmada e, desse modo, não introduz um novo nível de isolamento.  
  
 O lado com otimização de memória da transação pode atingir um dos dois níveis: se condition1 for true, ele atingirá serializável, se for false, o lado com otimização de memória atinge somente o isolamento de instantâneo.  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  select * from t1 (repeatableread)  
  
  if condition1 begin  
    insert t3 select * from t4 (serializable)  
  end  
  else begin  
    insert t3 select * from t4 (snapshot)  
  end  
  
  delete from t1  
commit  
```  
  
### <a name="supported-isolation-levels-for-cross-container-transactions"></a>Níveis de isolamento com suporte para transações entre contêineres  
 Há limitações sobre os níveis de isolamento usados com operações em tabelas com otimização de memória nas transações entre contêineres.  
  
 As tabelas com otimização de memória oferecem suporte aos níveis de isolamento SNAPSHOT, REPEATABLE READ e SERIALIZABLE. Para transações de confirmação automática, as tabelas com otimização de memória oferecem suporte ao nível de isolamento READ COMMITTED.  
  
 Os cenários a seguir têm suporte:  
  
-   As transações entre contêineres READ UNCOMMITTED, READ COMMITTED e READ_COMMITTED_SNAPSHOT podem acessar tabelas com otimização de memória no isolamento SNAPSHOT, REPEATABLE READ e SERIALIZABLE. A garantia READ COMMITTED é mantida para a transação; todas as linhas lidas pela transação foram confirmadas no banco de dados.  
  
-   As transações REPEATABLE READ e SERIALIZABLE podem acessar tabelas com otimização de memória no isolamento SNAPSHOT.  
  
## <a name="read-only-cross-container-transactions"></a>Transações entre contêineres somente leitura  
 A maioria das transações somente leitura no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é revertida no momento da confirmação. Como não há nenhuma alteração a ser confirmada no banco de dados, o sistema simplesmente libera os recursos usados pela transação. Para transações baseadas em disco somente leitura, todos os bloqueios aplicados pela transação são liberados nesse momento. Para transações com otimização de memória somente leitura que abrangem uma única execução do procedimento originalmente compilado, nenhuma validação é executada.  
  
 As transações somente leitura entre contêineres no modo de confirmação automática são simplesmente revertidas no fim da transação. Nenhuma validação é executada.  
  
 As transações somente leitura entre contêineres explícitas ou implícitas executarão a validação no momento da confirmação se a transação acessar tabelas com otimização de memória no isolamento REPEATABLE READ ou SERIALIZABLE. Para obter detalhes sobre a validação de consulte a seção sobre detecção de conflito, validação, e verificações de dependência de confirmação em [transações em tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre transações em tabelas com otimização de memória](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Diretrizes para níveis de isolamento da transação com tabelas com otimização de memória](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)   
 [Diretrizes para lógica de repetição das transações em tabelas com otimização de memória](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
