---
title: Perfis de atributo (Visualizador do modelo de mineração) da guia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.profiles.f1
ms.assetid: 17c7e7ae-273c-4a6b-9a35-e8b9b8e65999
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b2bb75ec06d9b5c14ce5c2dcc85561412b362b40
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063166"
---
# <a name="attribute-profiles-tab-mining-model-viewer"></a>Guia Perfis de Atributo (Visualizador do Modelo de Mineração)
  Utilize a guia **Perfis de Atributo** para ver como a distribuição de valores de entrada em um estado de modelo Naive Bayes contribui para cada estado do atributo de resultado. A distribuição de valores é mostrada como um histograma colorido, todas as distribuições apresentadas em um formato de tabela, para facilitar a comparação de valores.  
  
 **Para obter mais informações:** [Algoritmo Microsoft Naive Bayes](data-mining/microsoft-naive-bayes-algorithm.md), [procurar um modelo usando o visualizador Microsoft Naive Bayes](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração a ser exibido, dentre eles na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Você pode escolher um visualizador personalizado fornecido para cada modelo de mineração ou o Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar os visualizadores de plug-in se estiverem disponíveis.  
  
 **Mostrar legenda**  
 Selecione esta opção para exibir uma chave que corresponde a cada valor em **States** a uma das cores usadas no gráfico de distribuição.  
  
 **Barras de histograma**  
 Selecione quantas barras deseja incluir no histograma. Caso haja mais barras do que você opte por exibir, as barras de maior importância serão retidas e as restantes serão agrupadas em **Outras**.  
  
 **Previsível**  
 Selecione uma coluna previsível a partir do modelo de mineração.  
  
 **Perfis de Atributo**  
 A tabela contém as seguintes colunas:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Atributos**|Lista as colunas do modelo de mineração contidas no modelo de mineração.|  
|**Estados**|Uma coluna opcional que descreve qual estado a cor da linha de atributos correspondente representa. Some ou remova usando a caixa de seleção **Mostrar Legenda** .|  
|**População**|Exibe a distribuição do atributo por todo o conjunto de dados.|  
|**Coluna para os estados do atributo previsível**|Exibe uma coluna para cada estado da coluna previsível em relação a cada linha correspondente a um atributo de entrada no modelo.|  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining/data-mining-model-viewers.md)  
  
  
