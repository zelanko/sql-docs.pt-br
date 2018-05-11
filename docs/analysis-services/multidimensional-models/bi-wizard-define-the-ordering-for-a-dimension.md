---
title: Definir a ordenação para uma dimensão | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2306e5d8c7414967e82c79e89449930c389cb4ba
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="bi-wizard---define-the-ordering-for-a-dimension"></a>Assistente de BI - definem a ordenação para uma dimensão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Adicione o aprimoramento de ordenação de atributos a um cubo ou dimensão para especificar como os membros de um atributo são ordenados. Os membros podem ser ordenados pelo nome ou pela chave do atributo ou pelo nome ou pela chave de outro atributo (com base na relação de um atributo). Por padrão, os membros são ordenados por nome. Esse aprimoramento altera as configurações das propriedades **OrderBy** e **OrderByAttributeID** dos atributos de uma dimensão.  
  
 Para adicionar uma ordenação de atributos, use o Assistente de Business Intelligence e selecione a opção **Especificar a Ordenação de Atributos** na página **Escolher Aprimoramento** . Esse assistente orientará você durante as etapas para selecionar a dimensão à qual você deseja aplicar a ordenação de atributos e especificar como ordenar os atributos da dimensão selecionada.  
  
## <a name="selecting-a-dimension"></a>Selecionando uma dimensão  
 Na primeira página **Especificar a Ordenação de Atributos** do assistente, especifique a dimensão à qual você deseja aplicar a ordenação de atributos. O aprimoramento de ordenação de atributos adicionado à dimensão selecionada provocará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
## <a name="specifying-ordering"></a>Especificando a ordenação  
 Na segunda página **Especificar a Ordenação de Atributos** do assistente, especifique como os atributos da dimensão serão ordenados.  
  
 Na coluna **Atributo de Ordenação** , você pode alterar o atributo usado para fazer a ordenação. Se o atributo que você deseja usar para ordenar os membros não estiver na lista, role para baixo na lista e, em seguida, selecione  **\<novo atributo... >** para abrir o **selecionar uma coluna** caixa de diálogo onde você pode Selecione uma coluna em uma tabela de dimensão. Com a seleção de uma coluna pela caixa de diálogo **Selecionar uma Coluna** , é criado um atributo adicional que será usado para ordenar os membros de um atributo.  
  
 Na coluna **Critérios** , você pode selecionar ordenar os membros do atributo por **Chave** ou **Nome**.  
  
  
