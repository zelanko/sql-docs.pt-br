---
title: Configurar atributos de dimensão (Assistente de Business Intelligence) | Microsoft Docs
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
- sql12.asvs.biwizard.acctintelligence.selectattributes.f1
ms.assetid: 3d046e63-bcb1-4ab1-9c37-652463fa68c3
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e9ce0f7535f111d5c9152304a4e27315f73e5087
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36021045"
---
# <a name="configure-dimension-attributes-business-intelligence-wizard"></a>Configurar Atributos de Dimensão (Assistente de Business Intelligence)
  Use a página **Configurar Atributos de Dimensão** para mapear atributos de dimensão para os tipos atributos usados pelo [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para identificar atributos para dimensões de conta.  
  
## <a name="options"></a>Opções  
 **Tipo de dimensão**  
 Exibe o tipo de dimensão selecionado.  
  
> [!NOTE]  
>  Essa opção não está disponível porque o `Type` propriedade da dimensão não pode ser alterada para um valor diferente de *conta* para dimensões de conta.  
  
 **Atributos de dimensão**  
 Exibe os tipos de atributos válidos que podem ser mapeados para os atributos de dimensão existentes na dimensão.  
  
 **Incluir**  
 Selecione uma caixa de seleção para incluir o tipo de atributo correspondente na dimensão.  
  
 **Tipo de atributo**  
 Lista os tipos de atributos que podem ser mapeados para os atributos de dimensão existentes na dimensão.  
  
 **Atributo de dimensão**  
 Selecione o atributo de dimensão que deve ser mapeado para o tipo de atributo correspondente.  
  
 **Definir medidas como semiaditivas com base no tipo de conta**  
 Selecione para alterar cada medida associada a essa dimensão a ser agregada por tipo de conta.  
  
> [!NOTE]  
>  Essa opção não será exibida se o Assistente de Business Intelligence tiver sido iniciado no Designer de Dimensão ou clicando com o botão direito do mouse em uma dimensão no Gerenciador de Soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente do Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Designer de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Designer de dimensão &#40;Analysis Services - dados multidimensionais&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  