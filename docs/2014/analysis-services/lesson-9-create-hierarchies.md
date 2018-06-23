---
title: 'Lição 10: Criar hierarquias | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: ea741676f07020291c2aa94d130c2f595a50f323
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006231"
---
# <a name="lesson-10-create-hierarchies"></a>Lição 10: Criar hierarquias
  Nesta lição, você criará hierarquias. Hierarquias são grupos de colunas organizados em níveis; por exemplo, uma hierarquia Geografia poderia ter subníveis para País, Estado, Município e Cidade. As hierarquias podem aparecer separadas de outras colunas em uma lista de campo de aplicativo cliente de relatório, tornando mais fácil para os usuários clientes navegarem e incluírem itens em um relatório. Para saber mais, consulte [Hierarquias &#40;SSAS Tabular&#41;](tabular-models/hierarchies-ssas-tabular.md).  
  
 Para criar hierarquias, você usará o designer de modelos na *Exibição de Diagrama*. Não há suporte para a criação e o gerenciamento de hierarquias no designer de modelos na Exibição de Dados.  
  
 Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de realizar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 9: Criar perspectivas](lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Criar hierarquias  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>Para criar uma hierarquia Categoria na tabela Produto  
  
1.  No designer de modelo, clique no `Model` menu e, em seguida, aponte para **exibição do modelo de**e, em seguida, clique em **exibição de diagrama**.  
  
    > [!TIP]  
    >  Use os controles do Minimapa no lado superior direito do designer de modelos para alterar o modo de exibição dos objetos em Exibição de Diagrama. Se você reposicionar objetos na Exibição de Diagrama, essa exibição será retida quando você salvar o projeto.  
  
2.  No designer de modelo, clique com botão direito do `Product` de tabela e, em seguida, clique em **criar hierarquia**. A nova hierarquia aparece na parte inferior da janela de tabela.  
  
3.  O nome da hierarquia, renomeie a hierarquia digitando `Category`, e pressione ENTER.  
  
4.  No `Product` da tabela, clique no **Product Category Name** coluna, em seguida, arraste-o para o `Category` hierarquia e solte sobre a `Category` nome.  
  
5.  No `Category` hierarquia, com o botão direito a **Product Category Name** coluna, em seguida, clique em **Renomear**e, em seguida, digite `Category`.  
  
    > [!NOTE]  
    >  A renomeação de uma coluna em uma hierarquia não renomeia essa coluna na tabela. Uma coluna em uma hierarquia é apenas uma representação da coluna na tabela.  
  
6.  No `Product` da tabela, clique o **nome da subcategoria do produto** coluna, no menu de contexto, aponte para **adicionar à hierarquia**e, em seguida, clique em `Category`.  
  
7.  Renomear **nome da subcategoria do produto** para `Subcategory`.  
  
8.  Usando clicar e arrastar ou usando o **adicionar à hierarquia** comando no menu de contexto, adicione o **nome do modelo** e **nome do produto** colunas (em ordem) e colocá-los abaixo de **Nome da subcategoria do produto** coluna. Renomeie as colunas `Model` e `Product`, respectivamente.  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>Para criar hierarquias na tabela Data  
  
1.  No designer de modelos, clique com o botão direito do mouse na tabela **Data** e clique em **Criar Hierarquia**.  
  
2.  Renomeie a hierarquia como **Calendário**.  
  
3.  Adicione as seguintes colunas, na ordem, e renomeie-as:  
  
    |coluna|Renomear para:|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  Na tabela **Date** , repita as etapas acima, criando a hierarquia **Fiscal** , incluindo as seguintes colunas:  
  
    |coluna|Renomear para:|  
    |------------|----------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  Por fim, na tabela **Date** , repita as etapas acima, criando a hierarquia **Calendário de Produção** , incluindo as seguintes colunas:  
  
    |coluna|Renomear para:|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|Week|  
    |Day Of Week|Day|  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 11: Criar partições](lesson-10-create-partitions.md).  
  
  