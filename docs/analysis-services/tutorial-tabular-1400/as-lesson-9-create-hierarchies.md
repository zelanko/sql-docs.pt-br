---
title: 'Lição tutorial do Analysis Services 9: criar hierarquias | Microsoft Docs'
description: ''
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 95953da3ff2fc71ac39db75daeea6dacdc0854f5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-hierarchies"></a>Criar hierarquias

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você deve criar hierarquias. Hierarquias são grupos de colunas organizados em níveis. Por exemplo, uma hierarquia de Geografia pode ter subníveis para país, estado, município e cidade. As hierarquias podem aparecer separadas de outras colunas em uma lista de campo de aplicativo cliente de relatório, tornando mais fácil para os usuários clientes navegarem e incluírem itens em um relatório. Para obter mais informações, consulte [hierarquias](../tabular-models/hierarchies-ssas-tabular.md)
  
Para criar hierarquias, use o designer de modelo do *exibição de diagrama*. Não há suporte para criar e gerenciar hierarquias na exibição de dados.  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 8: criar perspectivas](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Criar hierarquias  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>Para criar uma hierarquia de categoria na tabela DimProduct  
  
1.  No designer de modelo (exibição de diagrama), clique com botão direito do **DimProduct** tabela > **criar hierarquia**. A nova hierarquia aparece na parte inferior da janela de tabela. Renomeie a hierarquia **categoria**.  
  
2.  Clique e arraste o **ProductCategoryName** coluna para o novo **categoria** hierarquia.  
  
3.  No **categoria** hierarquia, clique com botão direito **ProductCategoryName** > **Renomear**e, em seguida, digite **categoria**.  
  
    > [!NOTE]  
    > A renomeação de uma coluna em uma hierarquia não renomeia essa coluna na tabela. Uma coluna em uma hierarquia é apenas uma representação da coluna na tabela.  
  
4.  Clique e arraste o **ProductSubcategoryName** coluna para o **categoria** hierarquia. Renomeie- **subcategoria**. 
  
5.  Clique com botão direito do **ModelName** coluna > **adicionar à hierarquia**e, em seguida, selecione **categoria**. Renomeie- **modelo**.

6.  Finalmente, adicione **EnglishProductName** à hierarquia de categoria. Renomeie- **produto**.  

    ![categoria como lesson9](../tutorial-tabular-1400/media/as-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>Para criar hierarquias na tabela DimDate  
  
1.  No **DimDate** de tabela, crie uma hierarquia chamada **calendário**.  
  
3.  Adicione a seguintes colunas na ordem:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  No **DimDate** de tabela, crie um **Fiscal** hierarquia. Inclua a seguintes colunas na ordem:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Por fim, no **DimDate** de tabela, crie um **ProductionCalendar** hierarquia. Inclua a seguintes colunas na ordem:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>O que vem a seguir?

[Lição 10: Criar partições](../tutorial-tabular-1400/as-lesson-10-create-partitions.md). 
  
  
