---
title: 'Exemplo: Renomeando o elemento &lt;row&gt; | Microsoft Docs'
description: Veja um exemplo de renomeação de um elemento de linha XML especificando um argumento opcional para o modo RAW na cláusula FOR XML.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc297571daec9825a91d4e35ebbac737d88b5619
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633048"
---
# <a name="example-renaming-the-ltrowgt-element"></a>Exemplo: Renomeando o elemento &lt;row&gt;
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Para cada linha no conjunto de resultados, o modo RAW gera um elemento `<row>`. Opcionalmente, é possível especificar outro nome para esse elemento especificando um argumento opcional para o modo RAW, conforme mostrado nesta consulta. A consulta retorna um elemento <`ProductModel`> para cada linha do conjunto de dados.  
  
## <a name="example"></a>Exemplo  
  
```  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122  
FOR XML RAW ('ProductModel'), ELEMENTS  
GO  
```  
  
 Este é o resultado. Como a diretiva `ELEMENTS` é adicionada à consulta, o resultado é centrado em elemento.  
  
```  
<ProductModel>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</ProductModel>   
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
