---
title: "Adicionar um atributo a uma dimensão | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding attributes
- automatic attribute creation
- attributes [Analysis Services], creating
- attributes [Analysis Services], adding
- manual attribute creation [Analysis Services]
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fd1a1579a81f1728a47b217f06739b722fe226c7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="attribute-properties---add-an--attribute-to-a-dimension"></a>Atributo propriedades - adicionar um atributo a uma dimensão
  Você pode adicionar um atributo a uma dimensão automática ou manualmente no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para criar um atributo automaticamente, na guia **Estrutura da Dimensão** , do Designer de Dimensão do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione a coluna que você deseja mapear para um atributo e a arraste do painel **Exibição da Fonte de Dados** para o painel **Atributos** . Essa ação criará um atributo mapeado para a coluna e atribuirá a ele o mesmo nome da coluna. Se já houver um atributo com esse nome, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] adicionará um número ordinal como sufixo, começando com "1" para o primeiro nome duplicado.  
  
 Para criar um atributo manualmente, configure o painel **Atributos** para exibição de grade. Na coluna Nome da última linha na grade, clique o  **\<novo atributo >** item. Digite um nome para o novo atributo. Será criado um atributo que não será mapeado para uma coluna e que manterá as configurações padrão para todas as suas propriedades. É possível definir o mapeamento na janela **Propriedades** do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] configurando a propriedade **KeyColumns** do novo atributo.  
  
 Para obter mais informações, consulte [Definir um novo atributo automaticamente](../../analysis-services/multidimensional-models/attribute-properties-define-a-new-attribute-automatically.md), [Associar um atributo a uma coluna de nome](../../analysis-services/multidimensional-models/attribute-properties-bind-an-attribute-to-a-name-column.md)e [Modificar a propriedade KeyColumn de um atributo](../../analysis-services/multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
