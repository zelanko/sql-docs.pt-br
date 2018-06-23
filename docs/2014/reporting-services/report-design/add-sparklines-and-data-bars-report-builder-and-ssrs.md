---
title: Adicionar minigráficos e barras de dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0b297c2e-d48b-41b0-aabd-29680cdcdb05
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: e95e9543cb3eb1efdc0f7a1589133f5691a9fd33
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020426"
---
# <a name="add-sparklines-and-data-bars-report-builder-and-ssrs"></a>Adicionar minigráficos e barras de dados (Construtor de Relatórios e SSRS)
  Minigráficos e barras de dados são pequenos gráficos que transmitem muitas informações com poucos detalhes externos. Para obter mais informações sobre eles, consulte [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
 Minigráficos e barras de dados geralmente são colocados nas células em uma tabela ou matriz. Em geral, os minigráficos exibem apenas uma série cada. As barras de dados podem conter um ou mais pontos de dados. Os minigráficos e as barras de dados exibem apenas uma série cada e causam impacto por repetir as informações da série para cada linha na tabela ou matriz.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-sparkline-or-data-bar-to-a-table-or-matrix"></a>Para adicionar um minigráfico ou uma barra de dados a uma tabela ou matriz  
  
1.  Se você ainda não tiver feito isso, crie uma tabela ou matriz com os dados que deseja exibir. Para obter mais informações, consulte [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md) ou [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md).  
  
2.  Insira uma coluna em sua tabela ou matriz. Para obter mais informações, consulte [Inserir ou excluir uma coluna &#40;Construtor de Relatórios e SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  Na guia **Inserir** , clique em **Minigráfico** ou **Barra de Dados**e clique em uma célula na nova coluna.  
  
    > [!NOTE]  
    >  Você não pode colocar minigráficos em um grupo de detalhes em uma tabela. Eles devem ficar em uma célula associada a um grupo.  
  
4.  Na caixa de diálogo **Alterar Tipo de Minigráfico/Barra de Dados** , clique no tipo desejado de minigráfico ou barra de dados e clique em **OK**.  
  
5.  Clique no minigráfico ou na barra de dados.  
  
     O painel **Dados do Gráfico** é aberto.  
  
6.  Na área **Valores** , em **Adicionar Campos** , clique no sinal de adição (**+**) e clique no campo cujos valores você deseja inserir no gráfico.  
  
7.  Na área **Grupos de Categorias** , em **Adicionar Campos** , clique no sinal de adição (**+**) e clique no campo por cujos valores você deseja agrupar.  
  
     Em geral, para minigráficos e barras de dados, você não adicionará um campo à área **Grupo de Séries** porque somente deseja uma série para cada linha.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Alinhar os dados de um gráfico em uma tabela ou matriz &#40;SSRS e construtor de relatórios&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  