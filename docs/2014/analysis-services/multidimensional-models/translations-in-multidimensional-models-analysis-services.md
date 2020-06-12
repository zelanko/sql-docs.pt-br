---
title: Traduções em modelos multidimensionais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.deletelanguagefirm.f1
ms.assetid: 5521f8ef-b10a-4861-9df7-1e43e0a1fb3f
author: minewiskan
ms.author: owend
ms.openlocfilehash: d01aeb00c7cf96bf993867388d6a2cbbede82d90
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547293"
---
# <a name="translations-in-multidimensional-models"></a>Traduções em modelos multidimensionais
  O suporte a vários idiomas no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é realizado usando traduções. Uma tradução contém um identificador de idioma e associações de propriedades de objetos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que podem ser apresentados em vários idiomas. Por exemplo, você pode definir uma tradução de um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para apresentar a legenda e a descrição desse banco de dados no idioma especificado. Para obter mais informações sobre traduções, consulte [traduções de cubo](../multidimensional-models-olap-logical-cube-objects/cube-translations.md).  
  
## <a name="defining-translations"></a>Definindo traduções  
 Você pode definir traduções no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando o designer apropriado para o objeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que será traduzido. Definir uma tradução cria um objeto `Translation` associado ao objeto apropriado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que tenha os valores literais explícitos especificados, no idioma especificado, para as propriedades do objeto associado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Os seguintes objetos e propriedades no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] podem ter traduções associadas a eles:  
  
|Objeto|Propriedades|Designer|  
|------------|----------------|--------------|  
|Banco de dados|`Caption`, `Description`|[Geral &#40;designer de banco de dados&#41; &#40;Analysis Services-dados multidimensionais&#41;](../general-database-designer-analysis-services-multidimensional-data.md)|  
|Cube|`Caption`, `Description`|[Traduções &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Grupo de medidas|`Caption`|[Traduções &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Medida|`Caption`, `DisplayFolder`|[Traduções &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Dimensão do cubo|`Caption`|[Traduções &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Perspectiva|`Caption`|[Traduções &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|KPI (indicador chave de desempenho)|`Caption`, `Description`, `DisplayFolder`|[Traduções &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Ação|`Caption`|[Traduções &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Conjunto nomeado|`Caption`|[Traduções &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|membro calculado|`Caption`|[Traduções &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Dimensão do banco de dados|`Caption`, `AttributeAllMember`|[Traduções &#40;o designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Atributo|`Caption`, `CaptionColumn` <sup>1</sup>, `AttributeHierarchyDisplayFolder` , `NamingTemplate` ,`MembersWithDataCaption`|[Traduções &#40;o designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Hierarquia|`Caption`, `AllMemberName`|[Traduções &#40;o designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Nível|`Caption`|[Traduções &#40;o designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
  
 <sup>1</sup> a `CaptionColumn` propriedade de um atributo pode ser associada a uma coluna em uma exibição da fonte de dados e pode usar um agrupamento do Windows diferente daquele especificado para a instância, ao contrário de outras traduções.  
  
### <a name="defining-attribute-translations"></a>Definindo traduções de atributo  
 Traduções associadas aos atributos em dimensões de banco de dados são tratadas diferentemente de outras traduções, conforme a seguir:  
  
-   Uma associação de coluna, em vez de um valor de literal explícito, pode ser associada à propriedade `CaptionColumn` para que os nomes dos membros desse atributo possam ser traduzidos.  
  
-   Uma ordenação do Windows diferente da especificada para a instância pode ser usada para que os membros em um atributo possam ser classificados apropriadamente para o idioma especificado na tradução.  
  
 Você pode usar a caixa de diálogo **conversão de dados de atributo** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para definir traduções para atributos em dimensões de banco de dado. Para obter mais informações sobre a caixa de diálogo **conversão de dados de atributo** , consulte caixa de [diálogo conversão de dados de atributo &#40;Analysis Services-&#41;de dados multidimensionais ](../attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="resolving-translations"></a>Resolvendo traduções  
 Se um aplicativo cliente solicita informações em um identificador de idioma específico, a instância no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta resolver dados e metadados para objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o identificador de idioma mais próximo possível. Se o aplicativo cliente não especificar um idioma padrão, especificar o identificador de localidade neutro (0) ou identificador de idioma padrão (1024), o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará o idioma padrão para a instância para retornar dados e metadados para objetos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Se um aplicativo cliente especifica um identificador de idioma diferente do identificador de idioma padrão, a instância itera por meio das traduções disponíveis para todos os objetos disponíveis. Se o identificador de idioma especificado corresponder ao identificador de idioma de uma tradução, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retornará essa tradução. Se uma correspondência não puder ser encontrada, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará usar um dos seguintes métodos para retornar traduções com o identificador de idioma que seja mais próximo do identificador do idioma especificado.  
  
-   Para os seguintes identificadores de idioma, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará usar um identificador de idioma alternativo se a tradução para o identificador de idioma especificado não for definido:  
  
    |Identificador de idioma especificado|Identificador de linguagem alternativo|  
    |-----------------------------------|-----------------------------------|  
    |3076 - Chinês (Hong Kong SAR, PRC)|1028 - Chinês (Taiwan)|  
    |5124 - Chinês (Macau SAR)|1028 - Chinês (Taiwan)|  
    |1028 - Chinês (Taiwan)|Idioma padrão|  
    |4100 – Chinês (Singapura)|2052 - Chinês (PRC)|  
    |2074 - Croata|Idioma padrão|  
    |3098 - Croata (Cirílico)|Idioma padrão|  
  
-   Para todos os outros identificadores de idioma especificados, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] extrai o idioma principal do identificador de idioma especificado e recupera o identificador de idioma indicado pelo Windows como a melhor correspondência para o idioma principal. Se uma tradução para a melhor correspondência de identificador de idioma não puder ser encontrada ou se o identificador de idioma especificado for a melhor correspondência para o idioma principal, então, o idioma padrão será usado.  
  
## <a name="deleting-translation-objects"></a>Excluindo objetos de tradução  
 Você pode clicar com o botão direito em um objeto de tradução na dimensão ou designer de cubo para removê-lo permanentemente. Você não pode restaurar nem reciclar um objeto excluído, portanto, examine a lista de objetos afetados antes de continuar.  
  
## <a name="see-also"></a>Consulte Também  
 [Cenários de globalização para Analysis Services multidimensional](../globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Idiomas e ordenações &#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md)  
  
  
