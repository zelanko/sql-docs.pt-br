---
title: Guia diagrama de cluster do clustering de sequências (Visualizador do modelo de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.diagrams.f1
ms.assetid: 4b705397-9af4-4678-9eda-149bc5d762fa
author: minewiskan
ms.author: owend
ms.openlocfilehash: a3e27ccc67858edd8e1f95bb910300a93a3e0db8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940747"
---
# <a name="sequence-clustering-cluster-diagram-tab-mining-model-viewer"></a>Guia Diagrama de Cluster do clustering de sequências (Visualizador do Modelo de Mineração)
  A guia **Diagrama de Cluster** no **Visualizador MSC** fornece uma exibição gráfica de todos os clusters que o modelo de cluster de sequências contém.  
  
 Use esta exibição de um modelo de clustering de sequência para analisar em cada cluster para os casos de apoio, se o detalhamento foi habilitado. Você também pode atribuir nomes descritivos aos clusters e alterar a variável de sombreamento para avaliar a distribuição de valores à primeira vista  
  
 **Para obter mais informações:** [Algoritmo MSC](data-mining/microsoft-sequence-clustering-algorithm.md), [Procurar um modelo usando o Visualizador de Cluster de Sequência da Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração para exibir o que está presente na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador que será usado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado, ou o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. Você também pode usar visualizadores de plug-in se houver.  
  
 **Ampliar**  
 Amplie o diagrama para obter uma exibição mais detalhada dos clusters.  
  
 **Reduzir**  
 Reduza o diagrama, para ver todos os clusters no modelo.  
  
 **Copiar Exibição do Gráfico**  
 Copie a seção visível do diagrama para a área de transferência.  
  
 **Copiar Todo o Gráfico**  
 Copie todo o diagrama na área de transferência.  
  
 **Dimensionar diagrama para ajustar à janela**  
 Reduza o diagrama até que o diagrama inteiro se ajuste na tela.  
  
 **Localizar Nó**  
 Use a caixa de diálogo **Localizar Nó** para filtrar os clusters no gráfico e facilitar a localização de um cluster específico. Para obter mais informações, consulte [Caixa de diálogo Localizar Nó &#40;Visualizador do modelo de mineração&#41;](find-node-dialog-box-mining-model-viewer.md).  
  
 Observe que, neste contexto, você está pesquisando somente o nome do cluster, não os atributos dentro dele; portanto, esta opção será muito útil se você tiver atribuído nomes descritivos ao cluster. Você pode atribuir nomes a clusters no visualizador clicando com o botão direito do mouse em cada cluster e selecionando **Renomear**.  
  
 **Aprimorar Layout**  
 Reordene os clusters no diagrama para aprimorar o layout.  
  
 **Densidade**  
 A aparência do gráfico de barra de densidade e os valores nele dependem do atributo que você selecionou em **Variável de Sombreamento**.  
  
-   Se nenhum estado de atributo for selecionado como a variável de sombreamento, por padrão o sombreamento de densidade aplicado a cada cluster representará o suporte para o cluster, comparado com a população geral de casos.  
  
-   Quando você selecionar um atributo para **Variável de Sombreamento**, deverá selecionar também um valor para **Estado** . Quando você faz isso, o gráfico da barra de densidade é atualizado para mostrar a probabilidade deste estado. Você pode pausar o mouse sobre qualquer cluster individual para ver a probabilidade do estado selecionado para o cluster.  
  
 **Variável de Sombreamento**  
 Selecione um atributo do modelo de mineração para usar no sombreamento do diagrama de cluster.  
  
 **State**  
 Selecione um estado que corresponde à **Variável de Sombreamento**. Por exemplo, se você quiser exibir as sequências que incluem um produto específico, selecione a coluna [Produto] como atributo para **Variável de Sombreamento**e o nome de produto específico como valor de **Estado** .  
  
 **Links**  
 As linhas no diagrama indicam associações entre clusters de sequência. É possível selecionar o número de links exibido no visualizador, ajustando-se o controle deslizante à direita dos clusters. Diminuindo o controle deslizante, somente os links mais fortes serão exibidos.  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining/data-mining-model-viewers.md)  
  
  
