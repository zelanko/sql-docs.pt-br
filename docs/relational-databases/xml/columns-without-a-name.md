---
title: Colunas sem nome | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f7990de0a0fb9dec2ee969ecdfe183a4e565777c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675305"
---
# <a name="columns-without-a-name"></a>Colunas sem um nome
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Qualquer coluna sem um nome será embutida. Por exemplo, colunas computadas ou consultas escalares aninhadas que não especificam o alias de coluna gerarão colunas sem nome. Se a coluna for de tipo **xml** , o conteúdo dessa instância de tipo de dados será inserido. Caso contrário, o conteúdo da coluna será inserido como um nó de texto.  
  
```  
SELECT 2+2  
FOR XML PATH  
```  
  
 Produza este XML. Por padrão, para cada linha no conjunto de linhas, um elemento <`row`> é gerado no XML resultante. Isso é o mesmo que o modo RAW.  
  
 `<row>4</row>`  
  
 A consulta a seguir retorna um conjunto de linhas de três colunas. A terceira coluna sem um nome tem dados XML. O modo PATH insere uma instância de tipo xml.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ;  
GO  
```  
  
 Este é o resultado parcial:  
  
```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location ...LocationID="10" ...></MI:Location>
  <MI:Location ...LocationID="20" ...></MI:Location>
  ...
</row>
```

## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
