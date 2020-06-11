---
title: Guia perfis de atributo (Visualizador do modelo de mineração) | Microsoft Docs
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
ms.openlocfilehash: 4df97455d2fae8cb3375967a8e37a2329a7509fa
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527904"
---
# <a name="attribute-profiles-tab-mining-model-viewer"></a>Guia Perfis de Atributo (Visualizador do Modelo de Mineração)
  Utilize a guia **Perfis de Atributo** para ver como a distribuição de valores de entrada em um estado de modelo Naive Bayes contribui para cada estado do atributo de resultado. A distribuição de valores é mostrada como um histograma colorido, todas as distribuições apresentadas em um formato de tabela, para facilitar a comparação de valores.  
  
 **Para obter mais informações:** [Algoritmo Microsoft Naive Bayes](data-mining/microsoft-naive-bayes-algorithm.md), [Procurar um modelo usando o Visualizador Naive Bayes da Microsoft](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração a ser exibido, dentre eles na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Você pode escolher um visualizador personalizado fornecido para cada modelo de mineração ou o Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar os visualizadores de plug-in se estiverem disponíveis.  
  
 **Mostrar Legenda**  
 Selecione esta opção para exibir uma chave que corresponde a cada valor em **States** a uma das cores usadas no gráfico de distribuição.  
  
 **Barras de Histograma**  
 Selecione quantas barras deseja incluir no histograma. Caso haja mais barras do que você opte por exibir, as barras de maior importância serão retidas e as restantes serão agrupadas em **Outras**.  
  
 **Previsível**  
 Selecione uma coluna previsível a partir do modelo de mineração.  
  
 **Perfis de atributo**  
 A tabela contém as seguintes colunas:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Atributos**|Lista as colunas do modelo de mineração contidas no modelo de mineração.|  
|**Européia**|Uma coluna opcional que descreve qual estado a cor da linha de atributos correspondente representa. Some ou remova usando a caixa de seleção **Mostrar Legenda** .|  
|**Média**|Exibe a distribuição do atributo por todo o conjunto de dados.|  
|**Coluna para os estados de atributo previsível**|Exibe uma coluna para cada estado da coluna previsível em relação a cada linha correspondente a um atributo de entrada no modelo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining/data-mining-model-viewers.md)  
  
  
