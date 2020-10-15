---
title: Definir a localidade em um relatório ou caixa de texto (Reporting Services) | Microsoft Docs
description: Use a propriedade Language em uma caixa de texto para fornecer a configuração de localidade para formatos que exibem dados que diferem por idioma e região no Construtor de Relatórios.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- locales [Reporting Services]
ms.assetid: df115b01-184b-47f0-b5ec-0ad965ff9bee
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e5a222b00b7ca2dc76c8038dd3b3b3bc4f1f72cd
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935122"
---
# <a name="set-the-locale-for-a-report-or-text-box-reporting-services"></a>Definir a localidade em um relatório ou caixa de texto (Reporting Services)
  A propriedade **Language** em um relatório ou caixa de texto contém as configurações de localidade, que determinam os formatos padrão para a exibição dos dados do relatório que são diferenciados por idioma e região, como, por exemplo, data, moeda ou valores numéricos. A propriedade **Language** em uma caixa de texto substitui a propriedade **Language** em um relatório. Quando nenhum valor é especificado para **Language**, o Reporting Services usa a localidade do sistema operacional no servidor de relatórios para os relatórios publicados ou do computador em que o relatório está sendo gerado na visualização do relatório.  
  
 Em relatórios em HTML, você pode substituir o valor **Idioma** padrão e usar o idioma especificado pelo cabeçalho HTTP do cliente navegador usando o campo interno User!Language em uma expressão para a propriedade **Language** de um relatório ou caixa de texto.  
  
 A propriedade **Language** também pode ser especificada para um relatório em uma URL. Para mais informações, consulte [Definir o idioma dos parâmetros do relatório em uma URL](../../reporting-services/set-the-language-for-report-parameters-in-a-url.md).  
  
### <a name="to-set-the-locale-for-a-report"></a>Para definir a localidade para um relatório  
  
1.  No modo Design, clique fora da superfície de design para selecionar o relatório.  
  
2.  No painel Propriedades, na propriedade **Language** , digite ou selecione o idioma que deseja usar no relatório.  
  
### <a name="to-set-the-locale-for-a-text-box"></a>Para definir a localidade para uma caixa de texto  
  
1.  No modo Design, selecione a caixa de texto para a qual você deseja aplicar as configurações de localidade.  
  
2.  No painel Propriedades, faça o seguinte:  
  
    -   Na propriedade **Calendar** , digite ou selecione o calendário que deseja usar para as datas.  
  
    -   Na propriedade **Direction** , digite ou selecione a direção na qual deseja que o texto seja exibido.  
  
    -   Na propriedade **Language** , digite ou selecione o idioma que deseja usar na caixa de texto. Esse valor substitui a propriedade **Language** para o Relatório.  
  
    -   Na propriedade **NumeralLanguage** , digite ou selecione o formato que deseja usar para os números na caixa de texto.  
  
    -   Na propriedade **NumeralVariant** , digite ou selecione a variação do formato que deseja usar para os números na caixa de texto.  
  
    -   Na propriedade **UnicodeBiDi** , digite ou selecione o nível de inserção bidirecional que deseja usar na caixa de texto.  
  
## <a name="see-also"></a>Consulte Também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Considerações sobre design da solução para implantações multilíngues ou globais (Reporting Services)](/previous-versions/sql/)  
  
