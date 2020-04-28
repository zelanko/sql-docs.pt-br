---
title: Expressões lógicas (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- logical operators [SQL Server], XQuery
- effective Boolean value [XQuery]
- logical expressions [XQuery]
- EBV
- expressions [XQuery], logical
ms.assetid: de94cd2e-2d48-49fb-9ebd-a2d90c79bf62
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b1dc7b961dd0b85824ea180cbc4815d5488a360
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68004499"
---
# <a name="logical-expressions-xquery"></a>Expressões lógicas (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  O XQuery dá suporte aos operadores **and** e **or** lógicos.  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 As expressões de teste `expression1,``expression2`,, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no, podem resultar em uma sequência vazia, uma sequência de um ou mais nós ou um único valor booliano. Com base no resultado, o valor Booliano efetivo da sequência é determinado da maneira seguinte:  
  
-   Se a expressão de teste resultar em uma sequência vazia, o resultado da expressão será False.  
  
-   Se a expressão de teste resultar em um único valor Booliano, esse valor será o resultado da expressão.  
  
-   Se a expressão de teste resultar em uma sequência de um ou mais nós, o resultado da expressão será True.  
  
-   Caso contrário, um erro estático surgirá.  
  
 O operador **and** e **or** lógico é então aplicado aos valores Boolianos resultantes das expressões com a semântica lógica padrão.  
  
 A consulta a seguir recupera do catálogo de produtos as imagens pequenas de ângulo de frente, `Picture` o <> elemento, para um modelo de produto específico. Observe que para cada documento de descrição de produto, o catálogo pode armazenar uma ou mais imagens de produto com atributos diferentes, como tamanho e ângulo.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $F in /PD:ProductDescription/PD:Picture[PD:Size="small"   
                                                 and PD:Angle="front"]  
     return   
         $F   
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 Este é o resultado:  
  
```  
<PD:Picture   
  xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  <PD:Angle>front</PD:Angle>  
  <PD:Size>small</PD:Size>  
  <PD:ProductPhotoID>31</PD:ProductPhotoID>  
</PD:Picture>  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões XQuery](../xquery/xquery-expressions.md)  
  
  
