---
title: "Usando variáveis e parâmetros (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5ac634400b85e49cdaf9f57e683cc13fe781ed2b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="using-variables-and-parameters-mdx"></a>Usando variáveis e parâmetros (MDX)
  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], é possível parametrizar uma instrução MDX (Multidimensional Expressions). Uma instrução parametrizada permite a criação de instruções genéricas que podem ser personalizadas no tempo de execução.  
  
 Ao criar uma instrução parametrizada, você identifica o nome do parâmetro incluindo um prefixo ao nome com o sinal arroba (@). Por exemplo, @Year seria um nome de parâmetro válido  
  
 A linguagem MDX oferece suporte apenas a valores literais ou escalares. Para criar um parâmetro que faça referência a um membro, conjunto ou tupla, use uma função como [StrToMember](../../../mdx/strtomember-mdx.md) ou [StrToSet](../../../mdx/strtoset-mdx.md).  
  
 No seguinte XML de exemplo de análise (XMLA), o @CountryName parâmetro conterá o país em que o cliente para os dados são recuperados:  
  
```  
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">  
  <Body>  
    <Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <Command>  
        <Statement>  
select [Measures].members on 0,   
       Filter(Customer.[Customer Geography].Country.members,   
              Customer.[Customer Geography].CurrentMember.Name =  
              @CountryName) on 1  
from [Adventure Works]  
</Statement>  
      </Command>  
      <Properties />  
      <Parameters>  
        <Parameter>  
          <Name>CountryName</Name>  
          <Value>'United Kingdom'</Value>  
        </Parameter>  
      </Parameters>  
    </Execute>  
  </Body>  
</Envelope>  
```  
  
 Para usar essa funcionalidade com OLE DB, use a interface **ICommandWithParameters** . Para usar essa funcionalidade com ADOMD.Net, use a interface **AdomdCommand.Parameters** .  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do script MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  

