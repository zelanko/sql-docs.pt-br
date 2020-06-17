---
title: Atomização (XQuery) | Microsoft Docs
description: Saiba mais sobre o processo de atomização no XQuery no qual os valores tipados de um item são extraídos.
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
author: rothja
ms.author: jroth
ms.openlocfilehash: 70d623d8583535aae7ddcc23f26ab7c5e4e36fc7
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84886889"
---
# <a name="atomization-xquery"></a>Atomização (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A atomização é o processo de extrair o valor digitado de um item. Esse processo está implícito em determinadas circunstâncias. Alguns dos operadores XQuery, como operadores de aritmética e de comparação, dependem desse processo. Por exemplo, quando você aplica operadores aritméticos diretamente a nós, o valor digitado de um nó é recuperado pela primeira vez, invocando implicitamente a [função de dados](../xquery/data-accessor-functions-data-xquery.md). Isso passa o valor atômico como um operando para o operador aritmético.  
  
 Por exemplo, a consulta a seguir retorna o total dos atributos LaborHours. Nesse caso, **os dados ()** são aplicados implicitamente aos nós de atributo.  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 Embora não seja necessário, você também pode especificar explicitamente a função **Data ()** :  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 Outro exemplo de atomização implícita é quando você usa operadores aritméticos. O **+** operador requer valores atômicos, e os **dados ()** são aplicados implicitamente para recuperar o valor atômico do atributo LaborHours. A consulta é especificada na coluna instruções do tipo **XML** na tabela ProductModel. A consulta a seguir retorna o atributo LaborHours três vezes. Na consulta, observe o seguinte:  
  
-   Na construção do atributo OriginalLaborHours, a atomização é aplicada implicitamente à sequência de singleton retornada por (`$WC/@LaborHours`). O valor digitado do atributo LaborHours é atribuído a OriginalLaborHours.  
  
-   Na construção do atributo UpdatedLaborHoursV1, o operador aritmético requer valores atômicos. Portanto, **Data ()** é aplicado implicitamente ao atributo LaborHours que é retornado por ( `$WC/@LaborHours` ). O valor atômico 1 é então adicionado a ele. A construção do atributo UpdatedLaborHoursV2 mostra a aplicação explícita de **dados ()**, mas não é necessária.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location[1]  
        return  
            <WC OriginalLaborHours = "{ $WC/@LaborHours }"  
                UpdatedLaborHoursV1 = "{ $WC/@LaborHours + 1 }"   
                UpdatedLaborHoursV2 = "{ data($WC/@LaborHours) + 1 }" >  
            </WC>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Este é o resultado:  
  
```  
<WC OriginalLaborHours="2.5"   
    UpdatedLaborHoursV1="3.5"   
    UpdatedLaborHoursV2="3.5" />  
```  
  
 A atomização resulta em uma instância de um tipo simples, um conjunto vazio ou um erro de tipo estático.  
  
 A atomização também ocorre em parâmetros de expressão de comparação passados para funções, valores retornados por funções, expressões **Cast ()** e expressões de ordenação passadas na cláusula order by.  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas do XQuery](../xquery/xquery-basics.md)   
 [Expressões de comparação &#40;XQuery&#41;](../xquery/comparison-expressions-xquery.md)   
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
