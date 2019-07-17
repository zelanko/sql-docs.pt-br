---
title: Copiar uma exibição de um modelo de mineração | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 685d4ce90312e9f34dcf9b8a6e0c94b419f37ee4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210168"
---
# <a name="copy-a-view-of-a-mining-model"></a>Copiar uma exibição de um modelo de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa um visualizador separado para cada tipo de modelo de mineração. Muitos dos visualizadores têm componentes a partir dos quais você pode copiar o conteúdo para a Área de Transferência e de lá colar o conteúdo em um documento ou no software de manipulação de imagens. Os componentes a seguir tornam essa funcionalidade disponível:  
  
-   Diagrama de Cluster no Visualizador de Cluster da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e o Visualizador de Cluster de Sequências da [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Árvore de Decisão no Visualizador de Árvore da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e o Visualizador MTS [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Transições de estado no Visualizador de Cluster de Sequências da [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Rede de Dependências no Visualizador de Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , Visualizador Naïve Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e o Visualizador de Árvore da [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Conteúdo do modelo de mineração, do painel Detalhes do Nó do Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
 Você pode copiar a representação completa do modelo de mineração ou apenas a parte que está visível no visualizador.  
  
> [!WARNING]  
>  Quando você copia um modelo usando o visualizador, ele não cria um novo objeto modelo. Para criar um novo modelo, você deve usar o assistente ou o Designer de Mineração de Dados. Para obter mais informações, consulte [Criar uma cópia de um modelo de mineração](../../analysis-services/data-mining/make-a-copy-of-a-mining-model.md).  
  
### <a name="to-copy-the-complete-model-to-the-clipboard"></a>Para copiar o modelo completo para a Área de Transferência  
  
1.  Na lista **Modelo de Mineração** na guia **Visualizador do Modelo de Mineração** , selecione o modelo de mineração que deseja exibir.  
  
2.  Selecione a guia apropriada, como a guia **Rede de Dependências** e, em seguida, clique em **Copiar Gráfico Inteiro** na barra de ferramentas da guia.  
  
### <a name="to-copy-the-visible-piece-of-the-model-to-the-clipboard"></a>Para copiar a parte visível do modelo para a Área de Transferência  
  
1.  Na lista **Modelo de Mineração** na guia **Visualizador do Modelo de Mineração** , selecione o modelo de mineração que deseja exibir.  
  
2.  Selecione a guia apropriada, como a guia **Rede de Dependência** e, em seguida, aplique mais ou menos zoom para exibir o modelo no nível desejado.  
  
3.  Clique em **Copiar Exibição de Gráfico** na barra de ferramentas da guia selecionada.  
  
### <a name="to-copy-the-mining-model-content-to-the-clipboard"></a>Para copiar o conteúdo do modelo de mineração para a Área de Transferência  
  
1.  Na lista **Modelo de Mineração** na guia **Visualizador do Modelo de Mineração** , selecione o modelo de mineração que deseja exibir.  
  
2.  Na lista suspensa **Visualizador** , selecione **Visualizador de Árvore de Conteúdo Genérica da Microsoft**.  
  
3.  No painel **Legenda do Nó (ID Exclusiva)** , clique em um nó.  
  
4.  Clique com o botão direito do mouse no painel **Detalhes do Nó** e, em seguida, selecione **Selecionar tudo**.  
  
5.  Clique com o botão direito do mouse no painel **Detalhes do Nó** novamente e selecione **Copiar**.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do visualizador do modelo de mineração](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
