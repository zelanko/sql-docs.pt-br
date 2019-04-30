---
title: Adicionar um gráfico a um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a6b595dc-f775-4a53-8554-74a0bf9335ec
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e8776cb0c1f0db206274ff7d766f31ba1c446f51
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206928"
---
# <a name="add-a-chart-to-a-report-report-builder-and-ssrs"></a>Adicionar um gráfico a um relatório (Construtor de Relatórios e SSRS)
  Para resumir dados em um formato visual, use uma região de dados do gráfico. É importante escolher um tipo de gráfico apropriado para o tipo de dados que você está apresentando. Isso influencia a interpretação dos dados quando colocados em formato de gráfico. Para obter mais informações, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
 A maneira mais simples de adicionar uma região de dados de gráfico a seu relatório é executar o Assistente de Novo Gráfico. O assistente oferece gráficos de colunas, linhas, pizza, barras e área. Para esses e outros tipos de gráfico, você pode adicionar um gráfico manualmente.  
  
 Depois de adicionar uma região de dados do gráfico à superfície de design, você pode arrastar campos do conjunto de dados do relatório de dados numéricos e não numéricos para o painel do gráfico Dados do Gráfico. Clique no gráfico para exibir o painel Dados do Gráfico com suas três áreas: Grupos de Séries, Grupos de Categorias e Valores.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-chart-to-a-report-by-using-the-chart-wizard"></a>Para adicionar um gráfico a um relatório usando o Assistente de Gráfico  
  
1.  > [!NOTE]  
    >  O Assistente de Gráfico só está disponível no Construtor de Relatórios.  
  
     Na guia **Inserir** , clique em **Gráfico**e em **Assistente de Gráfico**.  
  
2.  Siga as etapas no Assistente de **Novo** Gráfico.  
  
3.  Na guia **Página Inicial** , clique em **Executar** para visualizar o relatório renderizado.  
  
4.  Na guia **Executar** , clique em **Design** para continuar trabalhando no relatório.  
  
### <a name="to-add-a-chart-to-a-report"></a>Para adicionar um gráfico a um relatório  
  
1.  Crie um relatório e defina um conjunto de dados. Para obter mais informações, consulte [adicionar dados a um relatório &#40;construtor de relatórios e SSRS&#41;](../report-data/report-datasets-ssrs.md).  
  
2.  Na guia **Inserir** , clique em **Gráfico**e em **Inserir Gráfico**.  
  
3.  Clique na superfície de design em que você deseja o canto superior esquerdo do gráfico e arraste até o local do canto inferior direito do gráfico.  
  
     A caixa de diálogo **Selecionar Tipo de Gráfico** é exibida.  
  
4.  Selecione o tipo de gráfico que você deseja adicionar. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Clique no gráfico para exibir o painel **Dados do Gráfico** .  
  
6.  Adicione um ou mais campos à área **Valores** . Essas informações serão plotadas no eixo de valor.  
  
7.  Adicione um campo de agrupamento à área **Grupos de Categorias** . Quando você adiciona esse campo à área **Grupos de Categorias** , um campo de agrupamento é criado automaticamente. Cada grupo representa um ponto de dados da série.  
  
8.  Para resumir os dados por categoria, clique com o botão direito do mouse no campo de dados e clique em **Propriedades da Série**. Na caixa **Categoria** , selecione o campo de categoria na lista suspensa. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
9. Na guia **Página Inicial** , clique em **Executar** para visualizar o relatório renderizado.  
  
10. Na guia **Executar** , clique em **Design** para continuar trabalhando no relatório.  
  
 Em gráficos com eixos, como gráficos de barras e de colunas, o eixo de categoria pode não exibir todos os rótulos de categoria. Para obter mais informações sobre como alterar os rótulos do eixo, consulte [Especificar um intervalo do eixo &#40;Construtor de Relatórios e SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Pontos de dados vazios e nulos em gráficos &#40;Construtor de Relatórios e SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um gráfico de barras ao relatório (Construtor de Relatórios)](https://go.microsoft.com/fwlink/?LinkId=198052)   
 [Tutorial: Adicionar um gráfico de barras a um relatório (Designer de Relatórios)](https://go.microsoft.com/fwlink/?LinkId=198042)   
 [Tutorial: Adicionar um gráfico de pizza ao relatório (Construtor de Relatórios)](https://go.microsoft.com/fwlink/?LinkId=198051)   
 [Tutorial: Adicionar um gráfico de pizza a um relatório (Designer de Relatórios)](https://go.microsoft.com/fwlink/?LinkId=198041)  
  
  
