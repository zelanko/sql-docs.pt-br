---
title: Examinar o uso de agregação (Assistente de design de agregação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.aggregationdesignwizard.reviewusage.f1
ms.assetid: 107ee872-3df2-4931-b56c-af11e38f6745
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f52ec05ddadc6bb23968f6b5f8ee7fda9adc65a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070216"
---
# <a name="review-aggregation-usage-aggregation-design-wizard"></a>Revisar Uso de Agregação (Assistente de Design de Agregação)
  Use a página **Revisar Uso de Agregação** para efetuar configurações do uso de agregação.  
  
## <a name="options"></a>Opções  
 **Default**  
 Selecione para definir a configuração do uso de agregação do atributo como Padrão. Quando essa configuração é utilizada, o designer aplica uma regra padrão com base no tipo de atributo e dimensão.  
  
 `Full`  
 Selecione para definir a configuração de uso de agregação para o atributo como `Full`. Quando essa configuração é utilizada, cada agregação para o cubo deve incluir esse atributo ou um atributo relacionado inferior na cadeia de atributos. A configuração de uso de agregação `Full` deverá ser evitada quando um atributo contiver muitos membros. Se for especificada para vários atributos ou atributos que têm muitos membros, essa configuração poderá impedir a criação de agregações por causa do seu tamanho excessivo.  
  
 **Nenhuma**  
 Selecione para definir a configuração do uso de agregação do atributo como Nenhum. Quando essa configuração é utilizada, nenhuma agregação para o cubo pode incluir esse atributo.  
  
 `Unrestricted`  
 Selecione para definir a configuração de uso de agregação para o atributo como `Unrestricted`. Quando essa configuração é utilizada , não são impostas restrições sobre o designer de agregação; porém, o atributo ainda deve ser avaliado para determinar se é um candidato de agregação valioso.  
  
 **Definir Tudo como Padrão**  
 Selecione para definir a configuração do uso de agregação de todos os atributos como Padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente de design de agregação](aggregation-design-wizard-f1-help.md)   
 [Analysis Services assistentes &#40;dados multidimensionais&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
