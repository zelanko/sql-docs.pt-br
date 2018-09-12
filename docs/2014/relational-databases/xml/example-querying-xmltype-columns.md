---
title: 'Exemplo: consultando colunas de tipo XML | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, querying XML example
ms.assetid: d9f3710d-7a2e-4abe-9c02-3e3c0df4d620
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8ed094b0f98514bcc6c50baf07de75b59161d911
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888462"
---
# <a name="example-querying-xmltype-columns"></a>Exemplo: Consultando colunas de tipo XML
  A consulta a seguir inclui colunas de `xml` tipo. A consulta recupera a ID, nome e etapas de fabricação do modelo do produto no primeiro local da coluna `Instructions` de tipo `xml`.  
  
## <a name="example"></a>Exemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name,  
   Instructions.query('  
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
   /MI:root/MI:Location[1]/MI:step  
')   
FROM Production.ProductModel  
FOR XML RAW ('ProductModelData')  
GO  
```  
  
 O seguinte é o resultado. Observe que a tabela armazena instruções de fabricação para apenas alguns modelos do produto. As etapas de fabricação são retornadas como subelementos do elemento <`ProductModelData`> no resultado.  
  
```  
<ProductModelData ProductModelID="5" Name="HL Mountain Frame" />  
<ProductModelData ProductModelID="6" Name="HL Road Frame" />  
<ProductModelData ProductModelID="7" Name="HL Touring Frame">  
    <MI:step> ... </MI:step>  
    <MI:step> ... </MI:step>  
 </ProductModelData>  
```  
  
 Se a consulta especificar um nome de coluna para o XML retornado pelo XQuery, conforme especificado na instrução `SELECT` a seguir, as etapas de fabricação serão encapsuladas no elemento que tem o nome especificado.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name,  
   Instructions.query('  
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
   /MI:root/MI:Location[1]/MI:step  
') as ManuSteps  
FROM Production.ProductModel  
FOR XML RAW ('ProductModelData')  
go  
```  
  
 Este é o resultado:  
  
```  
<ProductModelData ProductModelID="5" Name="HL Mountain Frame" />  
<ProductModelData ProductModelID="6" Name="HL Road Frame" />  
<ProductModelData ProductModelID="7" Name="HL Touring Frame">  
  <ManuSteps>  
    <MI:step ... </MI:step>  
    <MI:step ... </MI:step>  
  </ManuSteps>  
</ProductModelData>  
```  
  
 A consulta a seguir especifica a política `ELEMENTS` . Portanto o resultado retornado é centrado em elemento. A opção `XSINIL` especificada com a política `ELEMENTS` retorna os elementos <`ManuSteps`>, mesmo que a colunas correspondentes no conjunto de linhas sejam NULL.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name,  
   Instructions.query('  
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
   /MI:root/MI:Location[1]/MI:step  
') as ManuSteps  
FROM Production.ProductModel  
FOR XML RAW ('ProductModelData'), root('MyRoot'), ELEMENTS XSINIL  
go  
```  
  
 Este é o resultado:  
  
```  
<MyRoot xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   ...  
  <ProductModelData>  
    <ProductModelID>6</ProductModelID>  
    <Name>HL Road Frame</Name>  
    <ManuSteps xsi:nil="true" />  
  </ProductModelData>  
  <ProductModelData>  
    <ProductModelID>7</ProductModelID>  
    <Name>HL Touring Frame</Name>  
    <ManuSteps>  
      <MI:step ... </MI:step>  
      <MI:step ...</MI:step>  
       ...  
    </ManuSteps>  
  </ProductModelData>  
</MyRoot>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar modo RAW com FOR XML](use-raw-mode-with-for-xml.md)  
  
  
