---
title: Guia diagrama de cluster (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.diagram.f1
ms.assetid: 180e6f48-5c4d-4160-b84d-608b98f7b840
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1855150cdfbb4d2132c1edc7c08604dd90b87a9d
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527452"
---
# <a name="cluster-diagram-tab-mining-model-viewer"></a>Guia Diagrama de Cluster (Visualizador do Modelo de Mineração)
  A guia **Diagrama de Cluster** fornece uma exibição gráfica de todos os clusters que o modelo de clustering contém.  
  
 **Para obter mais informações:** [Algoritmo MSC](data-mining/microsoft-clustering-algorithm.md), [Procurar um modelo usando o Visualizador de Cluster da Microsoft](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração dentre eles na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador para explorar o modelo de mineração selecionado. Você pode usar um dos visualizadores de clustering personalizados, ou Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar um visualizador de plug-in se houver.  
  
 **Ampliar**  
 Amplie o diagrama para obter uma exibição detalhada dos clusters.  
  
 **Reduzir**  
 Reduza a imagem do diagrama, para ver mais clusters.  
  
 **Copiar Exibição do Gráfico**  
 Copie a seção visível do diagrama para a área de transferência.  
  
 **Copiar Todo o Gráfico**  
 Copie todo o diagrama na área de transferência.  
  
 **Dimensionar diagrama para ajustar à janela**  
 Reduza o diagrama até que o diagrama inteiro se ajuste na tela.  
  
 **Localizar Nó**  
 Abre a caixa de diálogo **Localizar Nó** . Este recurso é útil em modelos grandes, onde pode ser difícil localizar o atributo de interesse. Você pode inserir critérios de pesquisa na caixa de diálogo e a exibição dos clusters será filtrada para mostrar somente o cluster que contém a cadeia de pesquisa.  
  
 **Aprimorar Layout**  
 Reordene os clusters no diagrama para aprimorar o layout.  
  
 **Densidade**  
 Use esta opção para alterar quais pares atributo-valor são exibidos no diagrama de cluster. Você usa a opção **Variável de Sombreamento** para selecionar um atributo e usa **Estado** para escolher um valor. O sombreamento no gráfico indica a densidade do par atributo-valor dentro do cluster.  
  
 Se **População** estiver selecionada, o diagrama mostrará a quantidade de suporte para cada cluster, ou seja, o número de casos já que nenhum atributo foi selecionado.  
  
 **Variável de Sombreamento**  
 Selecione um atributo para representar no diagrama de cluster.  
  
 **State**  
 Selecione um único estado da **Variável de Sombreamento** para usar no diagrama de cluster.  
  
 **Vincule**  
 Ajuste quantos links são mostrados entre clusters, movendo o controle deslizante para cima ou para baixo. Abaixar o controle deslizante deixa somente as associações mais fortes entre clusters.  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining/data-mining-model-viewers.md)  
  
  
