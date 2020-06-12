---
title: Expressões quantificadas (XQuery) | Microsoft Docs
description: Saiba como usar expressões quantificadas em XQuery para aplicar Existential ou Quantificação universal a uma expressão em uma ou várias sequências.
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
- universal quantifiers
- effective Boolean value [XQuery]
- quantified expressions [XQuery]
- XQuery, quantified expressions
- every expression [XQuery]
- existential quantifiers [XQuery]
- some expression [XQuery]
- EBV
- expressions [XQuery], quantifiers
ms.assetid: a3a75a6c-8f67-4923-8406-1ada546c817f
author: rothja
ms.author: jroth
ms.openlocfilehash: 5f7c79cd185b88b8681460d2811f0d0ac4c20557
ms.sourcegitcommit: 9921501952147b9ce3e85a1712495d5b3eb13e5b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84215247"
---
# <a name="quantified-expressions-xquery"></a>Expressões quantificadas (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os quantificadores existenciais e universais especificam semânticas diferentes para operadores Boolianos que são aplicados a duas sequências. Isso é mostrado na tabela a seguir.  
  
 *Quantificador existencial*  
 Considerando-se duas sequências, se qualquer item na primeira sequência tiver uma correspondência na segunda sequência, com base no operador de comparação usado, o valor retornado será True.  
  
 *Quantificador universal*  
 Considerando-se duas sequências, se cada item na primeira sequência tiver uma correspondência na segunda sequência, o valor retornado será True.  
  
 O XQuery oferece suporte a expressões quantificadas da seguinte forma:  
  
```  
( some | every ) <variable> in <Expression> (,...) satisfies <Expression>  
```  
  
 Você pode usar essas expressões em uma consulta para aplicar explicitamente quantificação existencial ou universal a uma expressão em uma ou em várias sequências. No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a expressão na cláusula `satisfies` deve resultar em um dos seguintes: uma sequência de nó, uma sequência vazia ou um valor Booliano. O valor Booliano efetivo do resultado dessa expressão será usado na quantificação. A quantificação Existential que usa **algumas** retornará true se pelo menos um dos valores associados pelo quantificador tiver um resultado verdadeiro na expressão de satisfazo. A quantificação universal que usa a **cada** deve ter verdadeiro para todos os valores associados pelo quantificador.  
  
 Por exemplo, a consulta a seguir verifica cada \<Location> elemento para ver se ele tem um atributo LocationID.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        if (every $WC in //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID)  
        then  
             <Result>All work centers have workcenterLocation ID</Result>  
         else  
             <Result>Not all work centers have workcenterLocation ID</Result>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Como LocationID é um atributo necessário do \<Location> elemento, você recebe o resultado esperado:  
  
```  
<Result>All work centers have Location ID</Result>   
```  
  
 Em vez de usar o [método Query ()](../t-sql/xml/query-method-xml-data-type.md), você pode usar o [método Value ()](../t-sql/xml/value-method-xml-data-type.md) para retornar o resultado para o mundo relacional, conforme mostrado na consulta a seguir. A consulta retornará True se todos os locais de centro de trabalho tiverem atributos LocationID. Caso contrário, a consulta retornará False.  
  
```  
SELECT Instructions.value('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        every $WC in  //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID',   
  'nvarchar(10)') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 A consulta a seguir verifica se uma das imagens de produto é pequena. No catálogo de produto XML, são armazenados vários ângulos para cada imagem de produto de um tamanho diferente. Convém garantir que cada catálogo de produto XML inclua, pelo menos, uma imagem de tamanho pequeno. A consulta a seguir realiza isso:  
  
```  
SELECT ProductModelID, CatalogDescription.value('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     some $F in /PD:ProductDescription/PD:Picture  
        satisfies $F/PD:Size="small"', 'nvarchar(20)') as SmallPicturesStored  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Este é um resultado parcial:  
  
```  
ProductModelID SmallPicturesStored   
-------------- --------------------  
19             true        
```  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   Não há suporte para a asserção de tipo como parte da associação da variável nas expressões quantificadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões XQuery](../xquery/xquery-expressions.md)  
  
  
