---
title: "Definir o idioma para parâmetros de relatório em uma URL | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- overriding report language settings
- report servers [Reporting Services], language settings
- languages [Reporting Services]
- URL access [Reporting Services], language overrides
- international considerations [Reporting Services]
- global considerations [Reporting Services]
ms.assetid: e1ccf22f-80d6-45bc-aae0-f5f263275092
caps.latest.revision: "29"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 65ad7f21e50fa0270a5ed39aeefd562293e19c63
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="set-the-language-for-report-parameters-in-a-url"></a>Definir o idioma dos parâmetros do relatório em uma URL
  O parâmetro de acesso de URL *rs:ParameterLanguage* reduz o problema de os parâmetros de relatório sensíveis a cultura, como datas, horas, moeda e números serem interpretados por meio do idioma do navegador. Com o *rs:ParameterLanguage*, a URL agora é interpretada independentemente do navegador. Por exemplo, se o servidor de relatório for definido como uma configuração regional do alemão, mas um usuário estiver acessando um relatório via uma URL usando um navegador definido com inglês norte-americano, os valores do parâmetro que são transmitidos para um servidor de relatório serão interpretados incorretamente.  
  
 Considere a URL a seguir para um relatório:  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008  
```  
  
 No caso acima, o servidor, executado em uma cultura de "de-de", gera uma URL por meio de uma assinatura de e-mail ou um hiperlink. O hyperlink indica que o relatório deve ser parametrizado pela data de início de 04 de outubro de 2008 e uma data de término de 11 de outubro de 2008 de acordo com os padrões de data/hora alemães. Entretanto, um usuário que está acessando a URL por meio de um navegador definido como "en-us" força o servidor a interpretar os valores como 10 de abril de 2008 e 10 de novembro de 2008 de acordo com os padrões de data/hora do inglês norte-americano. Para corrigir o problema, o *rs:ParameterLanguage* pode ser usado para substituir o idioma do navegador para interpretação de parâmetro:  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
```  
  
 Além de um valor **true** e **false** para o parâmetro de acesso da URL *rc:Parameters*, agora você pode transmitir um valor de **Recolhido**. Ao usar *rc:Parameters*=**Recolhido** em uma URL, a área de prompt do parâmetro do visualizador de HTML será recolhida, mas ainda poderá ser alternada pelo usuário. Um valor igual a **false** remove a área de prompt de parâmetro da barra de ferramentas do visualizador de HTML e a torna indisponível para o usuário final.  
  
## <a name="see-also"></a>Consulte Também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  
  
  
