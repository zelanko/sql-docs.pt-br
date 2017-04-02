---
title: "Adicionar um atributo a uma dimens&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "adicionando atributos"
  - "criação de atributo automática"
  - "atributos [Analysis Services], criando"
  - "atributos [Analysis Services], adicionando"
  - "criação de atributo manual [Analysis Services]"
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Adicionar um atributo a uma dimens&#227;o
  Você pode adicionar um atributo a uma dimensão automática ou manualmente no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para criar um atributo automaticamente, na guia **Estrutura da Dimensão** , do Designer de Dimensão do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione a coluna que você deseja mapear para um atributo e a arraste do painel **Exibição da Fonte de Dados** para o painel **Atributos** . Essa ação criará um atributo mapeado para a coluna e atribuirá a ele o mesmo nome da coluna. Se já houver um atributo com esse nome, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] adicionará um número ordinal como sufixo, começando com "1" para o primeiro nome duplicado.  
  
 Para criar um atributo manualmente, configure o painel **Atributos** para exibição de grade. Na coluna de nome da última linha da grade, clique no item **\<new attribute>**. Digite um nome para o novo atributo. Será criado um atributo que não será mapeado para uma coluna e que manterá as configurações padrão para todas as suas propriedades. É possível definir o mapeamento na janela **Propriedades** do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] configurando a propriedade **KeyColumns** do novo atributo.  
  
 Para obter mais informações, consulte [Definir um novo atributo automaticamente](../../analysis-services/multidimensional-models/define-a-new-attribute-automatically.md), [Definir um novo atributo manualmente](../Topic/Define%20a%20New%20Attribute%20Manually.md), [Associar um atributo a uma coluna de nome](../../analysis-services/multidimensional-models/bind-an-attribute-to-a-name-column.md) e [Modificar a propriedade KeyColumn de um atributo](../../analysis-services/multidimensional-models/modify-the-keycolumn-property-of-an-attribute.md).  
  
## Consulte também  
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  