---
title: Criando uma estrutura e um modelo de previsão (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6e631a8983705d4f58e4b193823c9a255284f346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63204814"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>Criando uma estrutura e um modelo de previsão (Tutorial de mineração de dados intermediário)
  Em seguida, você usará o Assistente de Mineração de Dados para criar uma nova estrutura e um novo modelo de mineração baseados na exibição da fonte de dados recém-criada. Nesta tarefa, você especificará que o modelo de mineração deverá usar o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series.  
  
### <a name="to-create-a-forecasting-mining-structure"></a>Para criar uma estrutura de mineração de previsão  
  
1.  Em Gerenciador de Soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse em **estruturas de mineração** e selecione **nova estrutura de mineração**.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  Na página **selecionar o método de definição** , verifique se a **partir de banco de dados relacional existente ou data warehouse** está selecionada e clique em **Avançar**.  
  
4.  Na página **criar a estrutura de mineração de dados** , sob a **qual data mining técnica você deseja usar?**, selecione **série temporal da Microsoft**e clique em **Avançar**.  
  
5.  Na página **selecionar exibição da fonte de dados** , em **exibições da fonte de dados disponíveis**, selecione **SalesByRegion**.  
  
6.  Clique em **Próximo**.  
  
7.  Na página **especificar tipos de tabela** , verifique se a caixa de seleção na coluna **caso** da tabela vTimeSeries está selecionada e clique em **Avançar**.  
  
8.  Na página **especificar os dados de treinamento** , marque as caixas de seleção na coluna **chave** para as colunas ModelRegion e ReportingDate.  
  
     ReportingDate deve estar marcada por padrão, já que você especificou essa coluna como a chave primária lógica quando criou a exibição da fonte de dados. Ao adicionar ModelRegion como uma segunda chave, você está dizendo ao algoritmo para criar uma série de tempo separada para cada combinação de modelo e região listada nesse campo.  
  
9. Marque as caixas de seleção nas colunas **entrada** e **previsível** para a quantidade, coluna e clique em **Avançar**.  
  
     Ao selecionar **previsível**, você indica que deseja criar previsões nos dados nesta coluna. No entanto, como você deseja basear as previsões em dados passados, deverá adicionar também a coluna como uma entrada.  
  
10. Na página **especificar conteúdo e tipo de dados das colunas**, examine as seleções.  
  
     A coluna ModelRegion é designada como uma coluna de **chave** e a coluna ReportingDate é designada automaticamente como uma coluna **Key Time** . Só é possível ter um de cada tipo de chave.  
  
11. Clique em **Próximo**.  
  
12. Na página **concluindo o assistente** , para **nome da estrutura**de mineração `Forecasting`, digite.  
  
    > [!NOTE]  
    >  A opção para habilitar o detalhamento não estará disponível para modelos de série temporal.  
  
13. Em **nome do modelo**de mineração `Forecasting`, digite e clique em **concluir**.  
  
     O designer de mineração de dados é `Forecasting` aberto para exibir a estrutura de mineração que você acabou de criar.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Modificando a estrutura de previsão &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Designer de mineração de dados](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo MTS](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
