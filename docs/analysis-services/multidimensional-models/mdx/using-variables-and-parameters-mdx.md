---
title: "Usando variáveis e parâmetros (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fa5c3ec91afb2fd8321aafa6146e9f9061c27c26
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="using-variables-and-parameters-mdx"></a>Usando variáveis e parâmetros (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], você pode parametrizar uma instrução MDX (Multidimensional Expressions). Uma instrução parametrizada permite a criação de instruções genéricas que podem ser personalizadas no tempo de execução.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do script MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
