---
title: Função Last (XQuery) | Microsoft Docs
description: Saiba mais sobre a função XQuery Last () que retorna o índice inteiro do último item em uma sequência.
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
- last function [XQuery]
- fn:last function
ms.assetid: dc92086e-3b01-4b0b-9f54-3bbf306cf7ae
author: rothja
ms.author: jroth
ms.openlocfilehash: 3713f0fadfe186c31a26f2f19adea88da2f28384
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729524"
---
# <a name="context-functions---last-xquery"></a>Funções de Contexto – last (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Retorna o número de itens na sequência que está sendo processada atualmente. Especificamente, retorna o índice de inteiro do último item na sequência. O primeiro item na sequência tem um valor de índice de 1.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:last() as xs:integer  
```  
  
## <a name="remarks"></a>Comentários  
 Em SQL Server, **fn: Last ()** só pode ser usado no contexto de um predicado dependente de contexto. Mais precisamente, ele só pode ser usado entre parênteses (`[ ]`).  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-last-xquery-function-to-retrieve-the-last-two-manufacturing-steps"></a>a. Usando a função last() XQuery para recuperar as últimas duas etapas de fabricação  
 A consulta a seguir recupera as duas últimas etapas do processo de fabricação de um modelo de produto específico. O valor, o número de etapas de fabricação, retornado pela função **Last ()** , é usado nesta consulta para recuperar as duas últimas etapas de fabricação.  
  
```  
SELECT ProductModelID, Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Na consulta anterior, a função **Last ()** em/ `/AWMI:root//AWMI:Location)[1]/AWMI:step[last()]` retorna o número de etapas de fabricação. Esse valor é usado para recuperar a última etapa de fabricação no local do centro de trabalho.  
  
 Este é o resultado:  
  
```  
ProductModelID Result    
-------------- -------------------------------------  
7      <LastTwoManuSteps>  
         <Last-1Step>  
            When finished, inspect the forms for defects per   
            Inspection Specification .  
         </Last-1Step>  
         <LastStep>Remove the frames from the tool and place them   
            in the Completed or Rejected bin as appropriate.  
         </LastStep>  
       </LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
