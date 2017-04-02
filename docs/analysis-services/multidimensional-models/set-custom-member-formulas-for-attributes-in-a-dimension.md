---
title: "Definir f&#243;rmulas de membro personalizado para os atributos em uma dimens&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
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
  - "Melhorias de Business Intelligence [Analysis Services], fórmulas de membro personalizadas"
  - "fórmulas de membro [Analysis Services]"
  - "dimensões [Analysis Services], melhorias de Business Intelligence"
  - "fórmulas de membro personalizado [Analysis Services]"
  - "propriedade CustomRollupColumn"
ms.assetid: c4467b08-ce59-4de7-a2d9-c22e246bdd52
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Definir f&#243;rmulas de membro personalizado para os atributos em uma dimens&#227;o
  Adicione um aprimoramento de fórmula de membro personalizado a um cubo ou a uma dimensão para substituir as agregações padrão associadas a um membro da dimensão pelos resultados de uma expressão MDX. (Esse aprimoramento define a propriedade **CustomRollupColumn** em um atributo especificado de uma dimensão.)  
  
> [!NOTE]  
>  Uma fórmula de membro personalizado estará disponível somente para dimensões baseadas em fontes de dados existentes. Para dimensões que foram criadas sem usar uma fonte de dados, execute o Assistente de Geração de Esquema para criar uma exibição da fonte de dados antes de adicionar a fórmula de membro personalizado.  
  
 Para adicionar uma fórmula de membro personalizado, use o Assistente de Business Intelligence e selecione a opção **Criar uma fórmula de membro personalizado** na página **Escolher Aprimoramento** . Esse assistente orientará você durante as etapas para selecionar a dimensão à qual você deseja aplicar a fórmula de membro personalizado e habilitá-la.  
  
## Selecionando uma dimensão  
 Na primeira página **Criar uma Fórmula de Membro Personalizado** do assistente, especifique a dimensão à qual você deseja aplicar fórmula de membro personalizado. O aprimoramento de fórmula de membro personalizado adicionado à dimensão selecionada provocará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
## Habilitando uma fórmula de membro personalizado  
 Na segunda página **Criar Fórmula de Membro Personalizado** , associe a coluna de origem que contém a fórmula de membro personalizado a um ou mais atributos da dimensão. Na coluna **Atributo** , marque a caixa de seleção junto ao atributo que você deseja associar à coluna de fórmula de membro personalizado. Depois que você selecionar cada atributo, o assistente exibirá a caixa de diálogo **Selecionar uma Coluna** . Nessa caixa de diálogo, clique na coluna da tabela de dimensão que contém a fórmula. Para alterar a seleção depois de fechar a caixa de diálogo **Selecionar uma Coluna**, clique na célula **Coluna de Origem** que você deseja alterar e, em seguida, clique nas reticências (**...**) para abrir novamente a caixa de diálogo **Selecionar uma Coluna**.  
  
## Consulte também  
 [Usar o Assistente de Business Intelligence para aprimorar dimensões](../Topic/Use%20the%20Business%20Intelligence%20Wizard%20to%20Enhance%20Dimensions.md)  
  
  