---
title: Expressões condicionais (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, conditional expressions
- expressions [XQuery], conditional
- effective Boolean value [XQuery]
- if-then-else statement [XQuery]
- conditional expressions [XQuery]
- EBV
ms.assetid: b280dd96-c80f-4c51-bc06-a88d42174acb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 62a061632b5f598932fe29499519d7eb897c78a6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041737"
---
# <a name="conditional-expressions-xquery"></a>Expressões condicionais (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery oferece suporte aos seguinte condicional **if-then-else** instrução:  
  
```  
if (<expression1>)  
then  
  <expression2>  
else  
  <expression3>  
```  
  
 Dependendo do valor Booliano efetivo de `expression1`, a `expression2` ou a `expression3` é avaliada. Por exemplo:  
  
-   Se a expressão de teste, `expression1`, resultar em uma sequência vazia, o resultado será False.  
  
-   Se a expressão de teste, `expression1`, resultar em um valor Booliano simples, esse valor será o resultado da expressão.  
  
-   Se a expressão de teste, `expression1`, resultar em uma sequência de um ou mais nós, o resultado da expressão será True.  
  
-   Caso contrário, um erro estático surgirá.  
  
 Também observe o seguinte:  
  
-   A expressão de teste deve ser incluída entre parênteses.  
  
-   O **else** expressão é necessária. Se você não precisar dela, poderá retornar " ( ) ", como ilustrado nos exemplos neste tópico.  
  
 Por exemplo, a consulta a seguir é especificada em relação a **xml** variável de tipo. O **se** condição testa o valor da variável SQL (@v) dentro da expressão XQuery usando a [função SQL: Variable](../xquery/xquery-extension-functions-sql-variable.md) função de extensão. Se o valor de variável for "FirstName", ele retornará o elemento <`FirstName`>. Caso contrário, retornará o elemento <`LastName`>.  
  
```  
declare @x xml  
declare @v varchar(20)  
set @v='FirstName'  
set @x='  
<ROOT rootID="2">  
  <FirstName>fname</FirstName>  
  <LastName>lname</LastName>  
</ROOT>'  
SELECT @x.query('  
if ( sql:variable("@v")="FirstName" ) then  
  /ROOT/FirstName  
 else  
   /ROOT/LastName  
')  
```  
  
 Esse é o resultado:  
  
```  
<FirstName>fname</FirstName>  
```  
  
 A consulta a seguir recupera as primeiras duas descrições de recurso da descrição do catálogo de produtos de um modelo de produto específico. Se houver mais recursos no documento, ele adicionará um elemento <`there-is-more`> com conteúdo vazio.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /p1:ProductDescription/@ProductModelID }  
          { /p1:ProductDescription/@ProductModelName }   
          {  
            for $f in /p1:ProductDescription/p1:Features/*[position()\<=2]  
            return  
            $f   
          }  
          {  
            if (count(/p1:ProductDescription/p1:Features/*) > 2)  
            then \<there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Na consulta anterior, a condição na **se** expressão verifica se há mais de dois elementos filho em <`Features`>. Caso haja, ela retornará o elemento `\<there-is-more/>` no resultado.  
  
 Esse é o resultado:  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  \<p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p1:WarrantyPeriod>3 years\</p1:WarrantyPeriod>  
    \<p1:Description>parts and labor\</p1:Description>  
  \</p1:Warranty>  
  \<p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p2:NoOfYears>10 years\</p2:NoOfYears>  
    \<p2:Description>maintenance contract available through your dealer or any AdventureWorks retail store.\</p2:Description>  
  \</p2:Maintenance>  
  \<there-is-more />  
</Product>  
```  
  
 Na consulta a seguir, será retornado um elemento <`Location`> com um atributo LocationID se o local de centro de trabalho não especificar as horas de instalação.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in //AWMI:root/AWMI:Location  
        return  
        if ( $WC[not(@SetupHours)] )  
        then  
          <WorkCenterLocation>  
             { $WC/@LocationID }   
          </WorkCenterLocation>  
         else  
           ()  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Esse é o resultado:  
  
```  
<WorkCenterLocation LocationID="30" />  
<WorkCenterLocation LocationID="45" />  
<WorkCenterLocation LocationID="60" />  
```  
  
 Essa consulta pode ser escrita sem a **se** cláusula, conforme mostrado no exemplo a seguir:  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in //AWMI:root/AWMI:Location[not(@SetupHours)]   
        return  
          <Location>  
             { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões XQuery](../xquery/xquery-expressions.md)  
  
  
