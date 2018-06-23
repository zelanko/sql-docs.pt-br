---
title: Definir a localidade em um relatório ou caixa de texto (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- locales [Reporting Services]
ms.assetid: df115b01-184b-47f0-b5ec-0ad965ff9bee
caps.latest.revision: 43
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: d2fdbe4d44dd16d4f3094725c7032379ab163902
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008565"
---
# <a name="set-the-locale-for-a-report-or-text-box-reporting-services"></a>Definir a localidade em um relatório ou caixa de texto (Reporting Services)
  A propriedade **Language** em um relatório ou caixa de texto contém as configurações de localidade, que determinam os formatos padrão para a exibição dos dados do relatório que são diferenciados por idioma e região, como, por exemplo, data, moeda ou valores numéricos. A propriedade **Language** em uma caixa de texto substitui a propriedade **Language** em um relatório. Quando nenhum valor é especificado para **Language**, o Reporting Services usa a localidade do sistema operacional no servidor de relatórios para os relatórios publicados ou do computador em que o relatório está sendo gerado na visualização do relatório.  
  
 Em relatórios em HTML, você pode substituir o valor **Idioma** padrão e usar o idioma especificado pelo cabeçalho HTTP do cliente navegador usando o campo interno User!Language em uma expressão para a propriedade **Language** de um relatório ou caixa de texto.  
  
 A propriedade **Language** também pode ser especificada para um relatório em uma URL. Para obter mais informações, consulte [definir o idioma para parâmetros de relatório em uma URL](../set-the-language-for-report-parameters-in-a-url.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Expressão usa relatórios de &#40;SSRS e construtor de relatórios&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  