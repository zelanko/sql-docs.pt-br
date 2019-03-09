---
title: 'Analysis Services lição 9 do tutorial: Criar hierarquias | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: cdb9f571e7bc1630ce12c0d0a4b7f57df8961907
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685413"
---
# <a name="create-hierarchies"></a>Criar hierarquias

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você criará hierarquias. Hierarquias são grupos de colunas organizados em níveis. Por exemplo, uma hierarquia de Geografia pode ter subníveis para país, estado, município e cidade. As hierarquias podem aparecer separadas de outras colunas em uma lista de campo de aplicativo cliente de relatório, tornando mais fácil para os usuários clientes navegarem e incluírem itens em um relatório. Para obter mais informações, consulte [hierarquias](../tabular-models/hierarchies-ssas-tabular.md)
  
Para criar hierarquias, use o designer de modelo do *exibição de diagrama*. Não há suporte para criar e gerenciar hierarquias na exibição de dados.  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 8: Criar perspectivas](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Criar hierarquias  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>Para criar uma hierarquia de categoria na tabela DimProduct  
  
1.  No designer de modelo (exibição de diagrama), clique com botão direito do **DimProduct** tabela > **criar hierarquia**. A nova hierarquia aparece na parte inferior da janela de tabela. Renomeie a hierarquia **categoria**.  
  
2.  Clique e arraste a **ProductCategoryName** coluna para a nova **categoria** hierarquia.  
  
3.  No **categoria** hierarquia, clique com botão direito **ProductCategoryName** > **Renomear**e, em seguida, digite **categoria**.  
  
    > [!NOTE]  
    > A renomeação de uma coluna em uma hierarquia não renomeia essa coluna na tabela. Uma coluna em uma hierarquia é apenas uma representação da coluna na tabela.  
  
4.  Clique e arraste a **ProductSubcategoryName** coluna para o **categoria** hierarquia. Renomeá-lo **subcategoria**. 
  
5.  Clique com botão direito do **ModelName** coluna > **adicionar à hierarquia**e, em seguida, selecione **categoria**. Renomeá-lo **modelo**.

6.  Por fim, adicione **EnglishProductName** à hierarquia de categoria. Renomeá-lo **produto**.  

    ![as-lesson9-category](../tutorial-tabular-1400/media/as-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>Para criar hierarquias na tabela DimDate  
  
1.  No **DimDate** da tabela, crie uma hierarquia chamada **calendário**.  
  
3.  Adicione as seguintes colunas em ordem:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  No **DimDate** da tabela, criar um **Fiscal** hierarquia. Incluem as seguintes colunas em ordem:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Por fim, na **DimDate** da tabela, criar um **ProductionCalendar** hierarquia. Incluem as seguintes colunas em ordem:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>O que vem a seguir?

[Lição 10: Criar partições](../tutorial-tabular-1400/as-lesson-10-create-partitions.md). 
  
  
