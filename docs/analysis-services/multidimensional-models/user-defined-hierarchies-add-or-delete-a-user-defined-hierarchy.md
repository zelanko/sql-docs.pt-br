---
title: Adicionar ou excluir uma hierarquia definida pelo usuário | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 89f92c07753462fc26cb6de7447395f02e571e7a
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578707"
---
# <a name="user-defined-hierarchies---add-or-delete-a-user-defined-hierarchy"></a>Hierarquias definidas pelo usuário – Adicionar ou excluir uma hierarquia definida pelo usuário
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Você adiciona ou remove uma hierarquia definida pelo usuário de uma dimensão na guia **Estrutura da Dimensão** no Designer de Dimensão em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando você adicionar uma hierarquia definida pelo usuário, ela não ficará disponível aos usuários até que seja instanciada em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e a dimensão seja processada. Para obter mais informações, consulte [bancos de dados de modelo Multidimensional](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) e [processando um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>Para adicionar uma hierarquia definida pelo usuário em uma dimensão  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto apropriado do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e abra a dimensão com a qual você quer trabalhar.  
  
     A dimensão será aberta no Designer de Dimensão na guia **Estrutura da Dimensão** .  
  
2.  No painel **Atributos** , arraste um atributo que você quer usar na hierarquia definida pelo usuário para o painel **Hierarquias** .  
  
3.  Arraste mais atributos para formar níveis na hierarquia definida pelo usuário.  
  
     A ordem na qual os atributos são listados na hierarquia é importante. Por exemplo, em uma hierarquia de tempo, os anos devem parecer mais acima na lista de hierarquia do que os dias.  
  
4.  Se desejar, reorganize os níveis na hierarquia definida pelo usuário arrastando-os para as posições corretas.  
  
5.  Se desejar, modifique as propriedades da hierarquia definida pelo usuário ou seus níveis.  
  
     Por exemplo, convém especificar um nome para a hierarquia definida pelo usuário, renomear um ou mais de seus níveis e definir um nome personalizado para o Todo o nível. Para obter mais informações, consulte [Propriedades de hierarquia de usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)e [Propriedades de nível – hierarquias de usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md).  
  
    > [!NOTE]  
    >  Por padrão, uma hierarquia definida pelo usuário é somente um caminho que permite que os usuários façam busca detalhada para obter informações. Porém, se houver relações entre níveis, você pode aumentar o desempenho da consulta configurando relações de atributo entre níveis. Para obter mais informações, consulte [Relações de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) e [Definir relações de atributo](../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>Para remover uma hierarquia definida pelo usuário de uma dimensão  
  
-   Na guia **Estrutura da Dimensão** , clique na hierarquia definida pelo usuário que deseja remover do painel **Hierarquias** . Na barra de ferramentas, clique em **Excluir**.  
  
     - ou –  
  
-   Clique com o botão direito do mouse na hierarquia definida pelo usuário que você quer remover do painel **Hierarquias** e clique em **Excluir**.  
  
     - ou –  
  
-   Arraste a hierarquia definida pelo usuário para fora da superfície de design.  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquias do usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Criar hierarquias definidas pelo usuário](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
  
  
