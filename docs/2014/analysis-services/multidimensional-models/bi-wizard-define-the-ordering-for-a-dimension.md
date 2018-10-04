---
title: Definir a ordenação para uma dimensão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OrderBy property
- dimensions [Analysis Services], ordering
- Business Intelligence enhancements [Analysis Services], ordering
- dimensions [Analysis Services], Business Intelligence enhancements
- ordering dimensions [Analysis Services]
- OrderByAttributeID property
ms.assetid: c42fbd58-244d-4e0a-b715-6f919cbc3ad9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 916663a7d667187acc6b881ec4ac3c68d406c987
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189796"
---
# <a name="define-the-ordering-for-a-dimension"></a>Definir a ordenação para uma dimensão
  Adicione o aprimoramento de ordenação de atributos a um cubo ou dimensão para especificar como os membros de um atributo são ordenados. Os membros podem ser ordenados pelo nome ou pela chave do atributo ou pelo nome ou pela chave de outro atributo (com base na relação de um atributo). Por padrão, os membros são ordenados por nome. Esse aprimoramento altera as `OrderBy` e `OrderByAttributeID` configurações de propriedade para atributos em uma dimensão.  
  
 Para adicionar uma ordenação de atributos, use o Assistente de Business Intelligence e selecione a opção **Especificar a Ordenação de Atributos** na página **Escolher Aprimoramento** . Esse assistente orientará você durante as etapas para selecionar a dimensão à qual você deseja aplicar a ordenação de atributos e especificar como ordenar os atributos da dimensão selecionada.  
  
## <a name="selecting-a-dimension"></a>Selecionando uma dimensão  
 Na primeira página **Especificar a Ordenação de Atributos** do assistente, especifique a dimensão à qual você deseja aplicar a ordenação de atributos. O aprimoramento de ordenação de atributos adicionado à dimensão selecionada provocará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
## <a name="specifying-ordering"></a>Especificando a ordenação  
 Na segunda página **Especificar a Ordenação de Atributos** do assistente, especifique como os atributos da dimensão serão ordenados.  
  
 Na coluna **Atributo de Ordenação** , você pode alterar o atributo usado para fazer a ordenação. Se o atributo que você deseja usar para ordenar os membros não estiver na lista, role para baixo na lista e, em seguida, selecione  **\<novo atributo... >** para abrir o **selecionar uma coluna** caixa de diálogo, no qual você pode Selecione uma coluna em uma tabela de dimensão. Com a seleção de uma coluna pela caixa de diálogo **Selecionar uma Coluna** , é criado um atributo adicional que será usado para ordenar os membros de um atributo.  
  
 Na coluna **Critérios** , você pode selecionar ordenar os membros do atributo por **Chave** ou **Nome**.  
  
  
