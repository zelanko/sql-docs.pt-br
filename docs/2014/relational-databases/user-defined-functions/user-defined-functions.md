---
title: Funções definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], components
- user-defined functions [SQL Server], about user-defined functions
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1d8b8569a35a67d2700c0ce48c9c1cd4b29da7e1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427465"
---
# <a name="user-defined-functions"></a>Funções definidas pelo usuário
  Assim como as funções em linguagens de programação, as funções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definidas pelo usuário são rotinas que aceitam parâmetros, executam uma ação, como um cálculo complexo, e retornam o resultado dessa ação como um valor. O valor de retorno pode ser um único valor escalar ou um conjunto de resultados.  
  
 **Neste tópico**  
  
 [Benefícios da função definida pelo usuário](#Benefits)  
  
 [Tipos de funções](#FunctionTypes)  
  
 [Diretrizes](#Guidelines)  
  
 [Instruções válidas em uma função](#ValidStatements)  
  
 [Funções associadas a esquema](#SchemaBound)  
  
 [Especificando parâmetros](#Parameters)  
  
 [Tarefas relacionadas](#Tasks)  
  
##  <a name="Benefits"></a> Benefícios da função definida pelo usuário  
 Os benefícios de usar funções definidas pelo usuário em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são:  
  
-   Eles permitem programação modular.  
  
     Você pode criar a função uma vez, armazená-la no banco de dados e chamá-la quantas vezes quiser em seu programa. Funções definidas pelo usuário podem ser modificadas independentemente do código-fonte do programa.  
  
-   Elas permitem execução mais rápida.  
  
     Semelhantemente aos procedimentos armazenados, [!INCLUDE[tsql](../../includes/tsql-md.md)] as funções definidas pelo usuário reduzem o custo de compilação do código [!INCLUDE[tsql](../../includes/tsql-md.md)] colocando os planos em cache e reusando-os para execuções repetidas. Isso significa que a função definida pelo usuário não precisa ser reanalisada e reotimizada em cada utilização resultando em tempos de execução mais rápidos.  
  
     As funções CLR oferecem uma vantagem de desempenho significativa sobre funções [!INCLUDE[tsql](../../includes/tsql-md.md)] para tarefas de computação, manipulação de cadeias de caracteres e lógica de negócios. As funções [!INCLUDE[tsql](../../includes/tsql-md.md)] são mais adequadas à lógica intensiva de acesso a dados.  
  
-   Eles podem reduzir o tráfego de rede.  
  
     Uma operação que filtra dados com base em alguma restrição complexa que não pode ser expressa em uma única expressão escalar pode ser expressa como uma função. Em seguida, a função pode ser invocada na cláusula WHERE para reduzir o número ou linhas enviadas ao cliente.  
  
> [!NOTE]  
>  As funções definidas pelo usuário [!INCLUDE[tsql](../../includes/tsql-md.md)] em consultas só podem ser executadas em um único thread (plano de execução serial).  
  
##  <a name="FunctionTypes"></a> Tipos de funções  
 Função escalar  
 As funções escalares definidas pelo usuário retornam um valor único de dados do tipo definido na cláusula RETURNS. Para uma função escalar embutida, não há um corpo de função; o valor escalar é o resultado de uma única instrução. Para uma função escalar de várias instruções, o corpo da função, definido em um bloco BEGIN...END, contém uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , que retornam o valor único. O tipo de retorno pode ser qualquer tipo de dados, exceto `text`, `ntext`, `image`, `cursor`, e `timestamp`.  
  
 Funções com valor de tabela  
 As funções com valor de tabela definidos pelo usuário retornam um `table` tipo de dados. Para uma função com valor de tabela embutida, não há um corpo de função; a tabela é o conjunto de resultados de uma única instrução SELECT.  
  
 Funções de sistema  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece muitas funções de sistema que você pode usar para executar uma variedade de operações. Elas não podem ser modificadas. Para obter mais informações, consulte [Funções internas &#40;Transact-SQL&#41;](/sql/t-sql/functions/functions), [Funções armazenadas do sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/system-functions-for-transact-sql) e [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views).  
  
##  <a name="Guidelines"></a> Diretrizes  
 Erros de [!INCLUDE[tsql](../../includes/tsql-md.md)] que levam ao cancelamento de uma instrução e continuam com a instrução seguinte no módulo (como gatilhos ou procedimentos armazenados) tratados de modo diferente em uma função. Nas funções, esses erros fazem com que a execução da função seja interrompida. Em troca, isso faz com que a instrução que chamou a função seja cancelada.  
  
 As instruções em um bloco BEGIN... END não podem ter nenhum efeito colateral. Os efeitos colaterais da função são as alterações permanentes realizada no estado de um recurso que tem um escopo fora da função como uma modificação em uma tabela do banco de dados. As únicas alterações que podem ser feitas pelas instruções na função são alterações em objetos locais à função, como cursores ou variáveis locais. As modificações em tabelas de banco de dados, operações em cursores que não são locais à função, envio de e-mail, tentativa de modificação em catálogo e geração de um conjunto de resultados retornados ao usuário são exemplos de ações que não devem ser realizadas em uma função.  
  
> [!NOTE]  
>  Se a instrução CREATE FUNCTION produzir efeitos colaterais contra os recursos que não existem quanto a instrução CREATE FUNCTION é emitida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa a instrução. Porém, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não executa a função quando é chamada.  
  
 O número de vezes em que uma função especificada em uma consulta é realmente executada pode variar entre os planos de execução desenvolvidos pelo otimizador. Um exemplo é a função chamada por uma subconsulta em uma cláusula WHERE. O número de vezes em que a subconsulta e sua função são executadas pode variar com os caminhos de acesso diferentes escolhidos pelo otimizador.  
  
##  <a name="ValidStatements"></a> Instruções válidas em uma função  
 Os tipos de instruções que são válidos em uma função incluem:  
  
-   As instruções DECLARE podem ser usadas para definir variáveis de dados e cursores que são locais à função.  
  
-   A atribuição de valores a objetos locais à função, como o uso de SET para atribuir valores para escalar e para as variáveis locais à tabela.  
  
-   As operações de cursor que referenciam cursores locais são declaradas, abertas, fechadas e desalocadas na função. As instruções FETCH que retornam os dados aos clientes não são permitidas. Somente instruções FETCH que atribuem valores a variáveis locais usando a cláusula INTO são permitidas.  
  
-   Instruções de controle-de-fluxo exceto as instruções TRY ... CATCH.  
  
-   Instruções SELECT com listas de seleção com expressões que atribuem valores às variáveis que são locais à função.  
  
-   As instruções UPDATE, INSERT e DELETE que modificam variáveis de tabela que são locais à função.  
  
-   Instruções EXECUTE que chamam um procedimento armazenado estendido.  
  
### <a name="built-in-system-functions"></a>Funções do sistema internas  
 As funções não determinísticas internas a seguir podem ser usadas nas funções definidas por usuário Transact-SQL.  
  
|||  
|-|-|  
|CURRENT_TIMESTAMP|@@MAX_CONNECTIONS|  
|GET_TRANSMISSION_STATUS|@@PACK_RECEIVED|  
|GETDATE|@@PACK_SENT|  
|GETUTCDATE|@@PACKET_ERRORS|  
|@@CONNECTIONS|@@TIMETICKS|  
|@@CPU_BUSY|@@TOTAL_ERRORS|  
|@@DBTS|@@TOTAL_READ|  
|@@IDLE|@@TOTAL_WRITE|  
|@@IO_BUSY||  
  
 As funções não determinísticas internas a seguir não podem ser usadas nas funções definidas pelo usuário Transact-SQL.  
  
|||  
|-|-|  
|NEWID|RAND|  
|NEWSEQUENTIALID|TEXTPTR|  
  
 Para obter uma lista das funções internas do sistema determinísticas e não determinísticas, consulte [Funções determinísticas e não determinísticas](../user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
##  <a name="SchemaBound"></a> Funções associadas a esquema  
 CREATE FUNCTION dá suporte à cláusula SCHEMABINDING que associa a função ao esquema de qualquer objeto que ela referencia, como tabelas, exibições e demais funções definidas pelo usuário. Uma tentativa para alterar ou descartar qualquer objeto referenciado por uma função associada a esquema falhará.  
  
 Essas condições devem ser cumpridas antes de especificar SCHEMABINDING em CREATE FUNCTION:  
  
-   Todas as exibições e as funções definidas pelo usuário referenciadas pela função devem ser associadas a esquema.  
  
-   Todos os objetos referenciados pela função devem estar no mesmo banco de dados da função. Os objetos devem ser referenciados usando nomes de uma única parte ou nomes de duas partes.  
  
-   Você deve ter permissão REFERENCES em todos os objetos (tabelas, exibições e funções definidas pelo usuário) referenciados na função.  
  
 Você pode usar ALTER FUNCTION para remover a associação a esquema. A instrução ALTER FUNCTION deve redefinir a função sem especificar WITH SCHEMABINDING.  
  
##  <a name="Parameters"></a> Especificando parâmetros  
 Uma função definida pelo usuário usa parâmetros de entrada zero ou mais e retorna um valor escalar ou uma tabela. A função pode ter um máximo de 1024 parâmetros de entrada. Quando um parâmetro da função tiver um valor padrão, a palavra-chave DEFAULT deve ser especificada quando a função for chamada para obter o valor padrão. Esse comportamento é diferente dos parâmetros com valores padrão nos procedimentos armazenados definidos pelo usuário nos quais a omissão de parâmetro também implica o valor padrão. Funções definidas pelo usuário não dão suporte aos parâmetros de saída.  
  
##  <a name="Tasks"></a> Tarefas relacionadas  
  
|||  
|-|-|  
|**Descrição da tarefa**|**Tópico**|  
|Descreve como criar uma função definida pelo usuário do Transact-SQL|[Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](../user-defined-functions/create-user-defined-functions-database-engine.md)|  
|Descreve como criar uma função CLR.|[Criar funções CLR](../user-defined-functions/create-clr-functions.md)|  
|Descreve como criar uma função de agregação definida pelo usuário|[Criar agregações definidas pelo usuário](../user-defined-functions/create-user-defined-aggregates.md)|  
|Descreve como modificar uma função definida pelo usuário do Transact-SQL|[Modificar funções definidas pelo usuário](../user-defined-functions/user-defined-functions.md)|  
|Descreve como excluir uma função definida pelo usuário.|[Excluir funções definidas pelo usuário](../user-defined-functions/delete-user-defined-functions.md)|  
|Descreve como executar uma função definida pelo usuário.|[Executar funções definidas pelo usuário](../user-defined-functions/execute-user-defined-functions.md)|  
|Descreve como renomear uma função definida pelo usuário|[Renomear funções definidas pelo usuário](../user-defined-functions/rename-user-defined-functions.md)|  
|Descreve como exibir a definição de uma função definida pelo usuário.|[Exibir funções definidas pelo usuário](view-user-defined-functions.md)|  
  
  
