---
title: Adicionando novos modelos à estrutura de mala direta (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
caps.latest.revision: 45
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c5e31e06a489b1807335f63dd1675fc9e77c45b4
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312374"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>Adicionando novos modelos à estrutura de mala direta (Tutorial de mineração de dados básico)
  Nesta tarefa, você definirá dois modelos adicionais usando o **modelos de mineração** guia do Designer de mineração de dados. Você usará os algoritmos Microsoft Naive Bayes e Microsoft Clustering para criar os modelos. Esses dois algoritmos foram selecionados por causa de sua capacidade de prever um valor discreto (por exemplo, compra de bicicletas). Para obter mais informações sobre esses algoritmos, consulte [Microsoft Clustering Algorithm](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md) e [algoritmo Naive Bayes da Microsoft](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>Para criar um modelo de mineração de clustering  
  
1.  Alterne para o **modelos de mineração** guia no Designer de mineração de dados no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
     Observe que o designer exibe duas colunas, uma estrutura de mineração e outra para o `TM_Decision_Tree` modelo de mineração, que você criou na lição anterior.  
  
2.  Clique com botão direito do **estrutura** coluna e selecione **novo modelo de mineração**.  
  
3.  No **novo modelo de mineração** na caixa **nome do modelo**, tipo `TM_Clustering`.  
  
4.  Em **nome do algoritmo**, selecione **Microsoft Clustering**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 O novo modelo agora aparece no **modelos de mineração** guia do Designer de mineração de dados. Esse modelo, criado com o [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering algoritmo, grupos de clientes com características similares em clusters e prevê a compra de bicicletas para cada cluster. Embora você possa modificar o uso da coluna e propriedades para o novo modelo, nenhuma alteração para o `TM_Clustering` modelo são necessários para este tutorial.  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>Criar um modelo de mineração Naive Bayes  
  
1.  No **modelos de mineração** guia do Designer de mineração de dados, clique à direita-no **estrutura** coluna e selecione **novo modelo de mineração**.  
  
2.  No **novo modelo de mineração** caixa de diálogo **nome do modelo**, tipo `TM_NaiveBayes`.  
  
3.  Em **nome do algoritmo**, selecione **Microsoft Naive Bayes**, em seguida, clique em **Okey**.  
  
     Será exibida uma mensagem informando que o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Naive Bayes não oferece suporte a **idade** e **Renda anual** colunas, que são contínuas.  
  
4.  Clique em **Sim** para reconhecer a mensagem e continuar.  
  
 Um novo modelo é exibido no **modelos de mineração** guia do Designer de mineração de dados. Embora você possa modificar o uso da coluna e propriedades para todos os modelos nessa guia, nenhuma alteração para o `TM_NaiveBayes` modelo são necessários para este tutorial.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Processando modelos na estrutura de mala direta &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar modelos de mineração a uma estrutura &#40;Analysis Services – mineração de dados&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [Designer de mineração de dados](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Movendo objetos de Mineração de dados](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  