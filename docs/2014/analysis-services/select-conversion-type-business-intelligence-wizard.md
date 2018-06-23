---
title: Selecione o tipo de conversão (Assistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.conversiontype.f1
ms.assetid: 2c664138-e8a1-4c47-8e7d-ee01c57e4692
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ba4018a6ce30e4e7de4e0ca3e79ae07007015650
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122257"
---
# <a name="select-conversion-type-business-intelligence-wizard"></a>Selecionar Tipo de Conversão (Assistente de Business Intelligence)
  Use a página **Selecionar Tipo de Conversão** para definir a relação entre as moedas locais e as moedas de relatório para transações armazenadas em várias moedas. Uma moeda local é a moeda na qual as transações de medidas selecionadas na página **Selecionar Medidas** estão armazenadas. Uma moeda de relatório é a moeda na qual as transações selecionadas na página **Selecionar Medidas** são convertidas.  
  
> [!NOTE]  
>  Essa página não será exibida se o Assistente de Business Intelligence tiver sido iniciado no Designer de Dimensão ou clicando com o botão direito do mouse em uma dimensão no Gerenciador de Soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opções  
 **Muitos para muitos**  
 Armazena transações que usam moedas locais. A funcionalidade de conversão de moeda converte essas transações na moeda corrente especificada na página **Definir Opções de Conversão de Moeda** e, em seguida, em uma ou mais moedas de relatório.  
  
 Por exemplo, a moeda corrente pode estar definida como USD (dólares dos EUA) e a tabela de fatos armazenar transações em EUR (euros), AUD (dólares australianos) e MXN (pesos mexicanos). A seleção desta opção converte essas transações das moedas locais especificadas na moeda corrente e, em seguida, as transações são convertidas novamente da moeda corrente na moeda de relatório especificada. O resultado é que as transações podem ser armazenadas nas moedas locais especificadas e exibidas na moeda corrente especificada ou em qualquer uma das moedas de relatório especificadas na página **Especificar Moedas de Relatório** .  
  
 **Muitos para um**  
 Armazena transações que usam moedas locais. A funcionalidade de conversão de moeda converte essas transações na moeda corrente especificada na página **Definir Opções de Conversão de Moeda** . A moeda corrente funciona como a única moeda de relatório especificada.  
  
> [!NOTE]  
>  Se esta opção estiver selecionada, a página **Especificar Moedas de Relatório** não será exibida.  
  
 Por exemplo, a moeda corrente pode estar definida como USD (dólares dos EUA) e a tabela de fatos armazenar transações em EUR (euros), AUD (dólares australianos) e MXN (pesos mexicanos). A seleção dessa opção converte as transações das moedas locais especificadas na moeda corrente. O resultado é que as transações podem ser armazenadas nas moedas locais especificadas e exibidas na moeda corrente especificada.  
  
 **Um para muitos**  
 Armazene transações usando a moeda corrente especificada na página **Definir Opções de Conversão de Moeda** e, em seguida, converta-a em uma ou mais moedas de relatório.  
  
> [!NOTE]  
>  Se essa opção estiver selecionada, a página **Definir Referência de Moeda Local** não será exibida.  
  
 Por exemplo, a moeda corrente pode estar definida como USD (dólares dos EUA) e a tabela de fatos armazenar transações em USD. A seleção dessa opção converte essas transações da moeda corrente nas moedas de relatório especificadas. O resultado é que essas transações podem ser armazenadas na moeda corrente especificada e exibidas na moeda corrente especificada ou em qualquer uma das moedas de relatório especificadas na página **Especificar Moedas de Relatório** .  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente do Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Designer de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Designer de dimensão &#40;Analysis Services - dados multidimensionais&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  