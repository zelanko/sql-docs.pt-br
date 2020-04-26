---
title: Adicionando uma exibição da fonte de dados para previsão (tutorial de mineração de dados intermediários) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62823126"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>Adicionando uma exibição da fonte de dados para previsão (Tutorial de mineração de dados intermediário)
  Nesta tarefa, você adiciona uma exibição da fonte de dados que será usada no cenário de previsão. Um modelo de previsão exige que os dados contenham uma coluna que possa ser usada na identificação das etapas de uma série temporal. Se você planeja analisar várias séries de dados, todas elas deverão terminar na mesma data ou período.  
  
### <a name="to-add-a-data-source-view"></a>Para adicionar uma exibição da fonte de dados  
  
1.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **exibições da fonte de dados**e selecione **nova exibição da fonte de dados**.  
  
2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados**, clique em **Próximo**.  
  
3.  Na página **selecionar uma fonte de dados** , em **fontes de dados relacionais**, selecione [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] a fonte de dados. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se você não tiver essa fonte de dados, poderá encontrar as etapas para criar a fonte de dados no [tutorial de mineração de dados básico](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
4.  Na página **selecionar tabelas e exibições** , selecione a tabela, vTimeSeries (dbo) e clique na seta para a direita para adicioná-la à exibição da fonte de dados.  
  
5.  Clique em **Avançar**.  
  
6.  Na página **concluindo o assistente** , por padrão, a exibição da fonte de [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]dados é denominada. Altere o nome para **SalesByRegion**e clique em **concluir**.  
  
     O designer de exibição da fonte de dados é aberto e a exibição da fonte de dados **SalesByRegion** é exibida.  
  
## <a name="working-with-the-data-source-view"></a>Trabalhando com a exibição da fonte de dados  
 Depois de criar a exibição da fonte de dados, será possível explorar os dados das seguintes formas:  
  
-   Clique com o botão direito do mouse na tabela vTimeSeries no designer e selecione **explorar dados** para abrir a tabela selecionada em uma grade.  
  
-   Clique em **Opções de amostragem** e use a caixa de diálogo opções de exploração de **dados** para alterar o método de amostragem. Clique em **Atualizar** para carregar os dados na tabela usando as novas configurações de opção. Por exemplo, você pode especificar o número de linhas a serem geradas no exemplo ou escolher as n linhas principais.  
  
-   Clique com o botão direito do mouse na tabela vTimeSeries e selecione **Propriedades** para atribuir um novo nome à tabela. Você também pode selecionar colunas individuais na exibição da fonte de dados e modificar as propriedades de coluna.  
  
-   Clique em qualquer ponto na área de design de exibição da fonte de dados para criar uma nova consulta e atribuir um nome a ela, para criar relações entre tabelas ou para alterar o layout da área de design.  
  
-   Clique com o botão direito do mouse em uma tabela e selecione **novo cálculo nomeado** para criar colunas derivadas, incluindo agregações. Você também pode adicionar novas tabelas e exibições da fonte de dados nesta exibição.  
  
 Na próxima tarefa, você irá explorar os dados da série temporal e determinar a melhor coluna a ser usada como o identificador de série temporal. Aprenderá também como tratar lacunas nos dados de série temporal.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Noções básicas sobre os requisitos de um modelo de série temporal &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo MTS](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
