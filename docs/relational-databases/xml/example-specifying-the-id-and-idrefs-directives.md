---
title: 'Exemplo: Especificando as diretivas ID e IDREFS | Microsoft Docs'
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- IDREFS directive
- ID directive
ms.assetid: 99b9f0d8-ecbb-4225-859f-881066c09785
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1574f3336ae06b8bfb368de7eff37d1bc4286af0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006690"
---
# <a name="example-specifying-the-id-and-idrefs-directives"></a>Exemplo: Especificando as diretivas ID e IDREFS

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Um atributo de elemento pode ser especificado como um atributo de tipo **ID** , e o atributo **IDREFS** pode ser usado para se referir a ele. Isso habilita vínculos intradocumento e é semelhante às relações de chave primária e de chave estrangeira em bancos de dados relacionais.  
  
 Este exemplo ilustra como as diretivas **ID** e **IDREFS** podem ser usadas para criar atributos de tipos **ID** e **IDREFS** . Como os IDs não podem ser valores inteiros, os valores de ID neste exemplo são convertidos. Em outras palavras, seus tipos são convertidos. Prefixos são usados para os valores de ID.  
  
 Assuma que você deseja construir XML, conforme mostrado no exemplo a seguir:  
  
```xml
<Customer CustomerID="C1" SalesOrderIDList=" O11 O22 O33..." >
    <SalesOrder SalesOrderID="O11" OrderDate="..." />  
    <SalesOrder SalesOrderID="O22" OrderDate="..." />  
    <SalesOrder SalesOrderID="O33" OrderDate="..." />  
    ...  
</Customer>  
```  
  
O atributo `SalesOrderIDList` do elemento `<Customer>` é um atributo com vários valores que se refere ao atributo `SalesOrderID` do elemento `<SalesOrder>`. Para estabelecer esse vínculo, o atributo `SalesOrderID` precisa ser declarado como sendo do tipo `ID` e o atributo `SalesOrderIDList` do elemento `<Customer>` precisa ser declarado como sendo do tipo `IDREFS`. Como um cliente pode solicitar vários pedidos, o tipo `IDREFS` é usado.
  
 Os elementos do tipo **IDREFS** também têm mais de um valor. Portanto você precisa usar uma cláusula select separada que reutilizará as mesmas informações de marca, pai e coluna de chave. O `ORDER BY` precisa garantir que a sequência de linhas que constituem os valores **IDREFS** são exibidas agrupadas sob seu elemento pai.  
  
 Esta é a consulta que produz o XML desejado. A consulta usa as diretivas `ID` e `IDREFS` para substituir os tipos nos nomes das colunas (`SalesOrder!2!SalesOrderID!ID`, `Customer!1!SalesOrderIDList!IDREFS`).  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID   [Customer!1!CustomerID],  
        NULL           [Customer!1!SalesOrderIDList!IDREFS],
        NULL           [SalesOrder!2!SalesOrderID!ID],  
        NULL           [SalesOrder!2!OrderDate]  
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
    ON  C.CustomerID = SOH.CustomerID
ORDER BY [Customer!1!CustomerID] ,
         [SalesOrder!2!SalesOrderID!ID],  
         [Customer!1!SalesOrderIDList!IDREFS]  
FOR XML EXPLICIT;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
