---
title: Especificar contagens de objetos (Assistente de otimização com base no uso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 306c7c25-ae24-4852-ab8c-c82f68a4bc1f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a6f4bb5bcf2584cba8265fb175b7581b6b40ce08
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48154056"
---
# <a name="specify-object-counts-usage-based-optimization-wizard"></a>Especificar Contagens de Objetos (Assistente de Otimização com Base no Uso)
  Use a página **Especificar Contagens de Objetos** para calcular a contagem de objetos no cubo automaticamente ou para inserir contagens estimadas manualmente. O Assistente de Otimização com Base no Uso usa a contagem de objetos para estimar requisitos de armazenamento.  
  
## <a name="options"></a>Opções  
 **Objetos Cube**  
 Exibe as dimensões e os atributos do cubo. Somente os atributos que não têm seus `AggregationUsage` propriedade definida como nenhum na **revisar uso de agregação** página do assistente são exibidos, porque esses são os únicos atributos que precisam de contagens especificadas.  
  
 **Contagem estimada**  
 Exibe o número estimado de linhas no grupo de medidas e as contagens de membros de atributo estimadas nas dimensões do banco de dados. Você pode digitar um valor a ser usado como a contagem estimada ou calcular os valores da contagem estimada. Para calcular os valores da contagem, digite 0 no campo e clique em **Contagem**. Os campos que já exibem uma contagem não são atualizados.  
  
 **Contagem de partições**  
 (Opcional) Digite o número estimado de linhas no grupo de medidas e as contagens de membros de atributo estimadas nas partições.  
  
 **Contagem**  
 Calcula e popula novamente os valores na coluna **Contagem estimada** para todos os campos vazios. Os campos que já exibem uma contagem não são atualizados.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente de Design de agregação](aggregation-design-wizard-f1-help.md)   
 [Assistentes do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
