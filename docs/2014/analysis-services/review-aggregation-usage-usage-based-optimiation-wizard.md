---
title: Revise o uso de agregação (Assistente de otimização baseada em uso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.reviewaggregationusage.f1
ms.assetid: 49ce2094-c4dc-4e46-8cef-c17c5db084ca
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 76140fbc19eaa8beae41c1196143a326dc5c6414
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235676"
---
# <a name="review-aggregation-usage-usage-based-optimiation-wizard"></a>Verificar Uso de Agregação (Assistente de Otimização com Base no Uso)
  Use a página **Revisar Uso de Agregação** para efetuar configurações do uso de agregação.  
  
## <a name="options"></a>Opções  
 **Default**  
 Selecione para definir a configuração do uso de agregação do atributo como Padrão. Quando essa configuração é utilizada, o designer aplica uma regra padrão com base no tipo de atributo e dimensão.  
  
 **Full (cheio)**  
 Selecione para definir a configuração do uso de agregação do atributo como Completo. Quando essa configuração é utilizada, cada agregação para o cubo deve incluir esse atributo ou um atributo relacionado inferior na cadeia de atributos. A configuração do uso de agregação Completo deverá ser evitada quando um atributo contiver muitos membros. Se for especificada para vários atributos ou atributos que têm muitos membros, essa configuração poderá impedir a criação de agregações por causa do seu tamanho excessivo.  
  
 **Nenhuma**  
 Selecione para definir a configuração do uso de agregação do atributo como Nenhum. Quando essa configuração é utilizada, nenhuma agregação para o cubo pode incluir esse atributo.  
  
 **Sem restrições**  
 Selecione para definir a configuração do uso de agregação do atributo como Irrestrito. Quando essa configuração é utilizada, nenhuma restrição é colocada no designer de agregação. O atributo, porém, ainda deverá ser avaliado para determinar se é um candidato de agregação valioso.  
  
 **Definir tudo como padrão**  
 Selecione para definir a configuração do uso de agregação de todos os atributos como Padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente de Design de agregação](aggregation-design-wizard-f1-help.md)   
 [Assistentes do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
