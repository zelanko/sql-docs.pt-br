---
title: Definir fórmulas de membro personalizado para os atributos em uma dimensão | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29b4d83956e6963aa7df0b4a1afd11edda6c83c4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="bi-wizard---custom-member-formulas-for-attributes-in-a-dimension"></a>Assistente de BI - fórmulas de membro personalizado para os atributos em uma dimensão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Adicione um aprimoramento de fórmula de membro personalizado a um cubo ou a uma dimensão para substituir as agregações padrão associadas a um membro da dimensão pelos resultados de uma expressão MDX. (Esse aprimoramento define a propriedade **CustomRollupColumn** em um atributo especificado de uma dimensão.)  
  
> [!NOTE]  
>  Uma fórmula de membro personalizado estará disponível somente para dimensões baseadas em fontes de dados existentes. Para dimensões que foram criadas sem usar uma fonte de dados, execute o Assistente de Geração de Esquema para criar uma exibição da fonte de dados antes de adicionar a fórmula de membro personalizado.  
  
 Para adicionar uma fórmula de membro personalizado, use o Assistente de Business Intelligence e selecione a opção **Criar uma fórmula de membro personalizado** na página **Escolher Aprimoramento** . Esse assistente orientará você durante as etapas para selecionar a dimensão à qual você deseja aplicar a fórmula de membro personalizado e habilitá-la.  
  
## <a name="selecting-a-dimension"></a>Selecionando uma dimensão  
 Na primeira página **Criar uma Fórmula de Membro Personalizado** do assistente, especifique a dimensão à qual você deseja aplicar fórmula de membro personalizado. O aprimoramento de fórmula de membro personalizado adicionado à dimensão selecionada provocará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
## <a name="enabling-a-custom-member-formula"></a>Habilitando uma fórmula de membro personalizado  
 Na segunda página **Criar Fórmula de Membro Personalizado** , associe a coluna de origem que contém a fórmula de membro personalizado a um ou mais atributos da dimensão. Na coluna **Atributo** , marque a caixa de seleção junto ao atributo que você deseja associar à coluna de fórmula de membro personalizado. Depois que você selecionar cada atributo, o assistente exibirá a caixa de diálogo **Selecionar uma Coluna** . Nessa caixa de diálogo, clique na coluna da tabela de dimensão que contém a fórmula. Para alterar a seleção depois de fechar a caixa de diálogo **Selecionar uma Coluna** , clique na célula **Coluna de Origem** que você deseja alterar e, em seguida, clique nas reticências (**...**) para abrir novamente a caixa de diálogo **Selecionar uma Coluna** .  
  
## <a name="see-also"></a>Consulte também  
 [Use o Assistente de Business Intelligence para aprimorar dimensões](http://msdn.microsoft.com/library/12d995d1-75ca-4890-bf4b-a2656910b8d0)  
  
  
