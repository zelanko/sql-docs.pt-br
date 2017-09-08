---
title: DEFINIR @local_variable (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SET @local_variable
- variables [SQL Server], assigning
- SET statement, @local_variable
- local variables [SQL Server]
ms.assetid: d410e06e-061b-4c25-9973-b2dc9b60bd85
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a92fa424de70d1ba9cccf437a2de49ab8432ba1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="set-localvariable-transact-sql"></a>DEFINIR @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Define a variável local especificada, criada anteriormente usando o DECLARE @*local_variable* instrução, para o valor especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET   
{ @local_variable  
    [ . { property_name | field_name } ] = { expression | udt_name { . | :: } method_name }  
}  
|  
{ @SQLCLR_local_variable.mutator_method  
}  
|  
{ @local_variable  
    {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
}  
|   
  { @cursor_variable =   
    { @cursor_variable | cursor_name   
    | { CURSOR [ FORWARD_ONLY | SCROLL ]   
        [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
        [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
        [ TYPE_WARNING ]   
    FOR select_statement   
        [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]   
      }   
    }  
}   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET @local_variable {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 **@***local_variable*  
 É o nome de uma variável de qualquer tipo, exceto **cursor**, **texto**, **ntext**, **imagem**, ou **tabela**. Nomes de variável devem começar com um sinal de arroba (**@**). Nomes de variáveis devem estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *Property_Name*  
 É uma propriedade de um tipo definido pelo usuário.  
  
 *nome_do_campo*  
 É um campo público de um tipo definido pelo usuário.  
  
 *udt_name*  
 É o nome de um tipo de dados CLR (Common Language Runtime) definido pelo usuário.  
  
 { **.** | **::** }  
 Especifica um método de um tipo de dados CLR definido pelo usuário. Para um método de instância (não estático), use um ponto (**.**). Para um método estático, use dois-pontos duplos (**::**). Para invocar um método, uma propriedade ou um campo de um tipo de dados CLR definido pelo usuário, você deve ter a permissão EXECUTE no tipo.  
  
 *nome_do_método* **(** *argumento* [ **,**... *n* ] **)**  
 É um método de um tipo definido pelo usuário que obtém um ou mais argumentos para modificar o estado de uma instância de um tipo. Os métodos estáticos devem ser públicos.  
  
 **@***SQLCLR_local_variable*  
 É uma variável cujo tipo está localizado em um assembly. Para obter mais informações, consulte [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md).  
  
 *mutator_method*  
 É um método no assembly que pode alterar o estado do objeto. SQLMethodAttribute.IsMutator será se aplicado a este método.  
  
 { **+=** | **-=** | **\*=** | **/=** | **%=** | **&=** | **^=** | **|=** }  
 Operador de atribuição composto:  
  
 + = Somar e atribuir  
  
 -= Subtrair e atribuir  
  
 * = Multiplicar e atribuir  
  
 / = Dividir e atribuir  
  
 % = Módulo e atribuir  
  
 & = AND bit a bit e atribuir  
  
 ^ = XOR bit a bit e atribuir  
  
 | = OR bit a bit e atribuir  
  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *cursor_variable*  
 É o nome de uma variável de cursor. Se a variável de cursor de destino tiver mencionado anteriormente um cursor diferente, essa referência anterior será removida.  
  
 *cursor_name*  
 É o nome de um cursor declarado usando a instrução DECLARE CURSOR.  
  
 CURSOR  
 Especifica que a instrução SET contém uma declaração de um cursor.  
  
 SCROLL  
 Especifica que o cursor oferece o suporte para todas as opções de busca: FIRST, LAST, NEXT, PRIOR, RELATIVE e ABSOLUTE. SCROLL não pode ser especificado quando FAST_FORWARD também está especificado.  
  
 FORWARD_ONLY  
 Especifica que o cursor oferece suporte somente para a opção FETCH NEXT. O cursor pode ser recuperado somente em uma direção, da primeira para a última linha. Quando FORWARD_ONLY está especificado sem as palavras-chave STATIC, KEYSET ou DYNAMIC, o cursor é implementado como DYNAMIC. Quando FORWARD_ONLY ou SCROLL não estiverem especificados, FORWARD_ONLY será o padrão; a não ser que as palavras-chave STATIC, KEYSET ou DYNAMIC estejam especificadas. Para os cursores STATIC, KEYSET e DYNAMIC, SCROLL é o padrão.  
  
 STATIC  
 Define um cursor que faz uma cópia temporária dos dados a serem usados por ele. Todas as solicitações para o cursor são respondidas a partir desta tabela temporária em tempdb; portanto, as modificações feitas na tabelas base não são refletidas nos dados retornados pelas buscas feitas nesse cursor, que não permite modificações.  
  
 KEYSET  
 Especifica que a associação e a ordem de linhas no cursor são fixas, quando o cursor é aberto. O conjunto de chaves que identificam exclusivamente as linhas é criado em keysettable em tempdb. Alterações em valores não chave nas tabelas base, realizadas pelo proprietário do cursor ou confirmadas por outros usuários, são visíveis como rolagens do proprietário ao redor do cursor. As inserções feitas por outros usuários não são visíveis e não é possível fazer inserções por um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Se uma linha for excluída, uma tentativa de buscar a linha retorna um @@FETCH_STATUS de -2. As atualizações de valores de chave externas ao cursor são similares à exclusão de uma linha antiga, seguida de uma inserção de uma nova linha. A linha com os novos valores não estiver visível, e tenta buscar a linha com os valores antigos retorna um @@FETCH_STATUS de -2. Os novos valores ficarão visíveis se a atualização for executada através do cursor, especificando-se a cláusula WHERE CURRENT OF.  
  
 DYNAMIC  
 Define um cursor que reflete todas as mudanças de dados feitas nas linhas no seu conjunto de resultados conforme o proprietário rola o cursor. Os valores de dados, a ordem e a associação das linhas podem ser alterados em cada busca. As opções de busca absoluta e relativa não têm suporte em cursores dinâmicos.  
  
 FAST_FORWARD  
 Especifica um cursor FORWARD_ONLY, READ_ONLY, com otimizações habilitadas. FAST_FORWARD não pode ser especificado quando SCROLL também está especificado.  
  
 READ_ONLY  
 Impede que esse cursor faça atualizações. O cursor não pode ser referenciado em uma cláusula WHERE CURRENT OF em uma instrução UPDATE ou DELETE. Essa opção anula a funcionalidade padrão de um cursor para ser atualizado.  
  
 SCROLL LOCKS  
 Especifica se atualizações posicionadas ou exclusões feitas pelo cursor têm garantia de êxito. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueia as linhas à medida que são lidas no cursor para garantir a disponibilidade para modificações posteriores. SCROLL_LOCKS não pode ser especificado quando FAST_FORWARD também está especificado.  
  
 OPTIMISTIC  
 Especifica que as atualizações posicionadas e exclusões realizadas pelo cursor não terão êxito se a linha tiver sido atualizada desde que foi lida no cursor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não bloqueia linhas à medida que são lidas no cursor. Em vez disso, ele usa comparações de valores de coluna timestamp, ou um valor de soma de verificação se a tabela não tiver nenhuma coluna timestamp, para determinar se a linha foi modificada depois de lida no cursor. Se a linha tiver sido modificada, a tentativa de atualização ou exclusão posicionada falhará. OPTIMISTIC não poderá ser especificado quando FAST_FORWARD também estiver especificado.  
  
 TYPE_WARNING  
 Especifica que uma mensagem de aviso é enviada ao cliente quando o cursor é convertido implicitamente em outro a partir do tipo solicitado.  
  
 PARA *select_statement*  
 É uma instrução SELECT padrão que define o conjunto de resultados de um cursor. As palavras-chave FOR BROWSE e INTO não são permitidas dentro de *select_statement* de uma declaração de cursor.  
  
 Se DISTINCT, UNION, GROUP BY ou HAVING são usadas, ou uma expressão de agregação é incluída no *select_list*, o cursor será criado como STATIC.  
  
 Se cada tabela subjacente não tiver um índice exclusivo e um cursor ISO SCROLL ou um cursor [!INCLUDE[tsql](../../includes/tsql-md.md)] KEYSET for solicitado, ele será automaticamente um cursor STATIC.  
  
 Se *select_statement* contém uma cláusula ORDER BY na qual as colunas não são identificadores de linha exclusivo, um cursor dinâmico é convertido em um cursor KEYSET, ou para um cursor estático se um cursor de conjunto de chaves não pode ser aberto. Isto também acontece para um cursor definido com a sintaxe ISO, mas sem a palavra-chave STATIC.  
  
 READ ONLY  
 Impede que esse cursor faça atualizações. O cursor não pode ser referenciado em uma cláusula WHERE CURRENT OF em uma instrução UPDATE ou DELETE. Essa opção anula a funcionalidade padrão de um cursor para ser atualizado. Essa palavra-chave é diferente do READ_ONLY anterior, pois tem um espaço em vez de um sublinhado entre READ e ONLY.  
  
 ATUALIZAÇÃO [OF *column_name*[ **,**... *n* ] ]  
 Define colunas atualizáveis em um cursor. Se OF *column_name* [**,**...  *n* ] for fornecido, somente as colunas listadas permitirão modificações. Se nenhuma lista for fornecida, todas as colunas poderão ser atualizadas, a menos que o cursor tenha sido definido como READ_ONLY.  
  
## <a name="remarks"></a>Comentários  
 Depois de uma variável ser declarada, ela é inicializada como NULL. Use a instrução SET para atribuir um valor que não é NULL a uma variável declarada. A instrução SET que atribui um valor à variável retorna um único valor. Ao inicializar várias variáveis, use uma instrução SET separada para cada variável local.  
  
 As variáveis podem ser usadas somente em expressões, não em nomes de objeto ou palavras-chave. Para construir instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] dinâmicas, use EXECUTE.  
  
 As regras de sintaxe para definir  **@**  *cursor_variable* não incluem as palavras-chave LOCAL e GLOBAL. Quando o conjunto  **@**  *cursor_variable* = CURSOR... sintaxe é usada, o cursor é criado como GLOBAL ou LOCAL, dependendo da configuração padrão da opção de banco de dados de cursor local.  
  
 As variáveis de cursor sempre são locais, mesmo se fizerem referência a um cursor global. Quando uma variável de cursor faz referência a um cursor global, o cursor tem as duas referências, uma global e uma local. Para obter mais informações, veja o Exemplo C.  
  
 Para obter mais informações, consulte [DECLARE CURSOR &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
 O operador de atribuição composto pode ser usado em qualquer lugar onde haja uma atribuição com uma expressão à direita do operador, incluindo variáveis, e uma instrução SET e uma instrução UPDATE, SELECT e RECEIVE.  
  
 Não use uma variável em uma instrução SELECT para concatenar valores (ou seja, para computar valores agregados). Resultados inesperados de consulta podem ocorrer. Isso ocorre porque todas as expressões na lista SELECT (incluindo atribuições) não têm garantia de serem executadas exatamente uma vez para cada linha de saída. Para obter mais informações, consulte [neste artigo da KB](http://support.microsoft.com/kb/287515).  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public. Todos os usuários podem usar SET  **@**  *local_variable*.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-printing-the-value-of-a-variable-initialized-by-using-set"></a>A. Imprimindo o valor de uma variável inicializada com a instrução SET  
 O exemplo a seguir cria o `@myvar` variável, coloca um valor de cadeia de caracteres na variável e imprime o valor do `@myvar` variável.  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT @myvar;  
GO  
```  
  
### <a name="b-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>B. Usando uma variável local que atribuiu um valor usando a instrução SET em uma instrução SELECT  
 O exemplo a seguir cria uma variável local chamada `@state` e usa essa variável em uma instrução `SELECT` para localizar o nome e o sobrenome de todos os funcionários que moram no estado de `Oregon`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @state char(25);  
SET @state = N'Oregon';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name, City  
FROM HumanResources.vEmployee  
WHERE StateProvinceName = @state;  
```  
  
### <a name="c-using-a-compound-assignment-for-a-local-variable"></a>C. Usando uma atribuição composta para uma variável local  
 Os dois exemplos a seguir produzem o mesmo resultado. Eles criam uma variável local chamada `@NewBalance`, multiplicam-na por 10 e exibem o novo valor da variável local em uma instrução `SELECT`. O segundo exemplo usa um operador de atribuição composto.  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  @NewBalance;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT @NewBalance;  
```  
  
### <a name="d-using-set-with-a-global-cursor"></a>D. Usando SET com um cursor global  
 O exemplo a seguir cria uma variável local e define a variável de cursor como o nome de cursor global.  
  
```  
DECLARE my_cursor CURSOR GLOBAL   
FOR SELECT * FROM Purchasing.ShipMethod  
DECLARE @my_variable CURSOR ;  
SET @my_variable = my_cursor ;   
--There is a GLOBAL cursor declared(my_cursor) and a LOCAL variable  
--(@my_variable) set to the my_cursor cursor.  
DEALLOCATE my_cursor;   
--There is now only a LOCAL variable reference  
--(@my_variable) to the my_cursor cursor.  
```  
  
### <a name="e-defining-a-cursor-by-using-set"></a>E. Definindo um cursor com a instrução SET  
 O exemplo a seguir usa a instrução `SET` para definir um cursor.  
  
```  
DECLARE @CursorVar CURSOR;  
  
SET @CursorVar = CURSOR SCROLL DYNAMIC  
FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN @CursorVar;  
  
FETCH NEXT FROM @CursorVar;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM @CursorVar  
END;  
  
CLOSE @CursorVar;  
DEALLOCATE @CursorVar;  
```  
  
### <a name="f-assigning-a-value-from-a-query"></a>F. Atribuindo um valor de uma consulta  
 O exemplo a seguir usa uma consulta para atribuir um valor a uma variável.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM Sales.Customer);  
SELECT @rows;  
```  
  
### <a name="g-assigning-a-value-to-a-user-defined-type-variable-by-modifying-a-property-of-the-type"></a>G. Atribuindo um valor a uma variável de tipo definido pelo usuário com a modificação de uma propriedade do tipo  
 O exemplo a seguir define o valor para o tipo `Point` definido pelo usuário modificando o valor da propriedade `X` do tipo.  
  
```  
DECLARE @p Point;  
SET @p.X = @p.X + 1.1;  
SELECT @p;  
GO  
```  
  
### <a name="h-assigning-a-value-to-a-user-defined-type-variable-by-invoking-a-method-of-the-type"></a>H. Atribuindo um valor a uma variável de tipo definida com a invocação de um método do tipo  
 O exemplo a seguir define um valor para o tipo definido pelo usuário **ponto** invocando o método `SetXY` do tipo.  
  
```  
DECLARE @p Point;  
SET @p=point.SetXY(23.5, 23.5);  
```  
  
### <a name="i-creating-a-variable-for-a-clr-type-and-calling-a-mutator-method"></a>I. Criando uma variável para um tipo CLR e chamando um método modificador  
 O exemplo a seguir cria uma variável para o tipo `Point` e, depois, executa um método modificador em `Point`.  
  
```  
CREATE ASSEMBLY mytest from 'c:\test.dll' WITH PERMISSION_SET = SAFE  
CREATE TYPE Point EXTERNAL NAME mytest.Point  
GO  
DECLARE @p Point = CONVERT(Point, '')  
SET @p.SetXY(22, 23);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-printing-the-value-of-a-variable-initialized-by-using-set"></a>J. Imprimindo o valor de uma variável inicializada com a instrução SET  
 O exemplo a seguir cria o `@myvar` variável, coloca um valor de cadeia de caracteres na variável e imprime o valor do `@myvar` variável.  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT top 1 @myvar FROM sys.databases;  
  
```  
  
### <a name="k-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>K. Usando uma variável local que atribuiu um valor usando a instrução SET em uma instrução SELECT  
 O exemplo a seguir cria uma variável local chamada `@dept` e usa essa variável em uma `SELECT` instrução para localizar os nomes e sobrenomes de todos os funcionários que trabalham no `Marketing` departamento.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @dept char(25);  
SET @dept = N'Marketing';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name  
FROM DimEmployee   
WHERE DepartmentName = @dept;  
```  
  
### <a name="l-using-a-compound-assignment-for-a-local-variable"></a>L. Usando uma atribuição composta para uma variável local  
 Os dois exemplos a seguir produzem o mesmo resultado. Eles criam uma variável local chamada `@NewBalance`, multiplica por `10` e exibe o novo valor da variável local em um `SELECT` instrução. O segundo exemplo usa um operador de atribuição composto.  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  TOP 1 @NewBalance FROM sys.tables;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT TOP 1 @NewBalance FROM sys.tables;  
```  
  
### <a name="m-assigning-a-value-from-a-query"></a>M. Atribuindo um valor de uma consulta  
 O exemplo a seguir usa uma consulta para atribuir um valor a uma variável.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM dbo.DimCustomer);  
SELECT TOP 1 @rows FROM sys.tables;  
```  
  
## <a name="see-also"></a>Consulte também  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


