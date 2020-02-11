---
title: Habilitar detalhamento para um modelo de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- drillthrough [Analysis Services]
ms.assetid: 4fa44f60-ef9a-4b59-98c0-c0baf1195c8e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06ce3967bf9258e9b8f6cd4a28cb28a29a1e0588
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084538"
---
# <a name="enable-drillthrough-for-a-mining-model"></a>Habilitar o detalhamento para um modelo de mineração
  Se você habilitou o detalhamento para um modelo de mineração, quando você procurar o modelo, poderá recuperar informações detalhadas sobre os casos usados para criar o modelo. Para exibir essas informações, você deve ter as permissões necessárias e a estrutura já deve ter sido processada.  
  
 **Permissões** do Para que um usuário faça drill-through para dados de modelo ou dados de estrutura, o usuário deve ser membro de uma função que tenha permissões [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) no modelo de mineração ou na estrutura de mineração. As permissões de detalhamento são definidas separadamente na estrutura e no modelo.  
  
-   As permissões de detalhamento no modelo lhe permitem detalhar do modelo, mesmo que você não tenha permissões na estrutura.  
  
-   As permissões para detalhamento na estrutura fornecem a capacidade adicional de incluir colunas de estrutura em consultas de detalhamento do modelo, usando a função [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx). Você também pode consultar os casos de treinamento e teste na estrutura usando a marca SELECT... DA \<estrutura>. Sintaxe CASEs.  
  
 **Cache de casos de treinamento** O detalhamento funciona recuperando informações sobre os casos de treinamento na estrutura de mineração. Essas informações são armazenadas em cache quando a estrutura é processada. Assim, se você optar por limpar todos os dados em cache alterando a propriedade <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> para `ClearAfterProcessing`, o detalhamento não funcionará.  
  
> [!NOTE]  
>  Se os casos de treinamento não tiverem sido armazenados em cache, você deverá alterar a propriedade <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> para **KeepTrainingCases** e processar o modelo novamente, antes de exibir os dados do caso.  
  
 Para obter mais informações, consulte [Drillthrough Queries &#40;Data Mining&#41;](drillthrough-queries-data-mining.md).  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>Como habilitar o detalhamento em um modelo de mineração  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], na guia **Modelos de Mineração** do Designer de Mineração de Dados, clique com o botão direito do mouse no nome do modelo de mineração no qual você deseja habilitar o detalhamento e selecione **Propriedades**.  
  
2.  Nas janelas **Propriedades** , clique em **AllowDrillthrough**e selecione **True**.  
  
3.  Na guia **Modelos de Mineração** , clique com o botão direito do mouse no modelo e selecione **Modelo de Processo**.  
  
### <a name="to-enable-caching-for-a-mining-structure"></a>Para habilitar o cache para uma estrutura de mineração  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], na guia **Estrutura de Mineração** do Designer de Mineração de Dados, clique com o botão direito do mouse no nome da estrutura de mineração.  
  
2.  Abra a janela **Propriedades** .  
  
3.  Na janela **Propriedades** , localize a propriedade **CacheMode** e selecione **KeepTrainingCases** na lista.  
  
4.  No menu **Banco de Dados** , selecione **Processo**.  
  
## <a name="see-also"></a>Consulte Também  
 [Consultas de detalhamento &#40;mineração de dados&#41;](drillthrough-queries-data-mining.md)  
  
  
