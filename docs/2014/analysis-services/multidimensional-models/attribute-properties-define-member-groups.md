---
title: Definir grupos de membros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- member groups [Analysis Services]
- grouping members
- DiscretizationMethod property
ms.assetid: 006cc915-c499-4781-b9a7-01ad31bebf6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 389439143ddd5f56d565cdebff42a91e241e16fe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219336"
---
# <a name="define-member-groups"></a>Definir grupos de membros
  Se um atributo possuir um grande número de membros, será possível agrupá-los em blocos, reduzindo o número de membros que os usuários veem ao navegar pelos dados da hierarquia. Você pode determinar o número de blocos em que os membros são agrupados e definir um esquema de nomeação para os blocos. Para obter mais informações, consulte [Agrupar membros de atributo &#40;Diferenciação&#41;](attribute-properties-group-attribute-members.md).  
  
 Para agrupar os membros, defina a propriedade **DiscretizationMethod** , acessada pela janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando você cria grupos de membros, suas alterações ficam indisponíveis para os usuários até que a dimensão seja processada. Para obter mais informações, consulte [processamento de objeto de modelo Multidimensional](processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-create-member-groups"></a>Criar grupos de membros  
  
1.  Abra a dimensão com a qual você deseja trabalhar. A guia **Estrutura da Dimensão** é aberta por padrão.  
  
2.  Em **Atributos**, clique com o botão direito do mouse no atributo cujos membros você quer agrupar e clique em **Propriedades**.  
  
3.  Na lista suspensa ao lado de **DiscretizationMethod**, selecione um método para agrupar os membros. Para obter mais informações sobre as configurações de **DiscretizationMethod**, consulte [Agrupar membros de atributo &#40;Discretização&#41;](attribute-properties-group-attribute-members.md).  
  
  
