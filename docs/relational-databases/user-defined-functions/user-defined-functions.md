---
title: Funções definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], components
- user-defined functions [SQL Server], about user-defined functions
- UDF
- TVF
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8deea6a37a8aca7791d84d9d32d9735525305913
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247245"
---
# <a name="user-defined-functions"></a>Funções definidas pelo usuário
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Assim como as funções em linguagens de programação, as funções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definidas pelo usuário são rotinas que aceitam parâmetros, executam uma ação, como um cálculo complexo, e retornam o resultado dessa ação como um valor. O valor de retorno pode ser um único valor escalar ou um conjunto de resultados.  
   
##  <a name="user-defined-functions"></a><a name="Benefits"></a> Funções definidas pelo usuário  
Por que usar UDFs (funções definidas pelo usuário)? 
  
-   Eles permitem programação modular.  
  
     Você pode criar a função uma vez, armazená-la no banco de dados e chamá-la quantas vezes quiser em seu programa. Funções definidas pelo usuário podem ser modificadas independentemente do código-fonte do programa.  
  
-   Elas permitem execução mais rápida.  
  
     Semelhantemente aos procedimentos armazenados, [!INCLUDE[tsql](../../includes/tsql-md.md)] as funções definidas pelo usuário reduzem o custo de compilação do código [!INCLUDE[tsql](../../includes/tsql-md.md)] colocando os planos em cache e reusando-os para execuções repetidas. Isso significa que a função definida pelo usuário não precisa ser reanalisada e reotimizada em cada utilização resultando em tempos de execução mais rápidos.  
  
     As funções CLR oferecem uma vantagem de desempenho significativa sobre funções [!INCLUDE[tsql](../../includes/tsql-md.md)] para tarefas de computação, manipulação de cadeias de caracteres e lógica de negócios. As funções [!INCLUDE[tsql](../../includes/tsql-md.md)] são mais adequadas à lógica intensiva de acesso a dados.  
  
-   Eles podem reduzir o tráfego de rede.  
  
     Uma operação que filtra dados com base em alguma restrição complexa que não pode ser expressa em uma única expressão escalar pode ser expressa como uma função. Em seguida, a função pode ser invocada na cláusula WHERE para reduzir o número de linhas enviadas ao cliente.  
  
> [!IMPORTANT]
> As UDFs [!INCLUDE[tsql](../../includes/tsql-md.md)] em consultas só podem ser executadas em um único thread (plano de execução serial). Portanto, usar UDFs inibe o processamento paralelo de consultas. Para obter mais informações sobre o processamento paralelo de consultas, confira o [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md#parallel-query-processing).
  
##  <a name="types-of-functions"></a><a name="FunctionTypes"></a> Tipos de funções  
**Função escalar**  
 As funções escalares definidas pelo usuário retornam um valor único de dados do tipo definido na cláusula RETURNS. Para uma função escalar embutida, o valor escalar retornado é o resultado de uma única instrução. Para uma função escalar de várias instruções, o corpo da função pode conter uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], que retornam o valor único. O tipo de retorno pode ser qualquer tipo de dados, exceto **text**, **ntext**, **image**, **cursor**e **timestamp**. 
 **[Exemplos.](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar)**
  
**Funções com valor de tabela**  
 As funções com valor de tabela definidas pelo usuário retornam um tipo de dados **table**. Para uma função com valor de tabela embutida, não há um corpo de função; a tabela é o conjunto de resultados de uma única instrução SELECT. **[Exemplos.](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)**
  
**Funções do Sistema**  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece muitas funções de sistema que você pode usar para executar uma variedade de operações. Elas não podem ser modificadas. Para obter mais informações, consulte [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md), [Funções armazenadas do sistema &#40;Transact-SQL&#41;](~/relational-databases/system-functions/system-functions-category-transact-sql.md) e [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
##  <a name="guidelines"></a><a name="Guidelines"></a> Diretrizes  
 Erros de [!INCLUDE[tsql](../../includes/tsql-md.md)] que levam ao cancelamento de uma instrução e continuam com a instrução seguinte no módulo (como gatilhos ou procedimentos armazenados) tratados de modo diferente em uma função. Nas funções, esses erros fazem com que a execução da função seja interrompida. Em troca, isso faz com que a instrução que chamou a função seja cancelada.  
  
 As instruções em um bloco `BEGIN...END` não podem ter nenhum efeito colateral. Os efeitos colaterais da função são as alterações permanentes realizada no estado de um recurso que tem um escopo fora da função como uma modificação em uma tabela do banco de dados. As únicas alterações que podem ser feitas pelas instruções na função são alterações em objetos locais à função, como cursores ou variáveis locais. As modificações em tabelas de banco de dados, operações em cursores que não são locais à função, envio de e-mail, tentativa de modificação em catálogo e geração de um conjunto de resultados retornados ao usuário são exemplos de ações que não devem ser realizadas em uma função.  
  
> [!NOTE]
> Se uma instrução `CREATE FUNCTION` produzir efeitos colaterais com base nos recursos que não existem quando a instrução `CREATE FUNCTION` for emitida, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará a instrução. Porém, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não executa a função quando é chamada.  
  
 O número de vezes em que uma função especificada em uma consulta é realmente executada pode variar entre os planos de execução desenvolvidos pelo otimizador. Um exemplo é a função chamada por uma subconsulta em uma cláusula `WHERE`. O número de vezes em que a subconsulta e sua função são executadas pode variar com os caminhos de acesso diferentes escolhidos pelo otimizador.  
 
> [!IMPORTANT]   
> Para obter mais considerações de desempenho e informações sobre funções definidas pelo usuário, confira [Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md). 
  
##  <a name="valid-statements-in-a-function"></a><a name="ValidStatements"></a> Instruções válidas em uma função  
Os tipos de instruções que são válidos em uma função incluem:  
  
-   As instruções `DECLARE` podem ser usadas para definir variáveis de dados e cursores que são locais à função.  
  
-   A atribuição de valores a objetos locais à função, como o uso de `SET` para atribuir valores para escalar e para as variáveis locais à tabela.  
  
-   As operações de cursor que referenciam cursores locais são declaradas, abertas, fechadas e desalocadas na função. As instruções `FETCH` que retornam os dados aos clientes não são permitidas. Somente instruções FETCH que atribuem valores a variáveis locais usando a cláusula `INTO` são permitidas.  
  
-   Instruções de controle de fluxo, exceto instruções `TRY...CATCH`.  
  
-   Instruções `SELECT` com listas de seleção com expressões que atribuem valores às variáveis que são locais à função.  
  
-   Instruções `UPDATE`, `INSERT` e `DELETE` que modificam variáveis de tabela locais à função.  
  
-   Instruções `EXECUTE` que chamam um procedimento armazenado estendido.  
  
### <a name="built-in-system-functions"></a>Funções do sistema internas  
 As funções não determinísticas internas a seguir podem ser usadas nas funções definidas por usuário Transact-SQL.
  
:::row:::
    :::column:::
        CURRENT_TIMESTAMP
    :::column-end:::
    :::column:::
        @@MAX_CONNECTIONS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GET_TRANSMISSION_STATUS
    :::column-end:::
    :::column:::
        @@PACK_RECEIVED
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GETDATE
    :::column-end:::
    :::column:::
        @@PACK_SENT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GETUTCDATE
    :::column-end:::
    :::column:::
        @@PACKET_ERRORS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@CONNECTIONS
    :::column-end:::
    :::column:::
        @@TIMETICKS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@CPU_BUSY
    :::column-end:::
    :::column:::
        @@TOTAL_ERRORS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@DBTS
    :::column-end:::
    :::column:::
        @@TOTAL_READ
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IDLE
    :::column-end:::
    :::column:::
        @@TOTAL_WRITE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IO_BUSY
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
 As funções não determinísticas internas a seguir **não** podem ser usadas nas funções [!INCLUDE[tsql](../../includes/tsql-md.md)] definidas pelo usuário.  
  
:::row:::
    :::column:::
        NEWID
    :::column-end:::
    :::column:::
        RAND
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        NEWSEQUENTIALID
    :::column-end:::
    :::column:::
        TEXTPTR
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
 Para obter uma lista das funções internas do sistema determinísticas e não determinísticas, consulte [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
##  <a name="schema-bound-functions"></a><a name="SchemaBound"></a> Funções associadas a esquema  
 `CREATE FUNCTION` dá suporte a uma cláusula `SCHEMABINDING` que associa a função ao esquema de qualquer objeto que ela referencia, como tabelas, exibições e demais funções definidas pelo usuário. Uma tentativa para alterar ou descartar qualquer objeto referenciado por uma função associada a esquema falhará.  
  
 Essas condições devem ser cumpridas antes de especificar `SCHEMABINDING` em [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md):  
  
-   Todas as exibições e as funções definidas pelo usuário referenciadas pela função devem ser associadas a esquema.  
  
-   Todos os objetos referenciados pela função devem estar no mesmo banco de dados da função. Os objetos devem ser referenciados usando nomes de uma única parte ou nomes de duas partes.  
  
-   Você deve ter permissão `REFERENCES` em todos os objetos (tabelas, exibições e funções definidas pelo usuário) referenciados na função.  
  
 Você pode usar `ALTER FUNCTION` para remover a associação de esquema. A instrução `ALTER FUNCTION` deve redefinir a função sem especificar `WITH SCHEMABINDING`.  
  
##  <a name="specifying-parameters"></a><a name="Parameters"></a> Especificando parâmetros  
 Uma função definida pelo usuário usa parâmetros de entrada zero ou mais e retorna um valor escalar ou uma tabela. A função pode ter um máximo de 1024 parâmetros de entrada. Quando um parâmetro da função tiver um valor padrão, a palavra-chave DEFAULT deve ser especificada quando a função for chamada para obter o valor padrão. Esse comportamento é diferente dos parâmetros com valores padrão nos procedimentos armazenados definidos pelo usuário nos quais a omissão de parâmetro também implica o valor padrão. Funções definidas pelo usuário não dão suporte aos parâmetros de saída.  
  
##  <a name="more-examples"></a><a name="Tasks"></a> Mais exemplos!  
  
|Descrição da tarefa|Tópico|  
|-|-|    
|Descreve como criar uma função definida pelo usuário do Transact-SQL|[Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)|  
|Descreve como criar uma função CLR.|[Criar funções CLR](../../relational-databases/user-defined-functions/create-clr-functions.md)|  
|Descreve como criar uma função de agregação definida pelo usuário|[Criar agregações definidas pelo usuário](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)|  
|Descreve como modificar uma função definida pelo usuário do Transact-SQL|[Modificar funções definidas pelo usuário](../../relational-databases/user-defined-functions/modify-user-defined-functions.md)|  
|Descreve como excluir uma função definida pelo usuário.|[Excluir funções definidas pelo usuário](../../relational-databases/user-defined-functions/delete-user-defined-functions.md)|  
|Descreve como executar uma função definida pelo usuário.|[Executar funções definidas pelo usuário](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)|  
|Descreve como renomear uma função definida pelo usuário|[Renomear funções definidas pelo usuário](../../relational-databases/user-defined-functions/rename-user-defined-functions.md)|  
|Descreve como exibir a definição de uma função definida pelo usuário.|[Exibir funções definidas pelo usuário](../../relational-databases/user-defined-functions/view-user-defined-functions.md)|  
  
  
