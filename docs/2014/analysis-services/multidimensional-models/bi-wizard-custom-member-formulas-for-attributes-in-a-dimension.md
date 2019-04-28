---
title: Definir fórmulas de membro personalizado para os atributos de uma dimensão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence enhancements [Analysis Services], custom member formulas
- member formulas [Analysis Services]
- dimensions [Analysis Services], Business Intelligence enhancements
- custom member formulas [Analysis Services]
- CustomRollupColumn property
ms.assetid: c4467b08-ce59-4de7-a2d9-c22e246bdd52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e8850ce0f77b69be681bf99bcdcaeddc5234656c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62700997"
---
# <a name="set-custom-member-formulas-for-attributes-in-a-dimension"></a>Definir fórmulas de membro personalizado para os atributos de uma dimensão
  Adicione um aprimoramento de fórmula de membro personalizado a um cubo ou a uma dimensão para substituir as agregações padrão associadas a um membro da dimensão pelos resultados de uma expressão MDX. (Esse aprimoramento define a propriedade `CustomRollupColumn` em um atributo especificado de uma dimensão.)  
  
> [!NOTE]  
>  Uma fórmula de membro personalizado estará disponível somente para dimensões baseadas em fontes de dados existentes. Para dimensões que foram criadas sem usar uma fonte de dados, execute o Assistente de Geração de Esquema para criar uma exibição da fonte de dados antes de adicionar a fórmula de membro personalizado.  
  
 Para adicionar uma fórmula de membro personalizado, use o Assistente de Business Intelligence e selecione a opção **Criar uma fórmula de membro personalizado** na página **Escolher Aprimoramento** . Esse assistente orientará você durante as etapas para selecionar a dimensão à qual você deseja aplicar a fórmula de membro personalizado e habilitá-la.  
  
## <a name="selecting-a-dimension"></a>Selecionando uma dimensão  
 Na primeira página **Criar uma Fórmula de Membro Personalizado** do assistente, especifique a dimensão à qual você deseja aplicar fórmula de membro personalizado. O aprimoramento de fórmula de membro personalizado adicionado à dimensão selecionada provocará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
## <a name="enabling-a-custom-member-formula"></a>Habilitando uma fórmula de membro personalizado  
 Na segunda página **Criar Fórmula de Membro Personalizado** , associe a coluna de origem que contém a fórmula de membro personalizado a um ou mais atributos da dimensão. Na coluna **Atributo** , marque a caixa de seleção junto ao atributo que você deseja associar à coluna de fórmula de membro personalizado. Depois que você selecionar cada atributo, o assistente exibirá a caixa de diálogo **Selecionar uma Coluna** . Nessa caixa de diálogo, clique na coluna da tabela de dimensão que contém a fórmula. Para alterar a seleção depois de fechar a caixa de diálogo **Selecionar uma Coluna** , clique na célula **Coluna de Origem** que você deseja alterar e, em seguida, clique nas reticências (**...**) para abrir novamente a caixa de diálogo **Selecionar uma Coluna** .  
  
## <a name="see-also"></a>Consulte também  
 [Usar o Assistente de Business Intelligence para aprimorar dimensões](../use-the-business-intelligence-wizard-to-enhance-dimensions.md)  
  
  
