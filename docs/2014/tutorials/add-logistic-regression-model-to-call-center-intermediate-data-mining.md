---
title: Adicionando um modelo de regressão logística à estrutura do Call Center (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ccadf7665b112b6ba1055fdcf69aeb99609c3ab3
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312424"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>Adicionando um modelo de regressão logística à estrutura do call center (Tutorial de mineração de dados intermediário)
  Além de analisar os fatores que podem afetar as operações do call center, você também recebeu uma solicitação para fornecer algumas recomendações específicas sobre como melhorar a qualidade de serviço. Nesta tarefa, você usará a mesma estrutura de mineração que usou para criar o modelo exploratório e adicionar um modelo de mineração que será usado para criar previsões.  
  
 No [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], um modelo de regressão logística se baseia no algoritmo de redes neurais e, portanto, fornece a mesma flexibilidade e capacidade que um modelo de rede neural. No entanto, a regressão logística é particularmente bem-apropriada para prever resultados binários.  
  
 Para este cenário, você poderá usar a mesma estrutura de mineração usada no modelo de rede neural. No entanto, você personalizará o novo modelo para direcionar suas questões comerciais. Você está interessado em melhorar a qualidade de serviço e saber quantos operadores experientes você precisa. Então, você configurará seu modelo para prever esses valores.  
  
 Para assegurar que todos os modelos baseados nos dados do call center sejam o mais semelhantes possível, você usará o mesmo valor de semente de antes. Definir o parâmetro de semente assegura que o modelo processa os dados do mesmo ponto de partida, e minimiza variações causadas por artefatos nos dados.  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>Para adicionar um novo modelo de mineração à estrutura de mineração do call center  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no Gerenciador de soluções, clique com botão direito na estrutura de mineração **Call Center guardado**e selecione **abrir Designer**.  
  
2.  No Designer de mineração de dados, clique o **modelos de mineração** guia.  
  
3.  Clique em **criar um modelo de mineração relacionado**.  
  
4.  No **novo modelo de mineração** caixa de diálogo para **nome do modelo**, tipo `Call Center - LR`.  Para **nome do algoritmo**, selecione **Regressão logística da Microsoft**.  
  
5.  Clique em **OK**.  
  
     O novo modelo de mineração é exibido no **modelos de mineração** guia.  
  
### <a name="to-customize-the-logistic-regression-model"></a>Para personalizar o modelo de regressão logística  
  
1.  Na coluna para o novo modelo de mineração, `Call Center - LR`, deixe Fact CallCenter ID como a chave.  
  
2.  Altere o valor de ServiceGrade e operadores de nível dois para **prever**.  
  
     Essas colunas serão usadas como entrada e para previsão. Em essência, você está criando dois modelos separados com os mesmos dados: um que prevê o número de operadores e outro que prevê a classificação de serviço.  
  
3.  Alterar todas as outras colunas para **entrada**.  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>Para especificar a semente e processar os modelos  
  
1.  No **modelo de mineração** guia, a coluna para o modelo denominado Call Center - LR e selecione **definir parâmetros de algoritmo**.  
  
2.  Na linha para o parâmetro HOLDOUT_SEED, clique na célula vazia em **valor**e o tipo `1`. Clique em **OK**.  
  
    > [!NOTE]  
    >  O valor escolhido como semente não importa, desde que você use a mesma semente para todos os modelos relacionados.  
  
3.  No **modelos de mineração** menu, selecione **processar estrutura de mineração e todos os modelos**. Clique em **Sim** para implantar o projeto de mineração de dados atualizados no servidor.  
  
4.  No **processar modelo de mineração** caixa de diálogo, clique em **executar**.  
  
5.  Clique em **fechar** para fechar o **progresso do processo** caixa de diálogo e clique **fechar** novamente no **processar modelo de mineração** caixa de diálogo.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando previsões para modelos de Call Center &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e considerações de processamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  