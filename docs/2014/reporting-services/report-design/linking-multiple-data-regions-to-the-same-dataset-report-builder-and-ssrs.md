---
title: Vinculando várias regiões de dados ao mesmo conjunto de dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 90c94a91-8fb2-42cb-b998-563691f30d2d
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 11b4552c73c07f40e40c900aeb29bf738c554dc5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118053"
---
# <a name="linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs"></a>Vinculando várias regiões de dados ao mesmo conjunto de dados (Construtor de Relatórios e SSRS)
  É possível adicionar várias regiões de dados a um relatório para fornecer exibições diferentes do mesmo conjunto de dados de relatório. Por exemplo, você pode desejar exibir dados em uma tabela e também exibi-los visualmente em um gráfico. Para isso, você deve usar expressões e escopos idênticos para as expressões de filtro, de classificação e de grupo apropriadas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Para usar um gráfico e uma tabela ou matriz para exibir os mesmos dados, é útil entender as similaridades entre uma tabela e gráficos de forma e gráficos de matriz e área, de barras e de colunas. Uma tabela com um único grupo de linhas pode ser exibida facilmente como um gráfico de pizza. Conforme adiciona vários grupos de linhas, você pode escolher tipos diferentes de gráficos para exibir melhor os grupos aninhados. A adição de grupos de linhas aninhados a um gráfico de pizza aumenta o número de fatias na pizza. Você deve decidir se o número de instâncias de grupo do grupo pai e do grupo filho combinadas é muito grande para ser exibido em um único gráfico de pizza. Para vários valores de grupo que são exibidos como fatias pequenas de um gráfico de pizza, é possível definir uma propriedade para que todos os valores abaixo de um determinado limite sejam exibidos como uma fatia da pizza. Para obter mais informações, consulte [Coletar fatias pequenas em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md).  
  
 Uma tabela com vários grupos de linhas pode ser mostrada como um gráfico de colunas com vários grupos de categorias. Para obter mais informações, consulte [Exibir os mesmos dados em uma matriz e um gráfico &#40;Construtor de Relatórios&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md). Para obter um exemplo de uma tabela ou gráfico que representa diferentes exibições do mesmo conjunto de dados de relatório, consulte o relatório Vendas de Linha de Produtos em Exemplos de relatórios da AdventureWorks. Como a tabela e o gráfico estão vinculados ao mesmo conjunto de dados neste relatório, quando você clica no botão de classificação interativa para Nome do Funcionário na classificação da tabela Funcionários Principais, o gráfico Funcionários Principais mostra a nova ordem de classificação automaticamente. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][(Relatórios de exemplo do Construtor de relatórios e Designer de relatórios) do](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
 Uma matriz com vários grupos de linhas e de colunas pode ser melhor exibida usando um gráfico de área, de barras ou de colunas com os grupos de categorias e de séries. Use as mesmas expressões de grupo para grupos de colunas nos grupos de matriz e de categorias no gráfico e as mesmas expressões para grupos de linhas nos grupos de matriz e de séries no gráfico. Lembre-se que o número de instâncias de grupo afeta a legibilidade do gráfico. É possível definir grupos baseados em valores de intervalo para reduzir o número de instâncias de grupo em um relatório. Para obter mais informações, consulte [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Regiões de dados aninhadas &#40;SSRS e construtor de relatórios&#41;](nested-data-regions-report-builder-and-ssrs.md)  
  
  