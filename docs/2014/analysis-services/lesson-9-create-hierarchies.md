---
title: 'Lição 10: criar hierarquias | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
author: minewiskan
ms.author: owend
ms.openlocfilehash: b6b57669eed30abf010b9d2775950bf0cd6c6e67
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542148"
---
# <a name="lesson-10-create-hierarchies"></a>Lição 10: Criar hierarquias
  Nesta lição, você criará hierarquias. Hierarquias são grupos de colunas organizados em níveis; por exemplo, uma hierarquia Geografia poderia ter subníveis para País, Estado, Município e Cidade. As hierarquias podem aparecer separadas de outras colunas em uma lista de campos de aplicativo cliente de relatório, facilitando sua navegação e inclusão em um relatório pelos usuários do cliente. Para saber mais, consulte [Hierarquias &#40;SSAS Tabular&#41;](tabular-models/hierarchies-ssas-tabular.md).  
  
 Para criar hierarquias, você usará o designer de modelos na *Exibição de Diagrama*. Não há suporte para a criação e o gerenciamento de hierarquias no designer de modelos na Exibição de Dados.  
  
 Tempo estimado para conclusão desta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de realizar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 9: Criar perspectivas](lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Criar hierarquias  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>Para criar uma hierarquia Categoria na tabela Produto  
  
1.  No designer de modelos, clique no `Model` menu, aponte para exibição de **modelo**e clique em exibição de **diagrama**.  
  
    > [!TIP]  
    >  Use os controles do Minimapa no lado superior direito do designer de modelos para alterar o modo de exibição dos objetos em Exibição de Diagrama. Se você reposicionar objetos na Exibição de Diagrama, essa exibição será retida quando você salvar o projeto.  
  
2.  No designer de modelo, clique com o botão direito do mouse na `Product` tabela e clique em **criar hierarquia**. A nova hierarquia aparece na parte inferior da janela de tabela.  
  
3.  No nome da hierarquia, renomeie a hierarquia digitando `Category` e pressione Enter.  
  
4.  Na `Product` tabela, clique na coluna **nome da categoria do produto** , arraste-a para a `Category` hierarquia e, em seguida, solte na parte superior do `Category` nome.  
  
5.  Na `Category` hierarquia, clique com o botão direito do mouse na coluna **nome da categoria do produto** , clique em **renomear**e digite `Category` .  
  
    > [!NOTE]  
    >  A renomeação de uma coluna em uma hierarquia não renomeia essa coluna na tabela. Uma coluna em uma hierarquia é apenas uma representação da coluna na tabela.  
  
6.  Na `Product` tabela, clique com o botão direito do mouse na coluna **nome da subcategoria do produto** e, no menu de contexto, aponte para **Adicionar à hierarquia**e clique em `Category` .  
  
7.  Renomeie o **nome da subcategoria do produto** para `Subcategory` .  
  
8.  Usando clicar e arrastar, ou usando o comando **Adicionar à hierarquia** no menu de contexto, adicione as colunas nome **do modelo** e **nome do produto** (em ordem) e coloque-as abaixo da coluna nome da **subcategoria do produto** . Renomeie essas colunas `Model` e `Product` , respectivamente.  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>Para criar hierarquias na tabela Data  
  
1.  No designer de modelos, clique com o botão direito do mouse na tabela **Data** e clique em **Criar Hierarquia**.  
  
2.  Renomeie a hierarquia como **Calendário**.  
  
3.  Adicione as seguintes colunas, na ordem, e renomeie-as:  
  
    |Coluna|Renomear para:|  
    |------------|----------------|  
    |Calendar Year|Ano|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Dia|  
  
4.  Na tabela **Date** , repita as etapas acima, criando a hierarquia **Fiscal** , incluindo as seguintes colunas:  
  
    |Coluna|Renomear para:|  
    |------------|----------------|  
    |Fiscal Year|Ano|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Dia|  
  
5.  Por fim, na tabela **Date** , repita as etapas acima, criando a hierarquia **Calendário de Produção** , incluindo as seguintes colunas:  
  
    |Coluna|Renomear para:|  
    |------------|----------------|  
    |Calendar Year|Ano|  
    |Week Number Of Year|Semana|  
    |Day Of Week|Dia|  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 11: Criar partições](lesson-10-create-partitions.md).  
  
  
