---
title: 'Exemplo: especificando as diretivas ID e IDREFS | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IDREFS directive
- ID directive
ms.assetid: 99b9f0d8-ecbb-4225-859f-881066c09785
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c567b0e66efc4d93789beb7d15ccda06ddb5eea5
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="example-specifying-the-id-and-idrefs-directives"></a>Exemplo: Especificando as diretivas ID e IDREFS
  Um atributo de elemento pode ser especificado como um atributo de tipo **ID** , e o atributo **IDREFS** pode ser usado para se referir a ele. Isso habilita vínculos intradocumento e é semelhante às relações de chave primária e de chave estrangeira em bancos de dados relacionais.  
  
 Este exemplo ilustra como as diretivas **ID** e **IDREFS** podem ser usadas para criar atributos de tipos **ID** e **IDREFS** . Como os IDs não podem ser valores inteiros, os valores de ID neste exemplo são convertidos. Em outras palavras, seus tipos são convertidos. Prefixos são usados para os valores de ID.  
  
 Assuma que você deseja construir XML, conforme mostrado no exemplo a seguir:  
  
```  
<Customer CustomerID="C1" SalesOrderIDList=" O11 O22 O33..." >  
    <SalesOrder SalesOrderID="O11" OrderDate="..." />  
    <SalesOrder SalesOrderID="O22" OrderDate="..." />  
    <SalesOrder SalesOrderID="O33" OrderDate="..." />  
    ...  
</Customer>  
```  
  
 O atributo `SalesOrderIDList` do elemento < `Customer` > é um atributo com vários valores que se refere ao atributo `SalesOrderID` do elemento < `SalesOrder` >. Para estabelecer esse link, o atributo `SalesOrderID` deve ser declarado como sendo do tipo `ID` e o atributo `SalesOrderIDList` do elemento < `Customer`> deve ser declarado como sendo do tipo `IDREFS`. Como um cliente pode solicitar vários pedidos, o tipo `IDREFS` é usado.  
  
 Os elementos do tipo **IDREFS** também têm mais de um valor. Portanto você precisa usar uma cláusula select separada que reutilizará as mesmas informações de marca, pai e coluna de chave. O `ORDER BY` precisa garantir que a sequência de linhas que constituem os valores **IDREFS** são exibidas agrupadas sob seu elemento pai.  
  
 Esta é a consulta que produz o XML desejado. A consulta usa as diretivas `ID` e `IDREFS` para substituir os tipos nos nomes das colunas (`SalesOrder!2!SalesOrderID!ID`, `Customer!1!SalesOrderIDList!IDREFS`).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID       [Customer!1!CustomerID],  
        NULL               [Customer!1!SalesOrderIDList!IDREFS],  
        NULL               [SalesOrder!2!SalesOrderID!ID],  
        NULL               [SalesOrder!2!OrderDate]  
FROM   Sales.Customer C   
UNION ALL   
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID,  
        'O-'+CAST(SalesOrderID as varchar(10)),   
        NULL,  
        NULL  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
        C.CustomerID,  
        NULL,  
        'O-'+CAST(SalesOrderID as varchar(10)),  
        OrderDate  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerIDORDER BY [Customer!1!CustomerID] ,  
         [SalesOrder!2!SalesOrderID!ID],  
         [Customer!1!SalesOrderIDList!IDREFS]  
FOR XML EXPLICIT;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
