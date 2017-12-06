---
title: "Operadores XQuery em relação ao tipo de dados xml | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8fc773e1770b907b6eba5e4d09372f0654054d47
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="xquery-operators-against-the-xml-data-type"></a>Operadores XQuery em relação ao tipo de dados xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  A XQuery oferece suporte aos seguintes operadores:  
  
-   Operadores numéricos (+, -, *, div, mod)  
  
-   Operadores para comparação de valor (eq, ne, lt, gt, le, ge)  
  
-   Operadores de comparação geral (=,! =, \<, >, \<=, > =)  
  
 Para obter mais informações sobre esses operadores, consulte [expressões de comparação &#40; XQuery &#41;](../xquery/comparison-expressions-xquery.md)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-general-operators"></a>A. Usando operadores gerais  
 A consulta ilustra o uso de operadores gerais que se aplicam a sequências, além de comparar sequências. A consulta recupera uma sequência de números de telefone para cada cliente do **AdditionalContactInfo** coluna o **contato** tabela. Em seguida, essa sequência é comparada com a sequência de dois números de telefone ("111-111-1111", "222-2222").  
  
 A consulta usa o  **=**  operador de comparação. Cada nó na sequência no lado direito do  **=**  operador é comparado com cada nó na sequência no lado esquerdo. Se os nós forem correspondentes, a comparação de nó é **TRUE**. Em seguida, o nó será convertido em int, comparado com 1 e a consulta retornará o ID do cliente.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 Há outra maneira de observar como a consulta anterior funciona: cada valor de número de telefone do telefone recuperado do **AdditionalContactInfo** coluna é comparada com o conjunto de dois números de telefone. Se o valor estiver no conjunto, esse cliente será retornado no resultado.  
  
### <a name="b-using-a-numeric-operator"></a>B. Usando um operador numérico  
 O operador + nessa consulta é um operador de valor, pois se aplica a um único item. Por exemplo, o valor 1 é adicionado a um tamanho de lote retornado pela consulta:  
  
```  
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in (/AWMI:root/AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"  
                   LotSize  = "{  number($i/@LotSize) }"  
                   LotSize2 = "{ number($i/@LotSize) + 1 }"  
                   LotSize3 = "{ number($i/@LotSize) + 2 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
### <a name="c-using-a-value-operator"></a>C. Usando um operador de valor  
 A seguinte consulta recupera os elementos <`Picture`> de um modelo de produto em que o tamanho da imagem é "pequeno":  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Como ambos os operandos para o **eq** operador são valores atômicos, o operador de valor é usado na consulta. Você pode escrever a mesma consulta usando o operador de comparação geral (  **=**  ).  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em relação ao tipo de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
