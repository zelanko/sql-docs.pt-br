---
title: Operadores XQuery em relação ao tipo de dados XML | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
author: rothja
ms.author: jroth
ms.openlocfilehash: b113fbd8111072790d1f0904b3e751c6629725b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67945951"
---
# <a name="xquery-operators-against-the-xml-data-type"></a>Operadores XQuery em relação ao tipo de dados xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  A XQuery oferece suporte aos seguintes operadores:  
  
-   Operadores numéricos (+, -, *, div, mod)  
  
-   Operadores para comparação de valor (eq, ne, lt, gt, le, ge)  
  
-   Operadores para comparação geral (=,! =, \<, >, \<=, >=)  
  
 Para obter mais informações sobre esses operadores, consulte [expressões de comparação &#40;XQuery&#41;](../xquery/comparison-expressions-xquery.md)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-general-operators"></a>a. Usando operadores gerais  
 A consulta ilustra o uso de operadores gerais que se aplicam a sequências, além de comparar sequências. A consulta recupera uma sequência de números de telefone para cada cliente da coluna **AdditionalContactInfo** da tabela **Contact** . Em seguida, essa sequência é comparada com a sequência de dois números de telefone ("111-111-1111", "222-2222").  
  
 A consulta usa o **=** operador de comparação. Cada nó na sequência no lado direito do **=** operador é comparado com cada nó na sequência no lado esquerdo. Se os nós corresponderem, a comparação de nós será **verdadeira**. Em seguida, o nó será convertido em int, comparado com 1 e a consulta retornará o ID do cliente.  
  
```sql
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 Há outra maneira de observar como a consulta anterior funciona: cada valor de número de telefone celular recuperado da coluna **AdditionalContactInfo** é comparado com o conjunto de dois números de telefone. Se o valor estiver no conjunto, esse cliente será retornado no resultado.  
  
### <a name="b-using-a-numeric-operator"></a>B. Usando um operador numérico  
 O operador + nessa consulta é um operador de valor, pois se aplica a um único item. Por exemplo, o valor 1 é adicionado a um tamanho de lote retornado pela consulta:  
  
```sql
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
 A consulta a seguir recupera os `Picture` elementos de> <para um modelo de produto em que o tamanho da imagem é "pequeno":  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Como ambos os operandos para o operador **EQ** são valores atômicos, o operador Value é usado na consulta. Você pode escrever a mesma consulta usando o operador de comparação geral ( **=** ).  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery no tipo de dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
