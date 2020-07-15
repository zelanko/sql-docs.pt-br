---
title: 'Exemplo: especificando a diretiva HIDE | Microsoft Docs'
description: Veja um exemplo de como usar a diretiva HIDE em uma consulta SQL.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- HIDE directive
ms.assetid: 87504d87-1cbd-412a-9041-47884b6efcec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f8f8f5a8eeeff444832d5cd6142f1bb0099c5913
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632500"
---
# <a name="example-specifying-the-hide-directive"></a>Exemplo: especificando a diretiva HIDE
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Este exemplo ilustra o uso da diretiva **HIDE** . Essa diretiva é útil quando você deseja que a consulta retorne um atributo para ordenar as linhas na tabela universal retornada pela consulta, mas não deseja esse atributo no documento XML resultante final.  
  
 Esta consulta constrói este XML:  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
           <Summary> element from XML stored in CatalogDescription column  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 Essa consulta gera o XML desejado. A consulta identifica dois grupos de colunas que têm 1 e 2 como valores de Marca nos nomes das colunas.  
  
 Essa consulta usa o [Método query() (tipo de dados xml)](../../t-sql/xml/query-method-xml-data-type.md) do tipo de dados **xml** para consultar a coluna CatalogDescription de tipo **xml** para recuperar a descrição resumida. A consulta também usa o [Método value() (tipo de dados xml)](../../t-sql/xml/value-method-xml-data-type.md) do tipo de dados **xml** para recuperar o valor de ProductModelID da coluna CatalogDescription. Esse valor não é necessário no XML resultante, mas é necessário ordenar o conjunto de linhas resultante. Portanto o nome da coluna `[Summary!2!ProductModelID!HIDE]`inclui a diretiva **HIDE** . Se essa coluna não estiver incluída na instrução SELECT, você precisará ordenar o conjunto de linhas por `[ProductModel!1!ProdModelID]` e `[Summary!2!SummaryDescription]` que é de tipo **xml** e usar a coluna de tipo **xml** em ORDER BY. Portanto a coluna `[Summary!2!ProductModelID!HIDE]` adicional é adicionada e especificada na cláusula ORDER BY.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID     as [ProductModel!1!ProdModelID],  
        Name               as [ProductModel!1!Name],  
        NULL               as [Summary!2!ProductModelID!hide],  
        NULL               as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
        CatalogDescription.value('  
         declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       (/PD:ProductDescription/@ProductModelID)[1]', 'int'),  
        CatalogDescription.query('  
         declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /pd:ProductDescription/pd:Summary')  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],[Summary!2!ProductModelID!hide]  
FOR XML EXPLICIT  
go  
```  
  
 Este é o resultado:  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription" xmlns="">  
        <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike. Performance-enhancing options include the innovative HL Frame, super-smooth front suspension, and traction for all terrain. </p1:p>  
      </pd:Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
