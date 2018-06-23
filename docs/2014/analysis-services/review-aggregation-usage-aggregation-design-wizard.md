---
title: Revise o uso de agregação (Assistente de Design de agregação) | Microsoft Docs
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
- sql12.asvs.aggregationdesignwizard.reviewusage.f1
ms.assetid: 107ee872-3df2-4931-b56c-af11e38f6745
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5a26ea23dda5bba4813a9c5a99d797471124750d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118232"
---
# <a name="review-aggregation-usage-aggregation-design-wizard"></a>Revisar Uso de Agregação (Assistente de Design de Agregação)
  Use a página **Revisar Uso de Agregação** para efetuar configurações do uso de agregação.  
  
## <a name="options"></a>Opções  
 **Default**  
 Selecione para definir a configuração do uso de agregação do atributo como Padrão. Quando essa configuração é utilizada, o designer aplica uma regra padrão com base no tipo de atributo e dimensão.  
  
 `Full`  
 Selecione para definir a configuração de uso de agregação para o atributo `Full`. Quando essa configuração é utilizada, cada agregação para o cubo deve incluir esse atributo ou um atributo relacionado inferior na cadeia de atributos. O `Full` configuração de uso de agregação deve ser evitada quando um atributo contiver muitos membros. Se for especificada para vários atributos ou atributos que têm muitos membros, essa configuração poderá impedir a criação de agregações por causa do seu tamanho excessivo.  
  
 **Nenhuma**  
 Selecione para definir a configuração do uso de agregação do atributo como Nenhum. Quando essa configuração é utilizada, nenhuma agregação para o cubo pode incluir esse atributo.  
  
 `Unrestricted`  
 Selecione para definir a configuração de uso de agregação para o atributo `Unrestricted`. Quando essa configuração é utilizada , não são impostas restrições sobre o designer de agregação; porém, o atributo ainda deve ser avaliado para determinar se é um candidato de agregação valioso.  
  
 **Definir tudo como padrão**  
 Selecione para definir a configuração do uso de agregação de todos os atributos como Padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente de Design de agregação](aggregation-design-wizard-f1-help.md)   
 [Assistentes do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  