---
title: Caixa de diálogo Filtrar (gráfico de precisão de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 71e884a9-7ec4-4459-a4c4-87f6c796d478
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6102fe9c623e785c0ca207660697bffebce82bb5
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544480"
---
# <a name="filter-dialog-box-mining-accuracy-chart"></a>Caixa de diálogo Filtro (gráfico de precisão de mineração)
  A caixa de diálogo **Filtro** o ajuda a criar condições que você pode aplicar em um conjunto de dados. O conjunto de dados pode ser um conjunto externo usado para teste ou os dados de caso usados para treinar um modelo de mineração. Essa caixa de diálogo ajuda a criar critérios que podem ser salvos como parte de critérios de filtragem mais complexos na caixa de diálogo **Filtro de Conjunto de Dados** ou na caixa de diálogo **Filtro de Modelos** .  
  
-   A caixa de diálogo **Filtro de Conjunto de Dados** está disponível na guia **Seleção de Entrada** do designer **Gráfico de Precisão de Mineração** .  
  
-   A caixa de diálogo **Filtro de Modelos** está disponível na guia **Modelos de Mineração** do Designer de Mineração de Dados.  
  
 Se estiver aplicando um filtro em um modelo de mineração, use primeiro a caixa de diálogo **Filtro de Modelos** para escolher uma tabela. Em seguida, use a caixa de diálogo **Filtro** para criar condições que só se aplicam à tabela selecionada.  
  
 Se estiver criando um filtro a ser aplicado em um conjunto de dados de teste externo, use primeiro a caixa de diálogo **Filtro de Conjunto de Dados** para escolher uma tabela na lista de tabelas em uma exibição da fonte de dados. Em seguida, use a caixa de diálogo **Filtro** para criar condições que só se aplicam à tabela selecionada.  
  
 Depois de criar um conjunto de condições que se aplicam a uma única tabela, [!INCLUDE[clickOK](../includes/clickok-md.md)]. As alterações feitas na caixa de diálogo **Filtro** são adicionadas automaticamente à expressão de filtro na caixa de diálogo pai, **Filtro de Conjunto de Dados** ou **Filtro de Modelos**.  
  
 Se você aplicar o filtro ao novo conjunto de dados, o modelo de mineração de dados existente será usado para avaliar somente os casos do conjunto de dados que satisfaçam as condições. No entanto, se você aplicar o filtro ao próprio modelo de mineração, a precisão do modelo será avaliada apenas para os casos do modelo de mineração que satisfazem esses critérios.  
  
 **Para obter mais informações: ** [Teste e validação &#40;Mineração de dados&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opções  
 **Condições**  
 Uma grade que contém colunas nas quais são especificadas condições para as colunas da tabela selecionada na caixa de diálogo **Filtro de Conjunto de Dados** .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**E/ou**|Clique para especificar se o operador AND ou OR deve ser aplicado à condição desta linha. Esses valores só ficam disponíveis depois que você seleciona uma coluna da lista **Coluna da Estrutura de Mineração** .|  
|**Coluna de Estrutura de Mineração**|Clique para selecionar uma coluna na lista de colunas contidas na tabela selecionada na fonte de dados na caixa de diálogo **Filtro de Conjunto de Dados** .|  
|**Operador**|Selecione um operador da lista. Os operadores que estão disponíveis dependem do tipo de dados da coluna.<br /><br /> Se a coluna contiver valores discretos, apenas os seguintes operadores estarão disponíveis:<br /><br /> = (igual a), <> (diferente de), IS NOT NULL, IS NULL.<br /><br /> Se a coluna contiver valores contínuos, os operadores para as operações maior que e menor que também serão suportados.|  
|**Valor**|Digite um valor a ser usado como uma condição.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas de teste e validação e instruções &#40;mineração de dados&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Designer de gráfico de precisão de mineração &#40;mineração de dados&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  
