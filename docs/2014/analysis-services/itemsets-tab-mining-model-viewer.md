---
title: Guia conjuntos de itens (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.itemsets.f1
ms.assetid: 95b2b805-b142-4064-9c80-4b1b3fe2fe63
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4fb7491a8c9fd4a3ee4656bac9c45f0f8a365b74
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019458"
---
# <a name="itemsets-tab-mining-model-viewer"></a>Guia Conjuntos de Itens (Visualizador do Modelo de Mineração)
  Use o painel **Conjunto de Itens** para exibir os conjuntos de itens frequentes presentes em um modelo de mineração de regras por associação. Como um modelo de associação pode conter muitos conjuntos de itens, os controles são fornecidos no visualizador para ajudá-lo a filtrar os conjuntos de itens exibidos no visualizador.  
  
 **Para obter mais informações:** [Algoritmo de associação da Microsoft](data-mining/microsoft-association-algorithm.md), [Procurar um modelo usando o Visualizador de regras da Microsoft](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração para exibir o que está presente na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador para exibir o modelo de mineração selecionado. Você pode usar o visualizador personalizado para modelos de associação ou o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar visualizadores de plug-in se houver.  
  
 **Suporte mínimo**  
 Altere este valor para definir o suporte mínimo que um conjunto de itens precisa conter para aparecer no visualizador. O valor padrão que é exibido quando você primeiro abre o modelo é calculado pelo modelo, mas você pode alterá-lo para ver mais ou menos conjuntos de itens.  
  
 **Tamanho mínimo do conjunto de itens**  
 Altere este valor para definir o número mínimo de itens que devem ser incluídos em um conjunto de itens antes de ele ser exibido no visualizador.  
  
 **Filtrar o conjunto de itens**  
 Digite um valor de cadeia de caracteres para filtrar os conjuntos de itens que aparecem no visualizador.  
  
 Você também pode digitar expressões regulares do .NET como critérios de filtro. Por exemplo, a expressão a seguir retorna todos os conjuntos de itens que contêm 'Road Bottle Cage':  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*`  
  
 Observe que você pode precisar atualizar a exibição para ver os critérios de filtro serem aplicados. Você também pode alternar a opção **Mostrar nome longo** como ligada e desligada para atualizar a lista.  
  
 Por padrão os critérios de filtro aplicam-se ao nome completo da combinação atributo-valor; portanto, se você só estiver exibindo o nome de atributo, pode não ser óbvio que os critérios de filtro foram aplicados corretamente. Use a lista suspensa **Mostrar** para selecionar **Mostrar o nome e valor de atributo**e verifique se a lista de conjuntos de itens está filtrada corretamente.  
  
 **Mostrar**  
 Ajuste como o conjunto de itens será exibido no visualizador. Você pode selecionar uma das três opções seguintes:  
  
-   Mostrar o nome e valor de atributo  
  
-   Mostrar apenas o valor de atributo  
  
-   Mostrar apenas o nome do atributo  
  
 Observe que esta opção não exige o modelo; ela apenas filtra os atributos ou valores exibidos.  
  
 **Mostrar nome longo**  
 Selecione esta opção para exibir o nome completo do conjunto de itens como aparece no conteúdo do modelo de mineração.  
  
 **Máximo de linhas**  
 Limite o número de conjunto de itens que serão exibidos no visualizador. Por padrão, os conjuntos de itens são ordenados por suporte em ordem decrescente, de modo que abaixar este valor restringirá a lista aos conjuntos de itens mais comuns.  
  
 **Suporte**  
 Exibe o suporte para cada conjunto de itens.  
  
 **Tamanho**  
 Exibe o número de itens que há em cada conjunto de itens.  
  
 **Conjunto de itens**  
 Exibe a descrição da dimensão de cada conjunto de itens. Por padrão, os conjuntos de itens são apresentados como uma lista delimitada por vírgulas de atributos e os respectivos valores. Você pode alterar o modo como eles são exibidos usando a opção **Mostrar** .  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – mineração de dados&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining/data-mining-model-viewers.md)  
  
  