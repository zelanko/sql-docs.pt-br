---
title: Colunas sem nome | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
author: rothja
ms.author: jroth
ms.openlocfilehash: c295a0795e8c073ae55fcb61457782496a91526f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046939"
---
# <a name="columns-without-a-name"></a>Colunas sem um nome
  Qualquer coluna sem um nome será embutida. Por exemplo, colunas computadas ou consultas escalares aninhadas que não especificam o alias de coluna gerarão colunas sem nome. Se a coluna for de tipo `xml`, o conteúdo dessa instância de tipo de dados será inserido. Caso contrário, o conteúdo da coluna será inserido como um nó de texto.  
  
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
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location ...LocationID="10" ...></MI:Location>`  
  
 `<MI:Location ...LocationID="20" ...></MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](use-path-mode-with-for-xml.md)  
  
  
