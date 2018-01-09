---
title: "Definir a ordenação para uma dimensão | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OrderBy property
- dimensions [Analysis Services], ordering
- Business Intelligence enhancements [Analysis Services], ordering
- dimensions [Analysis Services], Business Intelligence enhancements
- ordering dimensions [Analysis Services]
- OrderByAttributeID property
ms.assetid: c42fbd58-244d-4e0a-b715-6f919cbc3ad9
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 128efeccdeb3b99a580bd4e2f2ba360df874c222
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="bi-wizard---define-the-ordering-for-a-dimension"></a>Assistente de BI - definem a ordenação para uma dimensão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Adicione o aprimoramento a um cubo ou dimensão para especificar como são ordenados os membros de um atributo de ordenação de atributos. Os membros podem ser ordenados pelo nome ou pela chave do atributo ou pelo nome ou pela chave de outro atributo (com base na relação de um atributo). Por padrão, os membros são ordenados por nome. Esse aprimoramento altera as configurações das propriedades **OrderBy** e **OrderByAttributeID** dos atributos de uma dimensão.  
  
 Para adicionar uma ordenação de atributos, use o Assistente de Business Intelligence e selecione a opção **Especificar a Ordenação de Atributos** na página **Escolher Aprimoramento** . Esse assistente orientará você durante as etapas para selecionar a dimensão à qual você deseja aplicar a ordenação de atributos e especificar como ordenar os atributos da dimensão selecionada.  
  
## <a name="selecting-a-dimension"></a>Selecionando uma dimensão  
 Na primeira página **Especificar a Ordenação de Atributos** do assistente, especifique a dimensão à qual você deseja aplicar a ordenação de atributos. O aprimoramento de ordenação de atributos adicionado à dimensão selecionada provocará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
## <a name="specifying-ordering"></a>Especificando a ordenação  
 Na segunda página **Especificar a Ordenação de Atributos** do assistente, especifique como os atributos da dimensão serão ordenados.  
  
 Na coluna **Atributo de Ordenação** , você pode alterar o atributo usado para fazer a ordenação. Se o atributo que você deseja usar para ordenar os membros não estiver na lista, role para baixo na lista e, em seguida, selecione  **\<novo atributo... >** para abrir o **selecionar uma coluna** caixa de diálogo onde você pode Selecione uma coluna em uma tabela de dimensão. Com a seleção de uma coluna pela caixa de diálogo **Selecionar uma Coluna** , é criado um atributo adicional que será usado para ordenar os membros de um atributo.  
  
 Na coluna **Critérios** , você pode selecionar ordenar os membros do atributo por **Chave** ou **Nome**.  
  
  
