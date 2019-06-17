---
title: Regras de guia (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.rules.f1
ms.assetid: 705d5492-b58f-45d9-94d7-ed57b7025823
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fca78578046122a1598df096e45965367b7880ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070097"
---
# <a name="rules-tab-mining-model-viewer"></a>Guia Regras (Visualizador do Modelo de Mineração)
  Use o painel **Regras** em um modelo de associação para exibir as regras que o algoritmo extraiu dos dados. As regras descrevem como os itens estão relacionados uns com os outros e podem ser usados para criar recomendações.  
  
 Pode-se utilizar as opções do visualizador para filtrar o número de regras exibidas no visualizador.  
  
> [!WARNING]  
>  Por padrão, somente as regras que estão acima do limite de probabilidade definidas em **Probabilidade mínima** são exibidas no visualizador. Você não pode diminuir este valor usando o visualizador, porque o limite de probabilidade para saída de regra é determinado quando o modelo é criado. Para obter mais informações, consulte [Referência técnica do algoritmo de associação da Microsoft](data-mining/microsoft-association-algorithm-technical-reference.md).  
  
 **Para obter mais informações:** [Algoritmo associação da Microsoft](data-mining/microsoft-association-algorithm.md), [procurar um modelo usando o Visualizador de regras de associação da Microsoft](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração para exibir o que está presente na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador para exibir o modelo de mineração selecionado. Você pode usar o visualizador personalizado para cada modelo de mineração, ou o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. Você também pode usar visualizadores de plug-in se houver.  
  
 **Probabilidade mínima**  
 Altere este valor para definir a probabilidade mínima exigida para uma regra a ser exibida no visualizador. Aumentar o valor para a probabilidade reduzirá o número de regras que são exibidas.  
  
 **Importância mínima**  
 Altere este valor para definir a importância mínima exigida para uma regra a ser exibida no visualizador. Aumentar o valor para a importância reduzirá o número de regras que são exibidas.  
  
 **Regra de filtro**  
 Digite um valor de cadeia de caracteres para filtrar o número de regras que aparecem no visualizador.  
  
 Você também pode digitar expressões regulares do .NET como critérios de filtro. Por exemplo, a expressão a seguir retorna todas as regras que contêm 'Road Bottle Cage' no lado esquerdo da regra:  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*->.*`  
  
 Observe que você pode precisar atualizar a exibição para ver os critérios de filtro serem aplicados. Você também pode alternar a opção **Mostrar nome longo** como ligada e desligada para atualizar a lista.  
  
 Por padrão os critérios de filtro aplicam-se ao nome completo da combinação atributo-valor; portanto, se você só estiver exibindo o nome de atributo, pode não ser óbvio que os critérios de filtro foram aplicados corretamente. Use a lista suspensa **Mostrar** para selecionar **Mostrar o nome e valor de atributo**e verifique se a lista de conjuntos de itens está filtrada corretamente.  
  
 **Mostrar**  
 Ajuste o modo pelo qual a regra é exibida no visualizador. Você pode selecionar uma das três opções seguintes:  
  
-   Mostrar o nome e valor de atributo  
  
-   Mostrar apenas o valor de atributo  
  
-   Mostrar apenas o nome de atributo  
  
 **Mostrar nome longo**  
 Mostrar o nome longo da regra conforme aparece no conteúdo de modelo de mineração.  
  
 **Máximo de linhas**  
 Limitar o número de regras exibidas no visualizador.  
  
 **Probabilidade**  
 Esta coluna no gráfico exibe a probabilidade para cada regra.  
  
 Clique no cabeçalho da coluna para classificar por probabilidade.  
  
 **Importância**  
 Esta coluna no gráfico exibe a importância para cada regra.  
  
 Clique no cabeçalho da coluna para classificar por importância.  
  
 **Regra**  
 Esta coluna no gráfico exibe a descrição de texto para cada regra, de acordo com o formato especificado usando as opções **Mostrar** e **Mostrar nome longo**.  
  
 Clique no cabeçalho da coluna para classificar pelo texto da regra.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining/data-mining-model-viewers.md)  
  
  
