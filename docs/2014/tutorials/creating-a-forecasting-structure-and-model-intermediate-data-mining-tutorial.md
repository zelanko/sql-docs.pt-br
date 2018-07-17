---
title: Criando uma estrutura de previsão e um modelo (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c73081ff9bb72684192ea17d0247b38bc4f7d64e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308826"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>Criando uma estrutura e um modelo de previsão (Tutorial de mineração de dados intermediário)
  Em seguida, você usará o Assistente de Mineração de Dados para criar uma nova estrutura e um novo modelo de mineração baseados na exibição da fonte de dados recém-criada. Nesta tarefa, você especificará que o modelo de mineração deverá usar o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series.  
  
### <a name="to-create-a-forecasting-mining-structure"></a>Para criar uma estrutura de mineração de previsão  
  
1.  No Gerenciador de soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique com botão direito **estruturas de mineração** e selecione **nova estrutura de mineração**.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  No **Selecionar método de definição** página, verifique **de warehouse existente de banco de dados ou dados relacional** está selecionado e, em seguida, clique em **próxima**.  
  
4.  Sobre o **criar a estrutura de mineração de dados** página, em **qual técnica de mineração de dados você deseja usar?**, selecione **Microsoft Time Series**e, em seguida, clique em  **Próxima**.  
  
5.  Sobre o **Selecionar exibição da fonte de dados** página, em **modos de exibição de fonte de dados disponíveis**, selecione **SalesByRegion**.  
  
6.  Clique em **Avançar**.  
  
7.  No **especificar tipos de tabela** página, certifique-se de que a caixa de seleção a **caso** coluna para a tabela vTimeSeries está selecionado e, em seguida, clique em **próxima**.  
  
8.  Sobre o **especificar os dados de treinamento** , marque as caixas de seleção a **chave** coluna para as colunas ModelRegion e ReportingDate.  
  
     ReportingDate deve estar marcada por padrão, já que você especificou essa coluna como a chave primária lógica quando criou a exibição da fonte de dados. Ao adicionar ModelRegion como uma segunda chave, você está dizendo ao algoritmo para criar uma série de tempo separada para cada combinação de modelo e região listada nesse campo.  
  
9. Marque as caixas de seleção de **entrada** e **previsível** colunas para a quantidade, coluna e clique **próxima**.  
  
     Selecionando **previsível**, você indica que você deseja criar previsões sobre os dados nesta coluna. No entanto, como você deseja basear as previsões em dados passados, deverá adicionar também a coluna como uma entrada.  
  
10. Na página **colunas especificar conteúdo e tipo de dados**, examine as seleções.  
  
     A coluna ModelRegion é designada como um **chave** coluna e a coluna ReportingDate é automaticamente designada como um **Key Time** coluna. Só é possível ter um de cada tipo de chave.  
  
11. Clique em **Avançar**.  
  
12. Sobre o **Concluindo o assistente** página, para **nome da estrutura de mineração**, tipo `Forecasting`.  
  
    > [!NOTE]  
    >  A opção para habilitar o detalhamento não estará disponível para modelos de série temporal.  
  
13. Na **nome do modelo de mineração**, digite `Forecasting`e, em seguida, clique em **concluir**.  
  
     Designer de mineração de dados é aberta para exibir o `Forecasting` estrutura de mineração que você acabou de criar.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Modificando a estrutura de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Designer de mineração de dados](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
