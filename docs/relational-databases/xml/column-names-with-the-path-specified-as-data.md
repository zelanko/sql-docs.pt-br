---
title: Nomes de coluna com o caminho especificado como data() | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77913ea6358f9a5d1b88de7426144b730b5c74e9
ms.sourcegitcommit: 982a1dad0b58315cff7b54445f998499ef80e68d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66175363"
---
# <a name="column-names-with-the-path-specified-as-data"></a>Nomes de colunas com o caminho especificado como data()

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Se o caminho especificado como nome da coluna for "data()", o valor será tratado com um valor atômico no XML gerado. Um caractere de espaço será adicionado ao XML se o próximo item na serialização também for um valor atômico. Isso é útil quando você está criando elemento de tipo lista e valores de atributos. A consulta a seguir recupera a ID e o nome do modelo do produto e a lista de produtos naquele modelo do produto.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ProductModelID       AS "@ProductModelID",  
       Name                 AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
      FOR XML PATH (''))    AS "@ProductIDs"  
FROM  Production.ProductModel  
WHERE ProductModelID= 7   
FOR XML PATH('ProductModelData');  
```  
  
 O SELECT aninhado recupera uma lista de IDs de produtos. Ele especifica "data()" como o nome da coluna para IDs de produtos. Como o modo PATH especifica uma cadeia de caracteres vazia para o nome do elemento de linha, não há nenhum elemento de linha gerado. Em vez disso, os valores são retornados conforme são atribuídos a um atributo ProductIDs do elemento de linha `<ProductModelData>` do SELECT pai. Este é o resultado:  

```sql
<ProductModelData
  ProductModelID="7"
  ProductModelName="HL Touring Frame"
  ProductIDs="885 887 888 889 890 891 892 893"
/>
```

## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
