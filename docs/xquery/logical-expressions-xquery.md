---
title: Expressões lógicas (XQuery) | Microsoft Docs
description: Saiba mais sobre as expressões lógicas com suporte no XQuery.
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
ms.openlocfilehash: 140a1631cfd4b7068e4729004f7aa41d9535a904
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717189"
---
# <a name="logical-expressions-xquery"></a>Expressões lógicas (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  O XQuery dá suporte aos operadores **and** e **or** lógicos.  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 As expressões de teste, `expression1,``expression2` , no, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem resultar em uma sequência vazia, uma sequência de um ou mais nós ou um único valor booliano. Com base no resultado, o valor Booliano efetivo da sequência é determinado da maneira seguinte:  
  
-   Se a expressão de teste resultar em uma sequência vazia, o resultado da expressão será False.  
  
-   Se a expressão de teste resultar em um único valor Booliano, esse valor será o resultado da expressão.  
  
-   Se a expressão de teste resultar em uma sequência de um ou mais nós, o resultado da expressão será True.  
  
-   Caso contrário, um erro estático surgirá.  
  
 O operador **and** e **or** lógico é então aplicado aos valores Boolianos resultantes das expressões com a semântica lógica padrão.  
  
 A consulta a seguir recupera do catálogo de produtos as imagens pequenas de ângulo de frente, o <`Picture`> elemento, para um modelo de produto específico. Observe que para cada documento de descrição de produto, o catálogo pode armazenar uma ou mais imagens de produto com atributos diferentes, como tamanho e ângulo.  
  
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
  
  
