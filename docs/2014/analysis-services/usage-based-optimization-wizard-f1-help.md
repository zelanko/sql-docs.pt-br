---
title: Ajuda F1 do assistente de otimização com base no uso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.f1
helpviewer_keywords:
- Usage-Based Optimization Wizard
ms.assetid: e5f5a938-ae7c-4f4e-9416-a7f94ac82763
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5e94818245ba1e87d90f87539ae07e9531e5450
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065567"
---
# <a name="usage-based-optimization-wizard-f1-help"></a>Ajuda F1 do Assistente de Otimização com Base no Uso
  O Assistente de Otimização com Base no Uso tem saída semelhante ao Assistente de Design de Agregação e é usado para criar agregações para uma partição. No entanto o Assistente de Otimização com Base no Uso cria agregações com base em padrões específicos de uso de consultas registradas no log de consultas para uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . As agregações fornecem melhorias de desempenho [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ao permitir que o recupere totais previamente calculados diretamente do armazenamento de cubo em vez de ter que recalcular os dados de uma fonte de dados subjacente para cada consulta.  
  
 Para abrir o assistente de otimização com base no uso [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]de dentro do, abra o designer [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de cubo para um projeto do e clique na guia **agregações** . Clique no botão de **otimização baseado em uso** na barra de ferramentas.  
  
 Para abrir o Assistente de Otimização com Base no Uso de dentro do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], conecte-se a um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e abra a pasta **Cubos** . Selecione um cubo, abra a pasta **Grupos de Medidas** e expanda o grupo de medidas que você deseja modificar. Clique com o botão direito do mouse na pasta **Partições** e selecione **Otimização com Base no Uso**.  
  
 Para projetar essas agregações, você pode usar o Assistente de Design de Agregação. Este assistente fornece instruções para as seguintes etapas:  
  
-   Selecionar configurações padrão ou personalizadas para as opções de armazenamento e cache de uma partição, grupo de medidas ou cubo.  
  
-   Fornecer contagens estimadas ou reais para objetos referenciados pela partição, grupo de medidas ou cubo.  
  
-   Especificar opções e limites de agregação para otimizar o desempenho do armazenamento e de consultas fornecido por agregações projetadas.  
  
-   Salvar e opcionalmente processar a partição, grupo de medidas ou cubo para gerar as agregações definidas.  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece o Assistente de Design de Agregação para criação de agregações com base em análise estatística da estrutura da partição para fornecer um design de agregação que pode ser limitado pelo tamanho do armazenamento ou ganho estimado de desempenho. É possível usar o Assistente de Design de Agregação para melhorar o desempenho geral de uma partição, mas o design de agregação não se destina a necessidades específicas de seus usuários empresariais. O Assistente de Otimização com Base no Uso pode fornecer um design de agregação destinado a essas necessidades específicas, mas o assistente poderá fazer isso apenas se o log de consultas da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] contiver informações suficientes para construir essas consultas.  
  
 Normalmente, os dois assistentes são usados em conjunto para melhorar o desempenho na implantação e com o passar do tempo. O Assistente de Design de Agregação deve ser usado primeiro quando a partição (ou o cubo ou o grupo de medidas que contém a partição) é implantado inicialmente para fornecer um benefício geral de desempenho. Após um período de tempo de registro de consultas de usuários empresariais da partição no log de consultas, você poderá usar o Assistente de Otimização com Base no Uso para focalizar ainda mais o design de agregação para atender melhor aos requisitos de desempenho e de consultas dos usuários empresariais.  
  
> [!NOTE]  
>  Para obter informações sobre como configurar o log de consultas, consulte [Configurando o log de consultas do Analysis Services](instances/log-operations-in-analysis-services.md?view=sql-server-2014#bkmk_querylog).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Selecione partições para modificar &#40;assistente de otimização com base no uso&#41;](select-partitions-to-modify-usage-based-optimization-wizard.md)  
  
-   [Especificar critérios de consulta &#40;assistente de otimização com base no uso&#41;](specify-query-criteria-usage-based-optimization-wizard.md)  
  
-   [Examine as consultas que serão otimizadas &#40;assistente de otimização com base no uso&#41;](review-the-queries-that-will-be-optimized-usage-based-optimization-wizard.md)  
  
-   [Examine o uso de agregação &#40;assistente de otimização com base no uso&#41;](review-aggregation-usage-usage-based-optimiation-wizard.md)  
  
-   [Especificar contagens de objetos &#40;assistente de otimização com base no uso&#41;](specify-object-counts-usage-based-optimization-wizard.md)  
  
-   [Definir opções de agregação &#40;assistente de otimização com base no uso&#41;](set-aggregation-options-usage-based-optimization-wizard.md)  
  
-   [Concluindo o assistente &#40;assistente de otimização com base no uso&#41;](completing-the-wizard-usage-based-optimization-wizard.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Agregações e designs de agregação](multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [Cubos em modelos multidimensionais](multidimensional-models/cubes-in-multidimensional-models.md)   
 [Ajuda F1 do assistente de design de agregação](aggregation-design-wizard-f1-help.md)   
 [Analysis Services assistentes &#40;dados multidimensionais&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
