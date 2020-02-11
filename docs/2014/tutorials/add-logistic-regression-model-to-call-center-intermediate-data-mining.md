---
title: Adicionando um modelo de regressão logística à estrutura do Call Center (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 32e66a84dea20964c11c7de0aa568530aa8c28c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62823260"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>Adicionando um modelo de regressão logística à estrutura do call center (Tutorial de mineração de dados intermediário)
  Além de analisar os fatores que podem afetar as operações do call center, você também recebeu uma solicitação para fornecer algumas recomendações específicas sobre como melhorar a qualidade de serviço. Nesta tarefa, você usará a mesma estrutura de mineração que usou para criar o modelo exploratório e adicionar um modelo de mineração que será usado para criar previsões.  
  
 No [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], um modelo de regressão logística se baseia no algoritmo de redes neurais e, portanto, fornece a mesma flexibilidade e capacidade que um modelo de rede neural. No entanto, a regressão logística é particularmente bem-apropriada para prever resultados binários.  
  
 Para este cenário, você poderá usar a mesma estrutura de mineração usada no modelo de rede neural. No entanto, você personalizará o novo modelo para direcionar suas questões comerciais. Você está interessado em melhorar a qualidade de serviço e saber quantos operadores experientes você precisa. Então, você configurará seu modelo para prever esses valores.  
  
 Para assegurar que todos os modelos baseados nos dados do call center sejam o mais semelhantes possível, você usará o mesmo valor de semente de antes. Definir o parâmetro de semente assegura que o modelo processa os dados do mesmo ponto de partida, e minimiza variações causadas por artefatos nos dados.  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>Para adicionar um novo modelo de mineração à estrutura de mineração do call center  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], em Gerenciador de soluções, clique com o botão direito do mouse na estrutura de mineração, **compartimentalizados do Call Center**e selecione **Abrir Designer**.  
  
2.  No designer de mineração de dados, clique na guia **modelos de mineração** .  
  
3.  Clique em **criar um modelo de mineração relacionado**.  
  
4.  Na caixa de diálogo **novo modelo de mineração** , para **nome**do modelo `Call Center - LR`, digite.  Para **nome do algoritmo**, selecione **regressão logística da Microsoft**.  
  
5.  Clique em **OK**.  
  
     O novo modelo de mineração é exibido na guia **modelos de mineração** .  
  
### <a name="to-customize-the-logistic-regression-model"></a>Para personalizar o modelo de regressão logística  
  
1.  Na coluna para o novo modelo de mineração, `Call Center - LR`deixe a ID callcenter do fato como a chave.  
  
2.  Altere o valor dos operadores ServiceGrade e Level dois para **prever**.  
  
     Essas colunas serão usadas como entrada e para previsão. Em essência, você está criando dois modelos separados com os mesmos dados: um que prevê o número de operadores e outro que prevê a classificação de serviço.  
  
3.  Altere todas as outras colunas para **entrada**.  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>Para especificar a semente e processar os modelos  
  
1.  Na guia **modelo de mineração** , clique com o botão direito do mouse na coluna do modelo chamado Call Center-LR e selecione **definir parâmetros de algoritmo**.  
  
2.  Na linha do parâmetro HOLDOUT_SEED, clique na célula vazia em **valor**e digite `1`. Clique em **OK**.  
  
    > [!NOTE]  
    >  O valor escolhido como semente não importa, desde que você use a mesma semente para todos os modelos relacionados.  
  
3.  No menu **modelos de mineração** , selecione **processar estrutura de mineração e todos os modelos**. Clique em **Sim** para implantar o projeto de Data Mining atualizado no servidor.  
  
4.  Na caixa de diálogo **modelo de mineração de processo** , clique em **executar**.  
  
5.  Clique em **fechar** para fechar a caixa de diálogo **progresso do processo** e clique em **fechar** novamente na caixa de diálogo **processar modelo de mineração** .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando previsões para os modelos do Call Center &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos e considerações de processamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
