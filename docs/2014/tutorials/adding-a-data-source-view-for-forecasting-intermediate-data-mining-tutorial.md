---
title: Adicionando dados de um exibição da fonte para a previsão (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2665040a-1291-4064-ba01-f458637dda57
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f60ea2b2a642cf9435ed8366c42e43abb927e426
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034797"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>Adicionando uma exibição da fonte de dados para previsão (Tutorial de mineração de dados intermediário)
  Nesta tarefa, você adiciona uma exibição da fonte de dados que será usada no cenário de previsão. Um modelo de previsão exige que os dados contenham uma coluna que possa ser usada na identificação das etapas de uma série temporal. Se você planeja analisar várias séries de dados, todas elas deverão terminar na mesma data ou período.  
  
### <a name="to-add-a-data-source-view"></a>Para adicionar uma exibição da fonte de dados  
  
1.  No Gerenciador de soluções, clique com botão direito **exibições da fonte de dados**e, em seguida, selecione **nova exibição da fonte de dados**.  
  
2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados** , clique em **Avançar**.  
  
3.  Sobre o **selecionar uma fonte de dados** página, em **fontes de dados relacionais**, selecione o [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] fonte de dados. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se você não tiver essa fonte de dados, você pode encontrar as etapas para criar a fonte de dados na [Tutorial básico de mineração de dados](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
4.  Sobre o **selecionar tabelas e exibições** página, selecione a tabela vTimeSeries (dbo) e, em seguida, clique na seta à direita para adicioná-la à exibição de fonte de dados.  
  
5.  Clique em **Avançar**.  
  
6.  Sobre o **Concluindo o assistente** página, por padrão, a exibição da fonte de dados é denominada [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Altere o nome para **SalesByRegion**e, em seguida, clique em **concluir**.  
  
     Designer de exibição de fonte de dados é aberta e o **SalesByRegion** exibição da fonte de dados é exibida.  
  
## <a name="working-with-the-data-source-view"></a>Trabalhando com a exibição da fonte de dados  
 Depois de criar a exibição da fonte de dados, será possível explorar os dados das seguintes formas:  
  
-   Clique com botão direito na tabela vTimeSeries do designer e selecione **explorar dados** para abrir a tabela selecionada em uma grade.  
  
-   Clique em **opções de amostragem** e, em seguida, usar o **opções de exploração de dados** caixa de diálogo para alterar o método de amostragem. Clique em **Refresh** para carregar dados na tabela usando as novas configurações de opção. Por exemplo, você pode especificar o número de linhas a serem geradas no exemplo, ou escolha as primeiras n linhas.  
  
-   Clique com botão direito na tabela vTimeSeries e selecione **propriedades** para atribuir um novo nome para a tabela. Você também pode selecionar colunas individuais na exibição da fonte de dados e modificar as propriedades de coluna.  
  
-   Clique em qualquer ponto na área de design de exibição da fonte de dados para criar uma nova consulta e atribuir um nome a ela, para criar relações entre tabelas ou para alterar o layout da área de design.  
  
-   Uma tabela com o botão direito e selecione **novo cálculo nomeado** para criar colunas derivadas, inclusive agregações. Você também pode adicionar novas tabelas e exibições da fonte de dados nesta exibição.  
  
 Na próxima tarefa, você irá explorar os dados da série temporal e determinar a melhor coluna a ser usada como o identificador de série temporal. Aprenderá também como tratar lacunas nos dados de série temporal.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Noções básicas sobre os requisitos para uma série de tempo de modelo &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
