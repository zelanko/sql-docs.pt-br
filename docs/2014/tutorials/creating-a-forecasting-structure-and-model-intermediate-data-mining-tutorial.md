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
ms.topic: article
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 47d6e75a691c53fe1658fb5f79ee2bde8e9c2d01
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312264"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>Criando uma estrutura e um modelo de previsão (Tutorial de mineração de dados intermediário)
  Em seguida, você usará o Assistente de Mineração de Dados para criar uma nova estrutura e um novo modelo de mineração baseados na exibição da fonte de dados recém-criada. Nesta tarefa, você especificará que o modelo de mineração deverá usar o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series.  
  
### <a name="to-create-a-forecasting-mining-structure"></a>Para criar uma estrutura de mineração de previsão  
  
1.  No Gerenciador de soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique com botão direito **estruturas de mineração** e selecione **nova estrutura de mineração**.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  No **Selecionar método de definição** Verifique **de warehouse existente de dados ou banco de dados relacional** está selecionado e, em seguida, clique em **próximo**.  
  
4.  Sobre o **criar a estrutura de mineração de dados** página em **qual técnica de mineração de dados você deseja usar?**, selecione **MTS**e, em seguida, clique em  **Próxima**.  
  
5.  Sobre o **Selecionar exibição da fonte de dados** página em **modos de exibição de fonte de dados disponíveis**, selecione **SalesByRegion**.  
  
6.  Clique em **Avançar**.  
  
7.  No **especificar tipos de tabela** página, certifique-se de que a caixa de seleção no **caso** coluna da tabela vTimeSeries está selecionado e, em seguida, clique em **próximo**.  
  
8.  Sobre o **especificar os dados de treinamento** , marque as caixas de seleção a **chave** coluna para as colunas ModelRegion e ReportingDate.  
  
     ReportingDate deve estar marcada por padrão, já que você especificou essa coluna como a chave primária lógica quando criou a exibição da fonte de dados. Ao adicionar ModelRegion como uma segunda chave, você está dizendo ao algoritmo para criar uma série de tempo separada para cada combinação de modelo e região listada nesse campo.  
  
9. Marque as caixas de seleção de **entrada** e **previsível** colunas para a quantidade, coluna e clique **próximo**.  
  
     Selecionando **previsível**, você indica que você deseja criar previsões sobre os dados nesta coluna. No entanto, como você deseja basear as previsões em dados passados, deverá adicionar também a coluna como uma entrada.  
  
10. Na página **colunas especificar conteúdo e tipo de dados**, examine as seleções.  
  
     A coluna ModelRegion é designada como um **chave** coluna e a coluna ReportingDate é automaticamente designada como um **Key Time** coluna. Só é possível ter um de cada tipo de chave.  
  
11. Clique em **Avançar**.  
  
12. Sobre o **Concluindo o assistente** página, para **nome da estrutura de mineração**, tipo `Forecasting`.  
  
    > [!NOTE]  
    >  A opção para habilitar o detalhamento não estará disponível para modelos de série temporal.  
  
13. Em **nome do modelo de mineração**, tipo `Forecasting`e, em seguida, clique em **concluir**.  
  
     Designer de mineração de dados é aberto para exibir o `Forecasting` estrutura de mineração que você acabou de criar.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Modificando a estrutura de previsão &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Designer de mineração de dados](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  