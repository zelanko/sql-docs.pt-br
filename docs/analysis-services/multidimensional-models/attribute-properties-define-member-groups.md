---
title: Definir grupos de membros | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- member groups [Analysis Services]
- grouping members
- DiscretizationMethod property
ms.assetid: 006cc915-c499-4781-b9a7-01ad31bebf6a
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f527aef051d304dc9cc89a953888c8b41090789d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---define-member-groups"></a>Propriedades de atributo - definir grupos de membros
  Se um atributo possuir um grande número de membros, será possível agrupá-los em blocos, reduzindo o número de membros que os usuários veem ao navegar pelos dados da hierarquia. Você pode determinar o número de blocos em que os membros são agrupados e definir um esquema de nomeação para os blocos. Para obter mais informações, consulte [Agrupar membros de atributo &#40;Diferenciação&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
 Para agrupar os membros, defina a propriedade **DiscretizationMethod** , acessada pela janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando você cria grupos de membros, suas alterações ficam indisponíveis para os usuários até que a dimensão seja processada. Para obter mais informações, consulte [Processando um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-create-member-groups"></a>Criar grupos de membros  
  
1.  Abra a dimensão com a qual você deseja trabalhar. A guia **Estrutura da Dimensão** é aberta por padrão.  
  
2.  Em **Atributos**, clique com o botão direito do mouse no atributo cujos membros você quer agrupar e clique em **Propriedades**.  
  
3.  Na lista suspensa ao lado de **DiscretizationMethod**, selecione um método para agrupar os membros. Para obter mais informações sobre as configurações de **DiscretizationMethod**, consulte [Agrupar membros de atributo &#40;Discretização&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
  

