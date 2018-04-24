---
title: Gerar irmãos com uma consulta aninhada em modo AUTO | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- queries [XML in SQL Server], nested AUTO mode
- nested AUTO mode query
ms.assetid: 748d9899-589d-4420-8048-1258e9e67c20
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b03f2b00ab34c9afa56738611dad4e760fc3c92
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="generate-siblings-with-a-nested-auto-mode-query"></a>Gerar irmãos com uma consulta aninhada em modo AUTO
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  O exemplo a seguir mostra como gerar irmãos usando uma consulta aninhada em modo AUTO. A única outra maneira de gerar esse tipo de XML é usar o modo EXPLICIT. No entanto isso pode ser trabalhoso.  
  
## <a name="example"></a>Exemplo  
 Esta consulta constrói XML que fornece informações de pedidos de vendas. Isso inclui o seguinte:  
  
-   Informações de cabeçalho de ordem de venda, `SalesOrderID`, `SalesPersonID`e `OrderDate`. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] armazena essas informações na tabela `SalesOrderHeader` .  
  
-   Informações sobre detalhes de pedidos de vendas. Isso inclui um ou mais produtos pedidos, o preço unitário e a quantidade pedida. Essas informações são armazenadas na tabela `SalesOrderDetail` .  
  
-   Informações sobre o vendedor. Esse é o vendedor que obteve o pedido. A tabela `SalesPerson` fornece o `SalesPersonID`. Para essa consulta, você precisa unir essa tabela com a tabela `Employee` para localizar o nome do vendedor.  
  
 As duas consultas `SELECT` distintas a seguir geram XML com uma pequena diferença na forma.  
  
 A primeira consulta gera XML no qual <`SalesPerson`> e <`SalesOrderHeader`> aparecem como filhos irmãos de <`SalesOrder`>:  
  
```  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID =   
                   SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
        FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
        for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As   
                     SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
```  
  
 Na consulta anterior, a instrução `SELECT` mais externa faz o seguinte:  
  
-   Consulta o conjunto de linhas, `SalesOrder`, especificado na cláusula `FROM`. O resultado é um XML com um ou mais elementos <`SalesOrder`>.  
  
-   Especifica o modo `AUTO` e a diretiva `TYPE` . `AUTO` O modo transforma o resultado da consulta em XML e a diretiva `TYPE` retorna o resultado como tipo **xml** .  
  
-   Inclui duas instruções `SELECT` aninhadas separadas por uma vírgula. O primeiro `SELECT` aninhado recupera informações sobre pedidos de vendas, cabeçalho e detalhes, e o segundo `SELECT` aninhado recupera informações sobre o vendedor.  
  
    -   A própria instrução `SELECT` que recupera `SalesOrderID`, `SalesPersonID`e `CustomerID` inclui outra instrução `SELECT ... FOR XML` aninhada (com modo `AUTO` e diretiva `TYPE` ) que retorna informações sobre detalhes do pedido de vendas.  
  
 A instrução `SELECT` que recupera as informações do vendedor consulta um conjunto de linhas, `SalesPerson`, criado na cláusula `FROM` . Para que as consultas `FOR XML` funcionem, você deve fornecer um nome para o conjunto de linhas anônimo gerado na cláusula `FROM` . Nesse caso, o nome fornecido é `SalesPerson`.  
  
 Este é o resultado parcial:  
  
```  
<SalesOrder>  
  <Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  </Sales.SalesOrderHeader>  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</SalesOrder>  
...  
```  
  
 A consulta a seguir gera as mesmas informações sobre pedidos de vendas, exceto que no XML resultante, o <`SalesPerson`> aparece como irmão de <`SalesOrderDetail`>:  
  
```  
<SalesOrder>  
    <SalesOrderHeader ...>  
          <SalesOrderDetail .../>  
          <SalesOrderDetail .../>  
          ...  
          <SalesPerson .../>  
    </SalesOrderHeader>  
  
</SalesOrder>  
<SalesOrder>  
  ...  
</SalesOrder>  
```  
  
 Esta é a consulta:  
  
```  
SELECT SalesOrderID, SalesPersonID, CustomerID,  
             (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
              from Sales.SalesOrderDetail  
              WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
              FOR XML AUTO, TYPE),  
              (SELECT *   
               FROM  (SELECT SalesPersonID, EmployeeID  
                    FROM Sales.SalesPerson, HumanResources.Employee  
                    WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
               WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
         FOR XML AUTO, TYPE)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID=43659 or SalesOrderID=43660  
FOR XML AUTO, TYPE  
```  
  
 Este é o resultado:  
  
```  
<Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
<Sales.SalesOrderHeader SalesOrderID="43660" SalesPersonID="279" CustomerID="117">  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="762" OrderQty="1" UnitPrice="419.4589" />  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="758" OrderQty="1" UnitPrice="874.7940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
```  
  
 Como a diretiva `TYPE` retorna um resultado de consulta como o tipo **xml** , é possível consultar o XML resultante usando vários métodos do tipo de dados **xml** . Para obter mais informações, veja [Métodos do tipo de dados xml](../../t-sql/xml/xml-data-type-methods.md). Na consulta a seguir, observe o seguinte:  
  
-   A consulta anterior é adicionada na cláusula `FROM` . O resultado da consulta é retornado como uma tabela. Observe o alias de `XmlCol` que é adicionado.  
  
-   A cláusula `SELECT` especifica um XQuery em relação à `XmlCol` retornada na cláusula `FROM` . O método **query()** do tipo de dados **xml** é usado para especificar o XQuery. Para obter mais informações, veja [Método query&#40;&#41; &#40;tipo de dados xml&#41;](../../t-sql/xml/query-method-xml-data-type.md).  
  
    ```  
    SELECT XmlCol.query('<Root> { /* } </Root>')  
    FROM (  
    SELECT SalesOrderID, SalesPersonID, CustomerID,  
                 (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
                  from Sales.SalesOrderDetail  
                  WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
                  FOR XML AUTO, TYPE),  
                  (SELECT *   
                   FROM  (SELECT SalesPersonID, EmployeeID  
                        FROM Sales.SalesPerson, HumanResources.Employee  
                        WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
                   WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
             FOR XML AUTO, TYPE)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesOrderID='43659' or SalesOrderID='43660'  
    FOR XML AUTO, TYPE ) as T(XmlCol)  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar consultas FOR XML aninhadas](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
