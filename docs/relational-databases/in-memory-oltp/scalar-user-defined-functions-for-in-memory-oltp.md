---
title: "Funções escalares definidas pelo usuário para OLTP in-memory | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d2546e40-fdfc-414b-8196-76ed1f124bf5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec9be02546a7402b1451a94ff9bc9fd0357e7210
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="scalar-user-defined-functions-for-in-memory-oltp"></a>Funções escalares definidas pelo usuário para OLTP na Memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode criar e remover funções escalares definidas pelo usuário compiladas de modo nativo. Também pode alterar essas funções definidas pelo usuário. A compilação nativa melhora o desempenho da avaliação de funções definidas pelo usuário no Transact-SQL.  
  
 Quando você altera uma função escalar definida pelo usuário e compilada nativamente, o aplicativo permanecerá disponível enquanto a operação estiver sendo executada e a nova versão da função estiver sendo compilada.  
  
 Para obter os constructos T-SQL com suporte, veja [Recursos com suporte para módulos T-SQL compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
## <a name="creating-dropping-and-altering-user-defined-functions"></a>Criando, ignorando e alterando funções definidas pelo usuário  
 Você pode usar CREATE FUNCTION para criar a função escalar definida pelo usuário e compilada nativamente, a função DROP FUNCTION para remover a função definida pelo usuário e a função ALTER FUNCTION para alterar a função. BEGIN ATOMIC WITH é necessário para as funções definidas pelo usuário.  
  
 Para saber mais sobre a sintaxe com suporte e as restrições, veja os tópicos a seguir.  
  
-   [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
-   [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)  
  
-   [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)  
  
     A sintaxe DROP FUNCTION para funções escalares definidas pelo usuário e compiladas nativamente é a mesma para funções interpretadas definidas pelo usuário.  
  
-   [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
 O procedimento armazenado [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) pode ser usado com a função escalar definida pelo usuário e compilada de modo nativo. Isso fará a função ser recompilada usando a definição que existe nos metadados.  
  
 O exemplo a seguir mostra uma UDF escalar do banco de dados de exemplo [AdventureWorks2016CTP3](https://www.microsoft.com/download/details.aspx?id=49502) .  
  
```sql  
CREATE FUNCTION [dbo].[ufnLeadingZeros_native](@Value int)   
RETURNS varchar(8)   
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
  
    DECLARE @ReturnValue varchar(8);  
    SET @ReturnValue = CONVERT(varchar(8), @Value);  
       DECLARE @i int = 0, @count int = 8 - LEN(@ReturnValue)  
  
    WHILE @i < @count  
       BEGIN  
            SET @ReturnValue = '0' + @ReturnValue;  
            SET @i += 1  
       END  
  
    RETURN (@ReturnValue);  
  
END  
```  
  
## <a name="calling-user-defined-functions"></a>Chamando funções definidas pelo usuário  
 As funções escalares definidas pelo usuário e compiladas nativamente podem ser usadas em expressões, no mesmo local que as funções escalares internas e as funções escalares interpretadas definidas pelo usuário. As funções escalares definidas pelo usuário e compilados também podem ser usadas com a instrução EXECUTE em uma instrução Transact-SQL e em um procedimento armazenado compilado nativamente.  
  
 Você pode usar essas funções escalares definidas pelo usuário em procedimentos armazenados compilados nativamente e funções definidas pelo usuário e compiladas nativamente, onde as funções internas forem permitidas. Você também pode usar funções escalares definidas pelo usuário e compiladas nativamente em módulos tradicionais de Transact-SQL.  
  
 Você pode usar essas funções escalares definidas pelo usuário em modo de interoperabilidade, sempre que uma função escalar interpretada definida pelo usuário puder ser usada. Esse uso está sujeito a limitações de transação entre contêineres, conforme descrito na seção **Níveis de isolamento com suporte para transações entre contêineres** no [Transações com tabelas com otimização de memória](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md). Para obter mais informações sobre o modo de interoperabilidade, veja [Acessando tabelas com otimização de memória usando Transact-SQL interpretado](../../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md).  
  
 As funções escalares definidas pelo usuário e compiladas nativamente exigem um contexto de execução explícito. Para obter mais informações, veja [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md). EXECUTE AS CALLER não tem suporte. Para obter mais informações, veja [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
 Para obter a sintaxe com suporte para as instruções Execute do Transact-SQL, para funções escalares definidas pelo usuário e compiladas de modo nativo, veja [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md). Para obter a sintaxe com suporte para executar as funções definidas pelo usuário em um procedimento armazenado compilado de modo nativo, veja [Recursos com suporte em módulos T-SQL compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
## <a name="hints-and-parameters"></a>Dicas e parâmetros  
 O suporte para tabela, junção e dicas de consulta dentro de funções escalares definidas pelo usuário e compiladas nativamente é igual ao suporte para essas dicas para procedimentos armazenados compilados nativamente. Assim como acontece com funções escalares interpretadas definidas pelo usuário, as dicas de consulta incluídas com uma consulta Transact-SQL que fazem referência a uma função escalar definida pelo usuário e compilada nativamente não afetam o plano de consulta para essa função definida pelo usuário.  
  
 Os parâmetros com suporte para as funções escalares definidas pelo usuário e compiladas nativamente são todos com suporte para procedimentos armazenados compilados nativamente, desde que os parâmetros sejam permitidos para funções escalares definidas pelo usuário. Um exemplo de um parâmetro com suporte é o parâmetro com valor de tabela.  
  
## <a name="schema-bound"></a>Associada a esquema  
 O item a seguir aplica-se a funções escalares definidas pelo usuário compiladas de modo nativo.  
  
-   Deve ser associada a um esquema, usando o argumento WITH SCHEMABINDING no CREATE FUNCTION e ALTER FUNCTION.  
  
-   Não pode ser descartada ou alterada quando referenciada por um procedimento armazenado de associação a esquema ou função definida pelo usuário.  
  
## <a name="showplanxml"></a>SHOWPLAN_XML  
 Funções escalares definidas pelo usuário compiladas de modo nativo dão suporte a SHOWPLAN_XML. Ele segue o esquema geral SHOWPLAN_XML, assim como acontece com procedimentos armazenados compilados nativamente. O elemento base para as funções definidas pelo usuário é `<UDF>`.  
  
 STATISTICS XML não tem suporte para funções escalares definidas pelo usuário e compiladas nativamente. Quando você executa uma consulta que referencia a função definida pelo usuário, com STATISTICS XML habilitado, o conteúdo de XML é retornado sem a parte da função definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Assim como acontece com procedimentos armazenados compilados nativamente, as permissões para objetos referenciados de uma função escalar definida pelo usuário e compilada nativamente são verificadas quando a função é criada. CREATE FUNCTION falhará se o usuário representado não tiver as permissões corretas. Se as alterações de permissão fizerem o usuário representado perder as permissões corretas, haverá falha nas execuções subsequentes da função definida pelo usuário.  
  
 Quando você usa uma função escalar definida pelo usuário e compilada nativamente dentro de um procedimento armazenado compilado nativamente, as permissões para executar a função definida pelo usuário serão verificadas quando o procedimento externo tiver sido criado. Se o usuário representado pelo procedimento externo não tiver permissões EXEC para a função definida pelo usuário, haverá falha na criação do procedimento armazenado. Se as alterações de permissão fizerem o usuário perder as permissões de EXEC, ocorrerá falha na execução do procedimento externo.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Salvar um plano de execução em formato XML](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
