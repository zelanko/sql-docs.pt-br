---
title: Função SUM (XQuery) | Microsoft Docs
description: Saiba mais sobre a função XQuery Sum () que retorna a soma de uma sequência de números.
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sum function [XQuery]
- fn:sum function
ms.assetid: 12288f37-b54c-4237-b75e-eedc5fe8f96d
author: rothja
ms.author: jroth
ms.openlocfilehash: 5f329d4e4684997138d3c54e6b2831d70b961a93
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765653"
---
# <a name="aggregate-functions---sum"></a>Funções de Agregação – sum
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Retorna a soma de uma sequência de números.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:sum($arg as xdt:anyAtomicType*) as xdt:anyAtomicType  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Sequência de valores atômicos cuja soma deve ser calculada.  
  
## <a name="remarks"></a>Comentários  
 Todos os tipos de valores Atom que são passados para **Sum ()** precisam ser subtipos do mesmo tipo base. Os tipos base aceitos são os três tipos base numéricos internos ou xdt:untypedAtomic. Valores do tipo xdt:untypedAtomic são convertidos em xs:double. Se houver uma mistura desses tipos, ou se outros valores de outros tipos forem passados, um erro estático será gerado.  
  
 O resultado de **Sum ()** recebe o tipo base do passado em tipos, como xs: Double no caso de xdt: untypedAtomic, mesmo que a entrada seja opcionalmente a sequência vazia. Se a entrada estiver estaticamente vazia, o resultado será 0 com o tipo estático e dinâmico de xs:integer.  
  
 A função **Sum ()** retorna a soma dos valores numéricos. Se um valor de xdt: untypedAtomic não puder ser convertido em xs: Double, o valor será ignorado na sequência de entrada, *$ARG*. Se a entrada for uma sequência vazia dinamicamente calculada, o valor 0 do tipo base usado será retornado.  
  
 A função retorna um erro de runtime quando um estouro ou exceção fora do intervalo acontece.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-using-the-sum-xquery-function-to-find-the-total-combined-number-of-labor-hours-for-all-work-center-locations-in-the-manufacturing-process"></a>a. Usando a função sum() XQuery para localizar o número combinado total de horas de trabalho para todos os locais do centro de trabalho no processo de fabricação.  
 A consulta a seguir acha o total de horas de trabalho de todos os locais de centro de trabalho no processo de fabricação de todos os modelos de produtos nos quais as instruções de fabricação são armazenadas.  
  
```  
SELECT Instructions.query('         
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
  <ProductModel PMID= "{ sql:column("Production.ProductModel.ProductModelID") }"         
  ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >         
   <TotalLaborHrs>         
     { sum(//AWMI:Location/@LaborHours) }         
   </TotalLaborHrs>         
 </ProductModel>         
    ') as Result         
FROM Production.ProductModel         
WHERE Instructions is not NULL         
```  
  
 Este é o resultado parcial.  
  
```  
<ProductModel PMID="7" ProductModelName="HL Touring Frame">  
   <TotalLaborHrs>12.75</TotalLaborHrs>  
</ProductModel>  
<ProductModel PMID="10" ProductModelName="LL Touring Frame">  
  <TotalLaborHrs>13</TotalLaborHrs>  
</ProductModel>  
...  
```  
  
 Em vez de retornar o resultado como XML, você pode escrever a consulta para gerar resultados relacionais, como mostrado nesta consulta:  
  
```  
SELECT ProductModelID,         
        Name,         
        Instructions.value('declare namespace   
      AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
    sum(//AWMI:Location/@LaborHours)', 'float') as TotalLaborHours         
FROM Production.ProductModel         
WHERE Instructions is not NULL          
```  
  
 Este é um resultado parcial:  
  
```  
ProductModelID Name                 TotalLaborHours         
-------------- -------------------------------------------------  
7              HL Touring Frame           12.75                   
10             LL Touring Frame           13                      
43             Touring Rear Wheel         3                       
...  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   Somente a versão de argumento único de **Sum ()** tem suporte.  
  
-   Se a entrada for uma sequência vazia dinamicamente calculada, o valor 0 do tipo base usado será retornado, em vez do tipo xs:integer.  
  
-   A função **Sum ()** mapeia todos os inteiros para xs: decimal.  
  
-   Não há suporte para a função **Sum ()** em valores do tipo xs: Duration.  
  
-   Não há suporte para sequências que misturam tipos, atravessando os limites de tipo base.  
  
-   A soma ((xs: Double ("INF"), xs: Double ("-INF"))) gera um erro de domínio.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
