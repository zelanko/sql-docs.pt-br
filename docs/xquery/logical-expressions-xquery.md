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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004499"
---
# <a name="logical-expressions-xquery"></a>Expressões lógicas (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery oferece suporte à lógica **e** e **ou** operadores.  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 As expressões de teste `expression1,``expression2`, no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode resultar em uma sequência vazia, uma sequência de um ou mais nós ou um único valor booliano. Com base no resultado, o valor Booliano efetivo da sequência é determinado da maneira seguinte:  
  
-   Se a expressão de teste resultar em uma sequência vazia, o resultado da expressão será False.  
  
-   Se a expressão de teste resultar em um único valor Booliano, esse valor será o resultado da expressão.  
  
-   Se a expressão de teste resultar em uma sequência de um ou mais nós, o resultado da expressão será True.  
  
-   Caso contrário, um erro estático surgirá.  
  
 A lógica **e** e **ou** operador é então aplicado a valores booliano resultantes das expressões com as semânticas lógicas padrão.  
  
 A consulta a seguir recupera do catálogo de produtos, as imagens pequenas de ângulo frontal, o <`Picture`> elemento, para um modelo de produto específico. Observe que para cada documento de descrição de produto, o catálogo pode armazenar uma ou mais imagens de produto com atributos diferentes, como tamanho e ângulo.  
  
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
  
 Esse é o resultado:  
  
```  
<PD:Picture   
  xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  <PD:Angle>front</PD:Angle>  
  <PD:Size>small</PD:Size>  
  <PD:ProductPhotoID>31</PD:ProductPhotoID>  
</PD:Picture>  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões XQuery](../xquery/xquery-expressions.md)  
  
  
