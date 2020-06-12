---
title: Usando variáveis e parâmetros (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
author: minewiskan
ms.author: owend
ms.openlocfilehash: fd01cf78ea5e3284aa51cad7dc848176a5dc9298
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546138"
---
# <a name="using-variables-and-parameters-mdx"></a>Usando variáveis e parâmetros (MDX)
  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , você pode parametrizar uma instrução MDX (Multidimensional Expressions). Uma instrução parametrizada permite a criação de instruções genéricas que podem ser personalizadas no runtime.  
  
 Ao criar uma instrução parametrizada, você identifica o nome do parâmetro incluindo um prefixo ao nome com o sinal arroba (@). Por exemplo, @Year seria um nome de parâmetro válido  
  
 A linguagem MDX oferece suporte apenas a valores literais ou escalares. Para criar um parâmetro que faça referência a um membro, conjunto ou tupla, use uma função como [StrToMember](/sql/mdx/strtomember-mdx) ou [StrToSet](/sql/mdx/strtoset-mdx).  
  
 No seguinte exemplo de XML for Analysis (XMLA), o @CountryName parâmetro conterá o país para o qual os dados do cliente são recuperados:  
  
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
  
 Para usar essa funcionalidade com OLE DB, use a interface `ICommandWithParameters`. Para usar essa funcionalidade com ADOMD.Net, use a interface **AdomdCommand.Parameters** .  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do script MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
  
