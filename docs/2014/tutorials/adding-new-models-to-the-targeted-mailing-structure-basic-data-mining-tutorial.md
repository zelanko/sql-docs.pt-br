---
title: Adicionando novos modelos à estrutura de endereçamento de destino (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 285ee82110ffdef521d75fb43343f4889663e981
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62822623"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>Adicionando novos modelos à estrutura de mala direta (Tutorial de mineração de dados básico)
  Nesta tarefa, você definirá dois modelos adicionais usando a guia **modelos de mineração** do designer de mineração de dados. Você usará os algoritmos Microsoft Naive Bayes e Microsoft Clustering para criar os modelos. Esses dois algoritmos foram selecionados por causa de sua capacidade de prever um valor discreto (por exemplo, compra de bicicletas). Para obter mais informações sobre esses algoritmos, consulte [algoritmo de clustering da Microsoft](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md) e [algoritmo do Microsoft Naive Bayes](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>Para criar um modelo de mineração de clustering  
  
1.  Alterne para a guia **modelos de mineração** no designer de mineração [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]de dados no.  
  
     Observe que o designer exibe duas colunas, uma para a estrutura de mineração e outra para `TM_Decision_Tree` o modelo de mineração que você criou na lição anterior.  
  
2.  Clique com o botão direito do mouse na coluna **estrutura** e selecione **novo modelo de mineração**.  
  
3.  Na caixa de diálogo **novo modelo de mineração** , em **nome**do modelo `TM_Clustering`, digite.  
  
4.  Em **nome do algoritmo**, selecione **clustering da Microsoft**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 O novo modelo agora aparece na guia **modelos de mineração** do designer de mineração de dados. Esse modelo, criado com o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo clustering, agrupa clientes com características semelhantes em clusters e prevê a compra de bicicletas para cada cluster. Embora você possa modificar o uso e as propriedades da coluna para o novo modelo, nenhuma alteração `TM_Clustering` no modelo é necessária para este tutorial.  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>Criar um modelo de mineração Naive Bayes  
  
1.  Na guia **modelos de mineração** do designer de mineração de dados, na coluna de **estrutura** clickthe à direita e selecione **novo modelo de mineração**.  
  
2.  Na caixa de diálogo **novo modelo de mineração** , em **nome**do modelo `TM_NaiveBayes`, digite.  
  
3.  Em **nome do algoritmo**, selecione **Microsoft Naive Bayes**e clique em **OK**.  
  
     Uma mensagem é exibida informando que o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Naive Bayes não dá suporte às colunas de renda e **idade** **anual** , que são contínuas.  
  
4.  Clique em **Sim** para confirmar a mensagem e continuar.  
  
 Um novo modelo é exibido na guia **modelos de mineração** do designer de mineração de dados. Embora você possa modificar o uso de coluna e as propriedades de todos os modelos nesta guia, nenhuma alteração no `TM_NaiveBayes` modelo é necessária para este tutorial.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Processando modelos na estrutura de mala direta direcionada &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar modelos de mineração a uma estrutura &#40;mineração de dados Analysis Services&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [Designer de mineração de dados](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Movendo objetos de mineração de dados](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  
