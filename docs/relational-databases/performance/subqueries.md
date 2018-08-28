---
title: Subconsultas (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/18/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Subquery
- Subqueries
- subqueries [SQL Server], fundamentals
- subqueries [SQL Server], correlated
- subqueries [SQL Server], types
ms.assetid: bfc97432-c14c-4768-9dc5-a9c512f6b2bd
caps.latest.revision: 52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9ae4e084911158fc56705d4b09e1e60d50ffb95a
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43063737"
---
# <a name="subqueries-sql-server"></a>Subconsultas (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 
Uma subconsulta é uma consulta que está aninhada dentro de uma instrução `SELECT`, `INSERT`, `UPDATE` ou `DELETE` ou em outra subconsulta. Uma subconsulta pode ser usada em qualquer lugar em que é permitida uma expressão. Neste exemplo, uma subconsulta é usada como uma expressão de coluna denominada MaxUnitPrice em uma instrução SELECT.

```sql
USE AdventureWorks2016;
GO
SELECT Ord.SalesOrderID, Ord.OrderDate,
    (SELECT MAX(OrdDet.UnitPrice)
     FROM Sales.SalesOrderDetail AS OrdDet
     WHERE Ord.SalesOrderID = OrdDet.SalesOrderID) AS MaxUnitPrice
FROM Sales.SalesOrderHeader AS Ord;
GO
```

## <a name="fundamentals"></a> Noções básicas sobre subconsultas
Uma subconsulta também é chamada de uma consulta interna ou seleção interna, enquanto a instrução que contém uma subconsulta também é chamada de uma consulta externa ou seleção externa.   

Muitas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que incluem subconsultas podem ser alternativamente formuladas como junções. Outras perguntas só podem ser feitas com subconsultas. Em [!INCLUDE[tsql](../../includes/tsql-md.md)], normalmente não há nenhuma diferença de desempenho entre uma instrução que inclui uma subconsulta e uma versão equivalente semanticamente que não inclui. Entretanto, em alguns casos em que a existência deve ser verificada, uma junção tem um desempenho melhor. Em outros casos, a consulta aninhada deve ser processada para cada resultado da consulta externa para assegurar a eliminação de duplicatas. Em tais casos, uma abordagem de junção geraria resultados melhores. O exemplo seguinte mostra uma subconsulta `SELECT` e uma junção `SELECT` que retornam o mesmo conjunto de resultados:

```sql
USE AdventureWorks2016;
GO

/* SELECT statement built using a subquery. */
SELECT Name
FROM Production.Product
WHERE ListPrice =
    (SELECT ListPrice
     FROM Production.Product
     WHERE Name = 'Chainring Bolts' );
GO

/* SELECT statement built using a join that returns
   the same result set. */
SELECT Prd1. Name
FROM Production.Product AS Prd1
     JOIN Production.Product AS Prd2
       ON (Prd1.ListPrice = Prd2.ListPrice)
WHERE Prd2. Name = 'Chainring Bolts';
GO
```

Uma subconsulta aninhada na instrução SELECT externa tem os seguintes componentes:    
-   Uma consulta regular `SELECT` incluindo os componentes regulares de lista de seleção.   
-   Uma cláusula regular `FROM` que inclui um ou mais nomes de tabela ou de exibição.   
-   Uma cláusula `WHERE` opcional.   
-   Uma cláusula `GROUP BY` opcional.   
-   Uma cláusula `HAVING` opcional.   

A consulta SELECT de uma subconsulta sempre é inclusa em parênteses. Não pode incluir uma cláusula `COMPUTE` ou `FOR BROWSE` e apenas pode incluir uma cláusula `ORDER BY` quando uma cláusula TOP também for especificada.   

Uma subconsulta pode ser aninhada na cláusula `WHERE` ou `HAVING` de uma instrução `SELECT`, `INSERT`, `UPDATE` ou `DELETE` externa ou em outra subconsulta. Até 32 níveis de aninhamento são possíveis, embora o limite varie com base na memória disponível e na complexidade de outras expressões da consulta. É possível que consultas individuais não ofereçam suporte a aninhamento até 32 níveis. Uma subconsulta pode aparecer em qualquer lugar em que uma expressão possa ser usada, se retornar um único valor.   

Se uma tabela só aparecer em uma subconsulta e não na consulta externa, então não poderão ser incluídas colunas dessa tabela na saída (a lista de seleção da consulta externa).   

Instruções que incluem uma subconsulta normalmente têm um destes formatos:   
-   Expressão WHERE \[NOT] IN (subconsulta)
-   Expressão WHERE comparison_operator \[ANY | ALL] (subconsulta)
-   WHERE \[NOT] EXISTS (subconsulta)   

Em algumas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], a subconsulta pode ser avaliada como se fosse uma consulta independente. Conceitualmente, os resultados da subconsulta são substituídos na consulta externa (embora isso não seja necessariamente como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processa de fato instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] com subconsultas).    

Há três tipos básicos de subconsultas. Aquelas que: 
-   Funcionam em listas introduzidas com `IN`, ou aquelas em que um operador de comparação modificou por `ANY` ou `ALL`.
-   São introduzidas com um operador de comparação inalterado e devem retornar um único valor.
-   São testes de existência introduzidos com `EXISTS`.

## <a name="rules"></a> Regras de subconsulta
Uma subconsulta está sujeita às seguintes restrições: 
-   A lista de seleção de uma subconsulta introduzida com um operador de comparação pode incluir apenas uma expressão ou um nome de coluna (exceto que `EXISTS` e `IN` operam em `SELECT *` ou em uma lista, respectivamente).   
-   Se a cláusula `WHERE` de uma consulta externa incluir um nome de coluna, ela deverá ser compatível com junção com a coluna na lista de seleção da subconsulta.   
-   Os tipos de dados **ntext**, **text**, e **image** não podem ser usados na lista de seleção de subconsultas.   
-   Como devem retornar um único valor, as subconsultas introduzidas por um operador de comparação inalterado (não seguido pela palavra-chave ANY ou ALL) não podem incluir as cláusulas `GROUP BY` e `HAVING`.   
-   A palavra-chave `DISTINCT` não pode ser usada com subconsultas que incluem GROUP BY.
-   As cláusulas `COMPUTE` e `INTO` não podem ser especificadas.   
-   `ORDER BY` só pode ser especificado quando `TOP` também for especificado.   
-   Uma exibição criada usando uma subconsulta não pode ser atualizada.   
-   A lista de seleção de uma subconsulta introduzida com `EXISTS`, por convenção, tem um asterisco (\*), em vez de um único nome de coluna. As regras para uma subconsulta introduzida com `EXISTS` são iguais àquelas para uma lista de seleção padrão, porque uma subconsulta introduzida com `EXISTS` cria um teste de existência e retorna TRUE ou FALSE, em vez de dados.   

## <a name="qualifying"></a> Qualificando nomes de coluna em subconsultas
No exemplo a seguir, a coluna *CustomerID* na cláusula `WHERE` da consulta externa está implicitamente qualificada pelo nome da tabela na cláusula `FROM` da consulta externa (*Sales.Store*). A referência a *CustomerID* na lista de seleção da subconsulta está qualificada pela cláusula `FROM` da subconsulta, ou seja, pela tabela *Sales.Customer*.

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Sales.Store
WHERE BusinessEntityID NOT IN
    (SELECT CustomerID
     FROM Sales.Customer
     WHERE TerritoryID = 5);
GO
```

A regra geral é que os nomes de coluna em uma instrução sejam implicitamente qualificados pela tabela referenciada na cláusula `FROM` no mesmo nível. Se a coluna não existir na tabela referenciada na cláusula `FROM` de uma subconsulta, ela será qualificada implicitamente pela tabela referenciada na cláusula `FROM` da consulta externa.   

Eis como a consulta se parece com as suposições implícitas especificadas:

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Sales.Store
WHERE Sales.Store.BusinessEntityID NOT IN
    (SELECT Sales.Customer.CustomerID
     FROM Sales.Customer
     WHERE TerritoryID = 5);
GO
```

Nunca é errado declarar o nome de tabela explicitamente e sempre é possível substituir as suposições implícitas sobre nomes de tabela com qualificações explícitas.   

> [!IMPORTANT]
> Se uma coluna for referenciada em uma subconsulta que não existe na tabela referenciada da cláusula `FROM` da subconsulta, mas existir em uma tabela referenciada pela consulta externa `FROM` cláusula, a consulta será executada sem erro. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implicitamente qualifica a coluna na subconsulta com o nome da tabela na consulta externa.   

## <a name="nesting"></a> Vários níveis de aninhamento
Uma subconsulta pode incluir uma ou mais subconsultas. Qualquer número de subconsultas pode ser aninhado em uma instrução.   

A seguinte consulta localiza os nomes de funcionários que também são vendedores.   

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person
WHERE BusinessEntityID IN
    (SELECT BusinessEntityID
     FROM HumanResources.Employee
     WHERE BusinessEntityID IN
        (SELECT BusinessEntityID
         FROM Sales.SalesPerson)
    );
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LastName                                           FirstName
-------------------------------------------------- -----------------------
Jiang                                              Stephen
Abbas                                              Syed
Alberts                                            Amy
Ansman-Wolfe                                       Pamela
Campbell                                           David
Carson                                             Jillian
Ito                                                Shu
Mitchell                                           Linda
Reiter                                             Tsvi
Saraiva                                            Jos
Vargas                                             Garrett
Varkey Chudukatil                                  Ranjit
Valdez                                             Rachel
Tsoflias                                           Lynn
Pak                                                Jae
Blythe                                             Michael
Mensa-Annan                                        Tete

(17 row(s) affected)
```

A consulta mais interna retorna a ID dos vendedores. A consulta no nível superior próximo é avaliada com essa ID de vendedor e retorna os números de ID de contato dos funcionários. Finalmente, a consulta externa usa a ID de contato para localizar os nomes dos funcionários.   

Você também pode expressar esta consulta como uma junção:

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person c
INNER JOIN HumanResources.Employee e
ON c.BusinessEntityID = e.BusinessEntityID
JOIN Sales.SalesPerson s 
ON e.BusinessEntityID = s.BusinessEntityID;
GO
```

## <a name="correlated"></a> Subconsultas correlacionadas
Muitas consultas podem ser avaliadas pela execução de uma subconsulta, uma vez, e pela substituição do valor ou dos valores resultantes na cláusula `WHERE` da consulta externa. Em consultas que incluem uma subconsulta correlacionada (também conhecida como uma subconsulta repetitiva), a subconsulta depende da consulta externa para obter seus valores. Isso significa que a subconsulta é executada repetidamente, uma vez para cada linha que pode ser selecionada pela consulta externa.
Essa consulta recupera uma instância do nome e do sobrenome de cada funcionário para os quais os bônus da tabela *SalesPerson* sejam 5000, e para os quais existam números de identificação de funcionário correspondentes nas tabelas *Employee* e *SalesPerson*.

```sql
USE AdventureWorks2016;
GO
SELECT DISTINCT c.LastName, c.FirstName, e.BusinessEntityID 
FROM Person.Person AS c JOIN HumanResources.Employee AS e
ON e.BusinessEntityID = c.BusinessEntityID 
WHERE 5000.00 IN
    (SELECT Bonus
    FROM Sales.SalesPerson sp
    WHERE e.BusinessEntityID = sp.BusinessEntityID) ;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LastName FirstName BusinessEntityID
-------------------------- ---------- ------------
Ansman-Wolfe Pamela 280
Saraiva José 282

(2 row(s) affected)
```

A subconsulta anterior dessa instrução não pode ser avaliada independentemente da consulta externa. Precisa de um valor para *Employee.BusinessEntityID*, mas esse valor muda conforme [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] examina diferentes linhas em *Employee*.   
Essa é exatamente a forma pela qual a consulta é avaliada: o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera cada linha da tabela Employee para inclusão nos resultados, substituindo o valor de cada uma das linhas na consulta interna.
Por exemplo, se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] primeiro examinar a linha `Syed Abbas`, a variável *Employee.BusinessEntityID* usa o valor 285, que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] substitui na consulta interna.

```sql
USE AdventureWorks2016;
GO
SELECT Bonus
FROM Sales.SalesPerson
WHERE BusinessEntityID = 285;
GO
```

O resultado é 0 (`Syed Abbas` não recebeu bônus porque não é vendedor). Dessa forma, a consulta externa avalia:

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person AS c JOIN HumanResources.Employee AS e
ON e.BusinessEntityID = c.BusinessEntityID 
WHERE 5000 IN (0.00);
GO
```

Como isso é falso, a linha para `Syed Abbas` não será incluída nos resultados. Siga o mesmo procedimento com a linha para `Pamela Ansman-Wolfe`. Você observará que essa linha está incluída nos resultados.     

As subconsultas correlacionadas também podem incluir funções com valor de tabela na cláusula `FROM`, fazendo referência a colunas de uma tabela na consulta externa como argumento da função com valor de tabela. Nesse caso, para cada linha da consulta externa, a função com valor de tabela é avaliada segundo a subconsulta.    
  
## <a name="types"></a> Tipos de subconsulta
As subconsultas podem ser especificadas em muitos lugares: 
-   Com aliases. Para obter mais informações, veja [Subconsultas com aliases](#aliases).
-   Com `IN` ou `NOT IN`. Para obter mais informações, veja [Subconsultas com IN](#in) e [Subconsultas com NOT IN](#notin).
-   Nas instruções `UPDATE`, `DELETE` e `INSERT`. Para obter mais informações, veja [Subconsultas em instruções UPDATE, DELETE e INSERT](#upsert).
-   Com operadores de comparação. Para obter mais informações, veja [Subconsultas com operadores de comparação](#comparison).
-   Com `ANY`, `SOME` ou `ALL`. Para obter mais informações, veja [Operadores de comparação modificados por ANY, SOME ou ALL](#comparison_modified).
-   Com `EXISTS` ou `NOT EXISTS`. Para obter mais informações, veja [Subconsultas com EXISTS](#exists) e [Subconsultas com NOT EXISTS](#notexists).
-   No lugar de uma expressão. Para obter mais informações, veja [Subconsultas usadas no lugar de uma Expressão](#expression).

### <a name="aliases"></a> Subconsultas com aliases
Várias instruções nas quais a subconsulta e a consulta externa se referem à mesma tabela podem ser especificadas como autojunções (associando uma tabela a ela mesma). Por exemplo, você pode localizar endereços de funcionários de um estado específico usando uma subconsulta:   

```sql
USE AdventureWorks2016;
GO
SELECT StateProvinceID, AddressID
FROM Person.Address
WHERE AddressID IN
    (SELECT AddressID
     FROM Person.Address
     WHERE StateProvinceID = 39);
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
StateProvinceID AddressID
----------- -----------
39 942
39 955
39 972
39 22660

(4 row(s) affected)
```   

Ou você pode usar uma autojunção:   

```sql
USE AdventureWorks2016;
GO
SELECT e1.StateProvinceID, e1.AddressID
FROM Person.Address AS e1
INNER JOIN Person.Address AS e2
ON e1.AddressID = e2.AddressID
AND e2.StateProvinceID = 39;
GO
```

São necessários aliases de tabela porque a tabela que é unida a ela mesma aparece em duas diferentes funções. Os aliases também podem ser utilizados em consultas aninhadas que se referem à mesma tabela em uma consulta interna e externa.    

```sql
USE AdventureWorks2016;
GO
SELECT e1.StateProvinceID, e1.AddressID
FROM Person.Address AS e1
WHERE e1.AddressID IN
    (SELECT e2.AddressID
     FROM Person.Address AS e2
     WHERE e2.StateProvinceID = 39);
GO
```

Os aliases explícitos deixam claro que a referência a *Person.Address* na subconsulta não tem o mesmo significado que referência da consulta externa.   

### <a name="in"></a> Subconsultas com IN
O resultado de uma subconsulta apresentada com `IN` (ou com `NOT IN`) é uma lista com zero ou mais valores. Depois dos resultados da subconsulta retornarem, a consulta exterior os utiliza.    
A consulta a seguir encontra os nomes de todos os produtos de roda Adventure Works Cycles fabrica.     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]     

```
Name
----------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```

Esta instrução é avaliada em dois passos. Primeiro, a consulta interna retorna o número de identificação da subcategoria que corresponde ao nome 'Wheel' (Roda) (17). Depois, esse valor é substituído na consulta exterior a qual acha o nome do produto que vai com os números de identificação da subcategoria em Produto.     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN ('17');
GO
```

Uma diferença ao usar uma junção em vez de uma subconsulta para esse e outros problemas semelhantes é que a junção o deixa mostrar colunas de mais de uma tabela no resultado. Por exemplo, se você quiser incluir o nome da subcategoria do produto no resultado, deverá usar uma versão de junção.    

```sql
USE AdventureWorks2016;
GO
SELECT p.Name, s.Name
FROM Production.Product p
INNER JOIN Production.ProductSubcategory s
ON p.ProductSubcategoryID = s.ProductSubcategoryID
AND s.Name = 'Wheels';
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]    

```
Name
LL Mountain Front Wheel Wheels
ML Mountain Front Wheel Wheels
HL Mountain Front Wheel Wheels
LL Road Front Wheel Wheels
ML Road Front Wheel Wheels
HL Road Front Wheel Wheels
Touring Front Wheel Wheels
LL Mountain Rear Wheel Wheels
ML Mountain Rear Wheel Wheels
HL Mountain Rear Wheel Wheels
LL Road Rear Wheel Wheels
ML Road Rear Wheel Wheels
HL Road Rear Wheel Wheels
Touring Rear Wheel Wheels

(14 row(s) affected)
```    

A consulta a seguir encontra o nome de todos os fornecedores cuja avaliação de crédito é boa, os nomes daqueles dos quais a Adventure Works Cycles comprou no mínimo 20 itens e prazo de entrega médio é menor que 16 dias.    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Purchasing.Vendor
WHERE CreditRating = 1
AND BusinessEntityID IN
    (SELECT BusinessEntityID
     FROM Purchasing.ProductVendor
     WHERE MinOrderQty >= 20
     AND AverageLeadTime < 16);
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
Name
--------------------------------------------------
Compete Enterprises, Inc
International Trek Center
First National Sport Co.
Comfort Road Bicycles
Circuit Cycles
First Rate Bicycles
Jeff's Sporting Goods
Competition Bike Training Systems
Electronic Bike Repair & Supplies
Crowley Sport
Expert Bike Co
Team Athletic Co.
Compete, Inc.   

(13 row(s) affected)
```   

A consulta interna é avaliada, produzindo os números de ID dos fornecedores que atendam às qualificações da subconsulta. A consulta exterior é então avaliada. Observe que você pode incluir mais de uma condição na cláusula WHERE tanto da consulta interna quanto da exterior.   

Usando uma junção, a mesma consulta é expressada assim:

```sql
USE AdventureWorks2016;
GO
SELECT DISTINCT Name
FROM Purchasing.Vendor v
INNER JOIN Purchasing.ProductVendor p
ON v.BusinessEntityID = p.BusinessEntityID
WHERE CreditRating = 1
  AND MinOrderQty >= 20
  AND AverageLeadTime < 16;
GO
```

Uma junção sempre pode ser expressada como uma subconsulta. Uma subconsulta pode frequentemente, mas não sempre, ser expressada como uma junção. Isso se deve ao fato de as junções serem simétricas: você pode unir as tabelas A e B em qualquer ordem e obter a mesma resposta. O mesmo não será verdade se uma subconsulta for envolvida.    

### <a name="notin"></a> Subconsultas com NOT IN
Subconsultas introduzidas com a palavra-chave NOT IN também retornam uma lista com zero ou outros valores.   
A consulta a seguir encontra os nomes dos produtos que não são bicicletas acabadas.   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID NOT IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Mountain Bikes' 
        OR Name = 'Road Bikes'
        OR Name = 'Touring Bikes');
GO
```

Esta instrução não pode ser convertida em uma junção. A junção análoga não igual tem um significado diferente: acha os nomes de produtos que estão em alguma subcategoria que não é uma bicicleta acabada.      

### <a name="upsert"></a> Subconsultas nas instruções UPDATE, DELETE e INSERT
Subconsultas podem ser aninhadas nas instruções `UPDATE`, `DELETE`, `INSERT` e `SELECT `(DML) de manipulação de dados.    

O exemplo a seguir dobra o valor na coluna *ListPrice* na tabela *Production.Product*. A subconsulta na cláusula `WHERE` faz referência à tabela *Purchasing.ProductVendor* para restringir as linhas atualizadas na tabela *Product* somente àquelas fornecidas pela *BusinessEntity* 1540.

```sql
USE AdventureWorks2016;
GO 
UPDATE Production.Product
SET ListPrice = ListPrice * 2
WHERE ProductID IN
    (SELECT ProductID 
     FROM Purchasing.ProductVendor
     WHERE BusinessEntityID = 1540);
GO
```

Aqui está uma instrução `UPDATE` equivalente usando uma junção:

```sql
USE AdventureWorks2016;
GO 
UPDATE Production.Product
SET ListPrice = ListPrice * 2
FROM Production.Product AS p
INNER JOIN Purchasing.ProductVendor AS pv
    ON p.ProductID = pv.ProductID AND BusinessEntityID = 1540;
GO   
```

### <a name="comparison"></a> Subconsultas com operadores de comparação
Podem ser introduzidas subconsultas com um dos operadores de comparação (=, < >, >, > =, <, ! >, ! < ou < =).   

Uma subconsulta introduzida com um operador de comparação não modificado (um operador de comparação não seguido por `ANY` ou `ALL`) deve retornar um valor único, em vez de uma lista de valores, como subconsultas introduzidas com `IN`. Se uma subconsulta desse tipo retornar mais de um valor, o SQL Server exibirá uma mensagem de erro.    

Para usar uma subconsulta introduzida com um operador de comparação não modificado, você deve estar bastante familiarizado com seus dados e com a natureza do problema para saber que a subconsulta retornará exatamente um valor.     

Por exemplo, se você pressupor que cada vendedor cobre apenas um território de vendas e quiser encontrar os clientes localizados no território coberto por `Linda Mitchell`, poderá gravar uma instrução com uma subconsulta introduzida com o operador simple = comparison.    

```sql
USE AdventureWorks2016;
GO
SELECT CustomerID
FROM Sales.Customer
WHERE TerritoryID =
    (SELECT TerritoryID
     FROM Sales.SalesPerson
     WHERE BusinessEntityID = 276);
GO
```

No entanto, se `Linda Mitchell` cobrisse mais de um território de vendas, então uma mensagem de erro seria gerada. Em vez do operador de comparação =, poderia ser usada uma formulação `IN` (=ANY também funciona).    

Subconsultas introduzidas com operadores de comparação não modificados incluem frequentemente funções de agregação, porque elas retornam um único valor. Por exemplo, a instrução apresentada a seguir encontra os nomes de todos os produtos cujo preço da lista seja maior que o preço médio da lista.     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >
    (SELECT AVG (ListPrice)
     FROM Production.Product);
GO
```     

Uma vez que as subconsultas introduzidas com operadores de comparação não modificados devem retornar um único valor, elas não podem incluir cláusulas `GROUP BY` ou `HAVING`, a menos que você saiba que a própria cláusula GROUP BY ou HAVING retorna um valor único. Por exemplo, a consulta a seguir encontra os produtos cujo preço é mais alto que o produto de preço mais baixo que está na subcategoria 14.     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >
    (SELECT MIN (ListPrice)
     FROM Production.Product
     GROUP BY ProductSubcategoryID
     HAVING ProductSubcategoryID = 14);
GO
```

### <a name="comparison_modified"></a> Operadores de comparação modificados por ANY, SOME ou ALL
Os operadores de comparação que introduzem uma subconsulta podem ser modificados pelas palavras-chave ALL ou ANY. SOME é um padrão ISO equivalente para `ANY`.     

As subconsultas introduzidas por um operador de comparação modificado retornam uma lista com zero ou mais valores e podem incluir uma cláusula `GROUP BY` ou `HAVING`. Essas subconsultas podem ser declaradas novamente com `EXISTS`.     

Usando o operador de comparação > como um exemplo, `>ALL` significa maior do que todos os valores. Em outras palavras, significa maior do que o valor máximo. Por exemplo, `>ALL (1, 2, 3)` significa maior que 3. `>ANY` significa maior do que pelo menos um valor, isto é, maior do que o mínimo. Portanto, `>ANY (1, 2, 3)` significa maior do que 1.
Para uma linha em uma subconsulta com `>ALL` satisfazer a condição especificada na consulta externa, o valor na coluna que introduz a subconsulta deve ser maior do que cada valor na lista de valores retornada pela subconsulta.    

De modo semelhante, `>ANY` significa que, para uma linha satisfazer a condição especificada na consulta exterior, o valor na coluna que introduz a subconsulta deve ser maior do que pelo menos um dos valores na lista de valores retornada pela subconsulta.    

A consulta a seguir fornece um exemplo de uma subconsulta introduzido com um operador de comparação modificado por ANY. Encontra os produtos cujos preços de tabela são maiores ou iguais ao preço máximo de tabela de qualquer subcategoria de produto.    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >= ANY
    (SELECT MAX (ListPrice)
     FROM Production.Product
     GROUP BY ProductSubcategoryID);
GO
```    

Para cada subcategoria de produto, a consulta interna encontra o preço máximo de tabela. A consulta exterior procura todos esses valores e determina quais os preços de tabela do produto individual são maiores ou iguais ao preço máximo de tabela de qualquer subcategoria de produto. Se `ANY` for alterado para `ALL`, a consulta retornará apenas aqueles produtos cujo preço de tabela é maior ou igual a todos os preços de tabela retornados na consulta interna.    

Se a subconsulta não retornar nenhum valor, a consulta inteira não retorna qualquer valor.    

O operador `=ANY` é equivalente a `IN`. Por exemplo, para localizar os nomes de todos os produtos de roda que a Adventure Works Cycles fabrica, você pode usar o `IN` ou `=ANY`.

```sql
--Using =ANY
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID =ANY
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO

--Using IN
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```

Aqui está o conjunto de resultados para ambas as consultas:

```
Name
--------------------------------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```    

O operador `<>ANY`, entretanto difere de `NOT IN`: `<>ANY` significa não = a ou não = b ou não = c. `NOT IN` significa não = a e não = b e não = c. `<>ALL` significa o mesmo que `NOT IN`.     

Por exemplo, a consulta a seguir encontra os clientes localizados em um território não coberto por qualquer vendedor.     

```sql
USE AdventureWorks2016;
GO
SELECT CustomerID
FROM Sales.Customer
WHERE TerritoryID <> ANY
    (SELECT TerritoryID
     FROM Sales.SalesPerson);
GO
```    

Os resultados incluem todos os clientes, exceto aqueles cujos territórios de vendas são NULL, porque todo território atribuído a um cliente está coberto por um vendedor. A consulta interna encontra todos os territórios de vendas cobertos por vendedores e então, para cada território, a consulta externa encontra os clientes que não estão em um.    

Pela mesma razão, quando você usa `NOT IN` nessa consulta, os resultados não incluem nenhum dos clientes.      

Você pode obter os mesmos resultados com o operador `<>ALL`, que é equivalente a `NOT IN`.   

### <a name="exists"></a> Subconsultas com EXISTS
Quando uma subconsulta é apresentada com a palavra-chave `EXISTS`, a subconsulta funciona como um teste de existência. A cláusula `WHERE` da consulta externa testa se as linhas retornadas pela subconsulta existem. A subconsulta não produz de fato nenhum dado; ela retorna um valor TRUE ou FALSE.   

Uma subconsulta introduzida com EXISTS tem a seguinte sintaxe:   

`WHERE [NOT] EXISTS (subquery)`    

A consulta a seguir encontra os nomes de todos os produtos que estão na subcategoria Rodas:    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE EXISTS
    (SELECT * 
     FROM Production.ProductSubcategory
     WHERE ProductSubcategoryID = 
            Production.Product.ProductSubcategoryID
        AND Name = 'Wheels');
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]    

```
Name
--------------------------------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```    

Para entender os resultados desta consulta, considere o nome de cada produto individualmente. Esse valor faz a subconsulta retornar pelo menos uma linha? Em outras palavras, a consulta faz com que o teste de existência seja avaliado como TRUE?   

Observe que subconsultas apresentadas com EXISTS são um pouco diferentes de outras subconsultas da seguinte forma: 
-   A palavra-chave `EXISTS` não é precedida por um nome de coluna, constante nem outra expressão.     
-   A lista de seleção de uma subconsulta introduzida por `EXISTS` quase sempre consiste em um asterisco (*). Não há nenhuma razão para listar nomes de coluna, pois você está apenas testando se existem linhas que atendem às condições especificadas na subconsulta.    

A palavra-chave `EXISTS` é importante porque geralmente não há formulação alternativa sem subconsultas. Embora algumas consultas que são criadas com EXISTS não possam ser expressadas de nenhum outro modo, muitas consultas podem usar IN ou um operador de comparação modificado por `ANY` ou `ALL` para alcançar resultados semelhantes.     

Por exemplo, a consulta precedente pode ser expressa usando IN:   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```   

### <a name="notexists"></a> Subconsultas com NOT EXISTS
`NOT EXISTS` funciona como `EXISTS`, exceto pela cláusula `WHERE`, em que é usado se nenhuma linha for retornada pela subconsulta.    

Por exemplo, para localizar os nomes de produtos que não estão na subcategoria rodas:   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE NOT EXISTS
    (SELECT * 
     FROM Production.ProductSubcategory
     WHERE ProductSubcategoryID = 
            Production.Product.ProductSubcategoryID
        AND Name = 'Wheels');
GO
```   

### <a name="expression"></a> Subconsultas usadas em vez de uma expressão
Em [!INCLUDE[tsql](../../includes/tsql-md.md)], uma subconsulta pode ser substituída em qualquer lugar em que uma expressão pode ser usada em instruções `SELECT`, `UPDATE`, `INSERT` e `DELETE`, exceto em uma lista `ORDER BY`.    

O exemplo a seguir ilustra como você poderia usar esse aprimoramento. Esta consulta encontra os preços de todos os produtos de mountain bike, o preço médio delas e a diferença entre o preço de cada bicicleta mountain bike e o preço médio.    

```sql
USE AdventureWorks2016;
GO
SELECT Name, ListPrice, 
(SELECT AVG(ListPrice) FROM Production.Product) AS Average, 
    ListPrice - (SELECT AVG(ListPrice) FROM Production.Product)
    AS Difference
FROM Production.Product
WHERE ProductSubcategoryID = 1;
GO
```   

## <a name="see-also"></a>Consulte Também  
[IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)       
[EXISTS &#40;Transact-SQL&#41;](../../t-sql/language-elements/exists-transact-sql.md)     
[ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)     
[SOME | ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)     
[Junções](../../relational-databases/performance/joins.md)    
[Operadores de comparação &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)       
  
