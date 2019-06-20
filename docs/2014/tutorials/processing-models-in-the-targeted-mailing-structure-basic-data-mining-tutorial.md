---
title: Processando modelos na estrutura de mala direta (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9d8233bb-117e-4563-9302-8a5a8ad1fae2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 605088d405cbd2dcfba92a2da5fa4e07c38d8f0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188229"
---
# <a name="processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>Processando modelos na estrutura de mala direta (Tutorial de mineração de dados básico)
  Antes de navegar ou trabalhar nos modelos de mineração criados por você, implante o projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e processe a estrutura de mineração e os modelos de mineração.  
  
-   *Implantando* envia o projeto para um servidor e cria objetos nesse projeto no servidor.  
  
-   *Processando* popula [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] objetos com os dados de fontes de dados relacionais.  
  
 Os modelos só poderão ser usados depois de serem implantados e processados. Além disso, ao fazer uma mudança no modelo, tal como adicionar novos dados, você deverá implantar e processar os modelos novamente.  
  
## <a name="ensuring-consistency-with-holdoutseed"></a>Garantindo a consistência com HoldoutSeed  
 Quando você implanta um projeto e processa a estrutura e os modelos, as linhas individuais da sua estrutura de dados são atribuídas ao conjunto de treinamento ou ao conjunto de teste com base em um valor numérico de semente aleatória. Por padrão, o valor numérico da semente aleatória é calculado com base em atributos da estrutura de dados. No entanto, se você alterar alguns aspectos do seu modelo, o valor da semente aleatória poderia ser alterado, levando a resultados um pouco diferentes. Portanto, para garantir que os resultados são iguais aos descritos aqui, atribuiremos fixo *semente de validação* de `12`. A semente de controle é usada para inicializar o algoritmo de amostragem e garante que os dados sejam particionados aproximadamente da mesma forma para todas as estruturas de mineração e seus modelos.  
  
 Esse valor não afeta o número de casos no conjunto de treinamento; apenas garante que o mesmo método de particionamento seja usado sempre na criação do modelo.  
  
 Para obter mais informações sobre sementes de validação, consulte [conjuntos de dados de teste e treinamento](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md).  
  
#### <a name="to-set-the-holdout-seed"></a>Para definir Holdout Seed  
  
1.  Clique no **estrutura de mineração** guia ou o **modelos de mineração** guia no Designer de mineração de dados no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
     **Direcionado MiningStructure de mala direta** exibe o **propriedades** painel.  
  
2.  Certifique-se de que o **propriedades** painel está aberto pressionando **F4**.  
  
3.  Certifique-se de que **CacheMode** é definido como **KeepTrainingCases**.  
  
4.  Insira `12` para **HoldoutSeed**.  
  
## <a name="deploying-and-processing-the-models"></a>Implantando e processando os modelos  
 No Designer de mineração de dados, você pode decidir que objetos processar, dependendo do escopo das alterações feitas ao seu modelo ou os dados subjacentes:  
  
 Para esta tarefa, como os dados e os modelos são novos, você processará a estrutura e todos os modelos ao mesmo tempo.  
  
#### <a name="to-deploy-the-project-and-process-all-the-mining-models"></a>Para implantar o projeto e processar todos os modelos de mineração  
  
1.  No **modelo de mineração** menu, selecione **processar estrutura de mineração e todos os modelos**.  
  
     Caso tenha feito alterações na estrutura de mineração, será solicitado que você crie e implante o projeto antes de processar os modelos. Clique em **Sim**.  
  
2.  Clique em **executados** na **processando estrutura de mineração - mala** caixa de diálogo.  
  
     A caixa de diálogo **Andamento do Processo** é aberta para exibir os detalhes sobre o processamento do modelo. O processamento do modelo pode demorar um pouco, dependendo do computador.  
  
3.  Clique em **Fechar** na caixa de diálogo **Andamento do Processo** após os modelos completarem seu processamento.  
  
4.  Clique em **feche** na **processando estrutura de mineração - \<estrutura >** caixa de diálogo.  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Adicionando novos modelos à estrutura de mala direta &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 4: Explorando os modelos de mala direta &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e considerações de processamento &#40;Mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
