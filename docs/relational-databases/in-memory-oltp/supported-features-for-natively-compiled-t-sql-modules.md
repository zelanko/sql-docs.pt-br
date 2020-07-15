---
title: Recursos para módulos T-SQL compilados nativamente
description: Saiba mais sobre a área de superfície do T-SQL e os recursos com suporte no corpo de módulos T-SQL compilados nativamente, como procedimentos armazenados e funções escalares definidas pelo usuário.
ms.custom: seo-dt-2019
ms.date: 07/01/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 172e3a271086564c0ae4da7fd01a3084d65a85e5
ms.sourcegitcommit: edad5252ed01151ef2b94001c8a0faf1241f9f7b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85834717"
---
# <a name="supported-features-for-natively-compiled-t-sql-modules"></a>Recursos com suporte para módulos T-SQL compilados nativamente
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]


  Este tópico contém uma lista da área da superfície do T-SQL e os recursos com suporte no corpo de módulos T-SQL compilados nativamente, como procedimentos armazenados ([CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)), gatilhos, funções escalares definidas pelo usuário e funções embutidas com valor de tabela.  

 Para ver os recursos com suporte na definição de módulos nativos, consulte [DDL com suporte para módulos nativamente compilados do T-SQL](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md).  

 Para obter informações completas sobre construções sem suporte e sobre como resolver problemas de alguns recursos sem suporte em módulos compilados nativamente, consulte [Migration Issues for Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md). Para mais informações sobre os recursos sem suporte, veja [Constructos do Transact-SQL sem suporte no OLTP in-memory](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md).  

##  <a name="query-surface-area-in-native-modules"></a><a name="qsancsp"></a> Área da superfície da consulta em módulos nativos  

Há suporte para as seguintes construções de consulta:  

expressão CASE: CASE pode ser usada em qualquer instrução ou cláusula que permita uma expressão válida.
   - **Aplica-se a:** [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
    A partir do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], agora há suporte para instruções CASE para módulos T-SQL compilados nativamente.

Cláusula SELECT:  

-   Aliases de nome e colunas (usando a sintaxe = ou então AS).  

-   Subconsultas escalares
    - **Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].
      A partir do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], agora há suporte para subconsultas escalares em módulos compilados nativamente.

-   INÍCIO*  

-   SELECT DISTINCT  
    - **Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].
      A partir do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], há suporte para o operador DISTINCT em módulos compilados nativamente.

        - Não há suporte para agregações de DISTINCT.  

-   UNION e UNION ALL
    - **Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].
      A partir do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], agora há suporte para os operadores UNION e UNION ALL em módulos compilados nativamente.

-   Atribuições de variável  

Cláusula FROM:  

-   FROM \<memory optimized table or table variable>  

-   FROM \<natively compiled inline TVF>  

-   LEFT OUTER JOIN, RIGHT OUTER JOIN, CROSS JOIN e INNER JOIN.
    - **Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].
      A partir do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], agora há suporte para JOINS em módulos compilados nativamente.

-   Subconsultas `[AS] table_alias`. Para obter mais informações, consulte [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md). 
    - **Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].
      A partir do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], agora há suporte para subconsultas em módulos compilados nativamente.

Cláusula WHERE:  

-   Predicado de filtro IS [NOT] NULL  

-   AND, BETWEEN  
-   OR, NOT, IN, EXISTS
    - **Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].
      A partir do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], agora há suporte para operadores OR/NOT/IN/EXISTS em módulos compilados nativamente.


Cláusula[GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) :

- Funções de agregação AVG, COUNT, COUNT_BIG, MIN, MAX e SUM.  

- MIN e MAX não têm suporte para os tipos nvarchar, char, varchar, varchar, varbinary e binary.  

Cláusula[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md) :


- Não há suporte para **DISTINCT** na cláusula **ORDER BY** .


- tem suporte com [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md) se uma expressão na lista ORDER BY for exibida literalmente na lista GROUP BY.
  - Por exemplo, GROUP BY + b ORDER BY a + b tem suporte, mas GROUP BY a, b ORDER BY a + b, não.  


Cláusula HAVING:

- sujeito às mesmas limitações de expressão que a cláusula WHERE.


#### <a name="order-by-and-top-are-supported-in-natively-compiled-modules-with-some-restrictions"></a>ORDER BY e TOP têm suporte em módulos compilados nativamente, com algumas restrições


- Não há suporte para **WITH TIES** ou **PERCENT** na cláusula **TOP** .


- Não há suporte para **DISTINCT** na cláusula **ORDER BY** .  


- **TOP** combinado com **ORDER BY** não dá suporte a mais de 8.192 ao usar uma constante na cláusula **TOP** .
  - Esse limite poderá ser diminuído caso a consulta contenha junções ou funções de agregação. (Por exemplo, com uma junção (duas tabelas), o limite é 4.096 linhas. Com duas junções (três tabelas), o limite é 2.730 linhas.)  
  - Você pode obter resultados maiores que 8.192 armazenando o número de linhas em uma variável:  

```sql
DECLARE @v INT = 9000;
SELECT TOP (@v) ... FROM ... ORDER BY ...
```

No entanto, uma constante na cláusula **TOP** resulta em um desempenho melhor comparado a usar uma variável.  

Essas restrições em [!INCLUDE[tsql](../../includes/tsql-md.md)] compilado nativamente não se aplica ao acesso [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado em tabelas com otimização de memória.  


##  <a name="data-modification"></a><a name="dml"></a> Modificação de dados  

Há suporte para as instruções DML a seguir.  

-   INSERT VALUES (uma linha por instrução) e INSERT ... SELECT  

-   UPDATE  

-   Delete (excluir)  

-   WHERE tem suporte com instruções UPDATE e DELETE.  

##  <a name="control-of-flow-language"></a><a name="cof"></a> Linguagem de controle de fluxo  
 Há suporte para as construções de linguagem de controle de fluxo a seguir.  

-   [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  

-   [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  

-   [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)  

-   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md) pode usar todos os [Tipos de dados com suporte no OLTP in-memory](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md), bem como os tipos de tabela com otimização de memória. É possível declarar variáveis como NULL ou NOT NULL.  

-   [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  

-   [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  

    - Para obter um desempenho ideal, use um único bloco TRY/CATCH para um módulo T-SQL nativamente compilado inteiro.  

-   [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  

-   BEGIN ATOMIC (no nível externo do procedimento armazenado). Para obter mais detalhes, consulte [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  

##  <a name="supported-operators"></a><a name="so"></a> Operadores com suporte  
 Há suporte para os operadores que se seguem.  

-   [Operadores de comparação &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md) (por exemplo, >, \<, >= e <=)  

-   Operadores unários (+, -).  

-   Operadores binários (*, /, +, -, % (módulo)).  

    - O operador de adição (+) tem suporte em números e cadeias de caracteres.  

-   Operadores lógicos (AND, OR, NOT).  

-   Operadores bit a bit ~, &, |, e ^  

-   operador APPLY
    - **Aplica-se a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].  
      A partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], há suporte para o operador APPLY em módulos compilados nativamente.

##  <a name="built-in-functions-in-natively-compiled-modules"></a><a name="bfncsp"></a> Funções internas em módulos compilados nativamente  
 As funções a seguir têm suporte em restrições nas tabelas com otimização de memória e em módulos T-SQL compilados nativamente.  

-   Todas as [Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  

-   Funções de data: CURRENT_TIMESTAMP, DATEADD, DATEDIFF, DATEFROMPARTS, DATEPART, DATETIME2FROMPARTS, DATETIMEFROMPARTS, DAY, EOMONTH, GETDATE, GETUTCDATE, MONTH, SMALLDATETIMEFROMPARTS, SYSDATETIME, SYSUTCDATETIME e YEAR.  

-   Funções de cadeia de caracteres: LEN, LTRIM, RTRIM e SUBSTRING.  
    - **Aplica-se a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].  
      A partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], também há suporte para as seguintes funções internas: TRIM, TRANSLATE e CONCAT_WS.  

-   Funções de identidade: SCOPE_IDENTITY  

-   Funções NULL: ISNULL  

-   Funções uniqueidentifier: NEWID e NEWSEQUENTIALID  

-   Funções JSON  
    - **Aplica-se a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].  
      A partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], há suporte para as funções JSON em módulos compilados nativamente.

-   Funções de erro: ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY e ERROR_STATE  

-   Funções do sistema: @@rowcount. As instruções dentro de procedimentos armazenados compilados nativamente atualizam @@rowcount e você pode usar @@rowcount em um procedimento armazenado compilado nativamente para determinar o número de linhas afetadas pela última instrução executada nesse procedimento armazenado compilado nativamente. No entanto, @@rowcount é redefinido como 0 no início e no final da execução de um procedimento armazenado compilado nativamente.  

-   Funções de segurança: IS_MEMBER({'group' | 'role'}), IS_ROLEMEMBER ('role' [, 'database_principal']), IS_SRVROLEMEMBER ('role' [, 'login']), ORIGINAL_LOGIN(), SESSION_USER, CURRENT_USER, SUSER_ID(['login']), SUSER_SID(['login'] [, Param2]), SUSER_SNAME([server_user_sid]), SYSTEM_USER, SUSER_NAME, USER, USER_ID(['user']), USER_NAME([id]), CONTEXT_INFO().

-   Execuções de módulos nativos podem ser aninhadas.

##  <a name="auditing"></a><a name="auditing"></a> Auditoria  
 A auditoria no nível de procedimento tem suporte em procedimentos armazenados compilados nativamente.  

 Para obter mais informações sobre a auditoria, consulte [Criar uma especificação de auditoria de banco de dados e de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md).  

##  <a name="table-and-query-hints"></a><a name="tqh"></a> Dicas de tabela e de consulta  
 Há suporte para o seguinte:  

-   As dicas INDEX, FORCESCAN e FORCESEEK, seja na sintaxe das dicas de tabela ou na [Cláusula OPTION &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md) da consulta. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  

-   FORCE ORDER  

-   Dica de LOOP JOIN  

-   OPTIMIZE FOR  

 Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  

##  <a name="limitations-on-sorting"></a><a name="los"></a> Limitações na classificação  
 Você pode classificar maior que 8.000 linhas em uma consulta que usa [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) e uma [Cláusula ORDER BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md). No entanto, sem a [Cláusula ORDER BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md), [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) pode classificar até 8.000 linhas (menos linhas se houver junções).  

 Se sua consulta usar o operador [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) e uma [Cláusula ORDER BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md), você pode especificar até 8192 linhas para o operador TOP. Se você especificar mais de 8192 linhas, receberá a mensagem de erro: **Msg 41398, Nível 16, Estado 1, Procedimento *\<procedureName>* , Linha *\<lineNumber>* O operador TOP pode retornar no máximo 8192 linhas; *\<number>* foi solicitado.**  

 Se você não tiver uma cláusula TOP, poderá classificar qualquer número de linhas com ORDER BY.  

 Se você não usar uma cláusula ORDER BY, poderá usar qualquer valor inteiro com o operador TOP.  

 Exemplo com TOP N = 8192: compila  

```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8192 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```

 Exemplo com TOP N > 8192: não compila.  

```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8193 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```

 A limitação de 8192 linhas só se aplica a `TOP N` onde `N` é uma constante, como nos exemplos anteriores.  Se você precisar de `N` maior que 8192, poderá atribuir o valor a uma variável e usar essa variável com `TOP`.  

 Exemplo usando uma variável: compila  

```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    DECLARE @v int = 8193   
    SELECT TOP (@v) ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```

 **Limitações nas linhas retornadas:** há dois casos em que isso pode, potencialmente, reduzir o número de linhas a serem retornadas pelo operador TOP:  

-   Uso de JOINs na consulta.  A influência de JOINs na limitação depende do plano de consulta.  

-   Uso de funções de agregação ou de referências a funções de agregação na cláusula ORDER BY.  

 A fórmula para calcular o pior caso de N com suporte em TOP N é: `N = floor ( 65536 / number_of_tables * 8 + total_size+of+aggs )`.  

## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)   
 [Problemas de migração para procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  


