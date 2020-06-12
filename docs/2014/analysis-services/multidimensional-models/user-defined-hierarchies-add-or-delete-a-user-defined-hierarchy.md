---
title: Adicionar ou excluir uma hierarquia definida pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], adding
- removing hierarchies
- adding hierarchies
- deleting hierarchies
- hierarchies [Analysis Services], removing
ms.assetid: 953818b4-9543-4c01-bb20-1d45ec6dfb91
author: minewiskan
ms.author: owend
ms.openlocfilehash: 50086ef38d9bd54a4088e9cf647a53553694a09d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84535748"
---
# <a name="add-or-delete-a-user-defined-hierarchy"></a>Adicionar ou excluir uma hierarquia definida pelo usuário
  Você adiciona ou remove uma hierarquia definida pelo usuário de uma dimensão na guia **Estrutura da Dimensão** no Designer de Dimensão em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando você adicionar uma hierarquia definida pelo usuário, ela não ficará disponível aos usuários até que seja instanciada em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e a dimensão seja processada. Para obter mais informações, consulte [bancos de dados de modelo multidimensional &#40;SSAS&#41;](multidimensional-model-databases-ssas.md) e [processamento de objeto de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>Para adicionar uma hierarquia definida pelo usuário em uma dimensão  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto apropriado do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e abra a dimensão com a qual você quer trabalhar.  
  
     A dimensão será aberta no Designer de Dimensão na guia **Estrutura da Dimensão** .  
  
2.  No painel **Atributos** , arraste um atributo que você quer usar na hierarquia definida pelo usuário para o painel **Hierarquias** .  
  
3.  Arraste mais atributos para formar níveis na hierarquia definida pelo usuário.  
  
     A ordem na qual os atributos são listados na hierarquia é importante. Por exemplo, em uma hierarquia de tempo, os anos devem parecer mais acima na lista de hierarquia do que os dias.  
  
4.  Se desejar, reorganize os níveis na hierarquia definida pelo usuário arrastando-os para as posições corretas.  
  
5.  Se desejar, modifique as propriedades da hierarquia definida pelo usuário ou seus níveis.  
  
     Por exemplo, convém especificar um nome para a hierarquia definida pelo usuário, renomear um ou mais de seus níveis e definir um nome personalizado para o Todo o nível. Para obter mais informações, consulte [Propriedades de hierarquia de usuário](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)e propriedades de [nível &#91;paved sobre&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md).  
  
    > [!NOTE]  
    >  Por padrão, uma hierarquia definida pelo usuário é somente um caminho que permite que os usuários façam busca detalhada para obter informações. Porém, se houver relações entre níveis, você pode aumentar o desempenho da consulta configurando relações de atributo entre níveis. Para obter mais informações, consulte [Relações de atributo](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) e [Definir relações de atributo](attribute-relationships-define.md).  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>Para remover uma hierarquia definida pelo usuário de uma dimensão  
  
-   Na guia **Estrutura da Dimensão** , clique na hierarquia definida pelo usuário que deseja remover do painel **Hierarquias** . Na barra de ferramentas, clique em **Excluir**.  
  
     - ou –  
  
-   Clique com o botão direito do mouse na hierarquia definida pelo usuário que você quer remover do painel **Hierarquias** e clique em **Excluir**.  
  
     - ou –  
  
-   Arraste a hierarquia definida pelo usuário para fora da superfície de design.  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquias de usuário](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Criar hierarquias definidas pelo usuário](user-defined-hierarchies-create.md)  
  
  
