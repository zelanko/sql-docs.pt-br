---
title: Usar o modo AUTO com FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, AUTO mode
- ELEMENTS option
- FOR XML AUTO mode
- AUTO FOR XML mode
ms.assetid: 7140d656-1d42-4f01-a533-5251429f4450
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1c1a278a1d712b464fba279112c1652d676f2542
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690744"
---
# <a name="use-auto-mode-with-for-xml"></a>Usar o modo AUTO com FOR XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Conforme descrito em [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md), o modo AUTO retorna os resultados da consulta como elementos XML aninhados. Isso não fornece muito controle sobre a forma do XML gerado em um resultado de consulta. As consultas em modo AUTO são úteis para gerar hierarquias simples. No entanto, [Usar o modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md) e [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md) fornecem mais controle e flexibilidade para decidir a forma do XML em um resultado de consulta.  
  
 Cada tabela na cláusula FROM, na qual pelo menos uma coluna esteja listada na cláusula SELECT, é representada como um elemento XML. As colunas listadas na cláusula SELECT serão mapeadas para atributos ou subelementos, se a opção ELEMENTS opcional estiver especificada na cláusula FOR XML.  
  
 A hierarquia XML, o aninhamento dos elementos, no XML resultante é baseada na ordem das tabelas identificada pelas colunas especificadas na cláusula SELECT. Portanto a ordem na qual os nomes das colunas são especificados na cláusula SELECT é significativa. A primeira tabela da estrema esquerda identificada forma o elemento superior no documento XML resultante. A segunda tabela da extremidade esquerda, identificada pelas colunas na instrução SELECT, forma um subelemento dentro do elemento superior e assim por diante.  
  
 Se um nome de coluna listado na cláusula SELECT for de uma tabela que já está identificada por uma coluna especificada anteriormente na cláusula SELECT, a coluna será adicionada como um atributo do elemento já criado, em vez de abrir um novo nível de hierarquia. Se a opção ELEMENTS estiver especificada, a coluna será adicionada como um atributo.  
  
 Por exemplo, execute esta consulta:  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO  
```  
  
 Este é o resultado parcial:  
  
```  
<Cust CustomerID="1" CustomerType="S">  
  <OrderHeader CustomerID="1" SalesOrderID="43860" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="44501" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="45283" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="46042" Status="5" />  
</Cust>  
...  
```  
  
 Observe o seguinte na cláusula SELECT:  
  
-   CustomerID faz referência à tabela Cust. Portanto um elemento <`Cust`> é criado e CustomerID é adicionado como seu atributo.  
  
-   Em seguida, três colunas, OrderHeader.CustomerID, OrderHeader.SaleOrderID e OrderHeader.Status, fazem referência à tabela OrderHeader. Portanto um elemento <`OrderHeader`> é adicionado como um subelemento do elemento <`Cust`> e as três colunas são adicionadas como atributos de <`OrderHeader`>.  
  
-   Em seguida, a coluna Cust.CustomerType faz referência novamente à tabela Cust que já foi identificada pela coluna Cust.CustomerID. Portanto  nenhum elemento novo é criado. Em vez disso, o atributo CustomerType é adicionado ao elemento <`Cust`> que foi criado anteriormente.  
  
-   A consulta especifica alias para os nomes das tabelas. Esses alias aparecem como nomes de elementos correspondentes.  
  
-   ORDER BY é necessário para agrupar todos os filhos sob um pai.  
  
 Esta consulta é semelhante a anterior, exceto que a cláusula SELECT especifica colunas na tabela OrderHeader antes das colunas na tabela Cust. Portanto o primeiro elemento <`OrderHeader`> é criado e, em seguida, o elemento filho <`Cust`> é adicionado a ele.  
  
```  
select OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerID,   
       Cust.CustomerType  
from Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
where Cust.CustomerID = OrderHeader.CustomerID  
for xml auto  
```  
  
 Este é o resultado parcial:  
  
```  
<OrderHeader CustomerID="1" SalesOrderID="43860" Status="5">  
  <Cust CustomerID="1" CustomerType="S" />  
</OrderHeader>  
...  
```  
  
 Se a opção ELEMENTS for adicionada à cláusula FOR XML, XML centrado em elemento será retornado.  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO, ELEMENTS  
```  
  
 Este é o resultado parcial:  
  
```  
<Cust>  
  <CustomerID>1</CustomerID>  
  <CustomerType>S</CustomerType>  
  <OrderHeader>  
    <CustomerID>1</CustomerID>  
    <SalesOrderID>43860</SalesOrderID>  
    <Status>5</Status>  
  </OrderHeader>  
   ...  
</Cust>  
...  
```  
  
 Nessa consulta, os valores de CustomerID são comparados de uma linha à seguinte, para criar os elementos \<Cust>, pois CustomerID é a chave primária da tabela. Se CustomerID não for identificado como a chave primária da tabela, todos os valores das colunas (CustomerID e CustomerType nessa consulta) serão comparados de uma linha para a seguinte; Se os valores forem diferentes, um novo elemento \<Cust> será adicionado ao XML.  
  
 Ao comparar esses valores de colunas, se qualquer uma das colunas a serem comparadas for do tipo **text**, **ntext**, **image**ou **xml**, FOR XML assumirá que os valores são diferentes e não comparados, embora possam parecer os mesmos. Isso é porque a comparação de objetos grandes não tem suporte. Os elementos são adicionados ao resultado de cada linha selecionada. Observe que as colunas **(n)varchar(max)** e **varbinary(max)** são comparadas.  
  
 Quando uma coluna na cláusula SELECT não puder ser associada a qualquer uma das tabelas identificadas na cláusula FROM, como no caso de uma coluna de agregação ou computada, a coluna será adicionada ao documento XML no nível de aninhamento mais profundo em vigor quando ela for encontrada na lista. Se ela aparecer como a primeira coluna na cláusula SELECT, a coluna será adicionada ao elemento superior.  
  
 Se o caractere curinga asterisco (*) for especificado na cláusula SELECT, o aninhamento será determinado da mesma maneira como descrito anteriormente, com base na ordem em que as linhas são retornadas pelo mecanismo de consulta.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os seguintes tópicos fornecem mais informações sobre o modo AUTO:  
  
-   [Usar a opção BINARY BASE64](../../relational-databases/xml/use-the-binary-base64-option.md)  
  
-   [Heurística de modo AUTO na formação do XML retornado](../../relational-databases/xml/auto-mode-heuristics-in-shaping-returned-xml.md)  
  
-   [Exemplos: Usando modo AUTO](../../relational-databases/xml/examples-using-auto-mode.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
