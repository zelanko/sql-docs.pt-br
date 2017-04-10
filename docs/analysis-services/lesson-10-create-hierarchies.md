---
title: "Li&#231;&#227;o 10: Criar hierarquias | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Li&#231;&#227;o 10: Criar hierarquias
Nesta lição, você criará hierarquias. Hierarquias são grupos de colunas organizados em níveis; por exemplo, uma hierarquia Geografia poderia ter subníveis para País, Estado, Município e Cidade. As hierarquias podem aparecer separadas de outras colunas em uma lista de campo de aplicativo cliente de relatório, tornando mais fácil para os usuários clientes navegarem e incluírem itens em um relatório. Para saber mais, consulte [Hierarquias &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/hierarchies-ssas-tabular.md).  
  
Para criar hierarquias, você usará o designer de modelos na *Exibição de Diagrama*. Não há suporte para a criação e o gerenciamento de hierarquias no designer de modelos na Exibição de Dados.  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de realizar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 9: Criar perspectivas](../Topic/Lesson%209:%20Create%20Perspectives.md).  
  
## Criar hierarquias  
  
#### Para criar uma hierarquia Categoria na tabela Produto  
  
1.  No designer de modelos, clique no menu **Modelo**, aponte para **Exibição de Modelo** e clique em **Exibição de Diagrama**.  
  
  
  
2.  Clique com o botão direito do mouse na tabela **Product** e clique em **Criar Hierarquia**. A nova hierarquia aparece na parte inferior da janela de tabela.  
  
3.  No nome de hierarquia, renomeie a hierarquia digitando **Categoria** e pressione ENTER.  
  
4.  Na tabela **Product**, clique na coluna **Nome da Categoria do Produto**, arraste-a até a hierarquia **Categoria** e solte-a acima de **Categoria**.  
  
5.  Na hierarquia **Categoria**, clique com o botão direito do mouse na coluna **Nome da Categoria do Produto**, clique em **Renomear** e digite **Categoria**.  
  
    > [!NOTE]  
    > A renomeação de uma coluna em uma hierarquia não renomeia essa coluna na tabela. Uma coluna em uma hierarquia é apenas uma representação da coluna na tabela.  
  
6.  Na tabela **Produto**, clique e arraste a coluna **Nome da Subcategoria do Produto** até a hierarquia **Categoria**.  
  
7.  Renomeie **Nome da Subcategoria do Produto** como **Subcategoria**.  
  
8.  Clique e arraste as colunas **Nome do Modelo** e **Nome do Produto** (na ordem) e coloque-as sob a coluna **Nome da Subcategoria do Produto**. Renomeie essas colunas **Modelo** e **Produto**, respectivamente.  
  
#### Para criar hierarquias na tabela Data  
  
1.  No designer de modelos, clique com o botão direito do mouse na tabela **Data** e clique em **Criar Hierarquia**.  
  
2.  Renomeie a hierarquia como **Calendário**.  
  
3.  Adicione as seguintes colunas, na ordem, e renomeie-as:  
  
    |Coluna|Renomear para:|  
    |----------|--------------|  
    |Calendar Year|Ano|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  Na tabela **Date**, repita as etapas acima, criando a hierarquia **Fiscal**, incluindo as seguintes colunas:  
  
    |Coluna|Renomear para:|  
    |----------|--------------|  
    |Fiscal Year|Ano|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  Por fim, na tabela **Date**, repita as etapas acima, criando a hierarquia **Calendário de Produção**, incluindo as seguintes colunas:  
  
    |Coluna|Renomear para:|  
    |----------|--------------|  
    |Calendar Year|Ano|  
    |Week Number Of Year|Week|  
    |Day Of Week|Day|  
  
## Próximas etapas  
Para continuar este tutorial, vá para a próxima lição: [Lição 11: Criar partições](../analysis-services/lesson-11-create-partitions.md).  
  
  
  
