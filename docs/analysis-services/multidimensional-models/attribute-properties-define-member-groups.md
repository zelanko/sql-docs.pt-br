---
title: Definir grupos de membros | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 15e02bff085d6a53d3573cbb354948b101a67513
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-properties---define-member-groups"></a>Propriedades de atributo - definir grupos de membros
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se um atributo possuir um grande número de membros, será possível agrupá-los em blocos, reduzindo o número de membros que os usuários veem ao navegar pelos dados da hierarquia. Você pode determinar o número de blocos em que os membros são agrupados e definir um esquema de nomeação para os blocos. Para obter mais informações, consulte [Agrupar membros de atributo &#40;Diferenciação&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
 Para agrupar os membros, defina a propriedade **DiscretizationMethod** , acessada pela janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando você cria grupos de membros, suas alterações ficam indisponíveis para os usuários até que a dimensão seja processada. Para obter mais informações, consulte [Processando um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-create-member-groups"></a>Criar grupos de membros  
  
1.  Abra a dimensão com a qual você deseja trabalhar. A guia **Estrutura da Dimensão** é aberta por padrão.  
  
2.  Em **Atributos**, clique com o botão direito do mouse no atributo cujos membros você quer agrupar e clique em **Propriedades**.  
  
3.  Na lista suspensa ao lado de **DiscretizationMethod**, selecione um método para agrupar os membros. Para obter mais informações sobre as configurações de **DiscretizationMethod**, consulte [Agrupar membros de atributo &#40;Discretização&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
  
