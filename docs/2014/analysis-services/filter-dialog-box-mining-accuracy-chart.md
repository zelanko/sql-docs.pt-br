---
title: Caixa de diálogo (gráfico de precisão de mineração) filtro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71e884a9-7ec4-4459-a4c4-87f6c796d478
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 328ebd3f09037c3288450b75b4acd011481c40a6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009032"
---
# <a name="filter-dialog-box-mining-accuracy-chart"></a>Caixa de diálogo Filtro (gráfico de precisão de mineração)
  A caixa de diálogo **Filtro** o ajuda a criar condições que você pode aplicar em um conjunto de dados. O conjunto de dados pode ser um conjunto externo usado para teste ou os dados de caso usados para treinar um modelo de mineração. Essa caixa de diálogo ajuda a criar critérios que podem ser salvos como parte de critérios de filtragem mais complexos na caixa de diálogo **Filtro de Conjunto de Dados** ou na caixa de diálogo **Filtro de Modelos** .  
  
-   A caixa de diálogo **Filtro de Conjunto de Dados** está disponível na guia **Seleção de Entrada** do designer **Gráfico de Precisão de Mineração** .  
  
-   A caixa de diálogo **Filtro de Modelos** está disponível na guia **Modelos de Mineração** do Designer de Mineração de Dados.  
  
 Se estiver aplicando um filtro em um modelo de mineração, use primeiro a caixa de diálogo **Filtro de Modelos** para escolher uma tabela. Em seguida, use a caixa de diálogo **Filtro** para criar condições que só se aplicam à tabela selecionada.  
  
 Se estiver criando um filtro a ser aplicado em um conjunto de dados de teste externo, use primeiro a caixa de diálogo **Filtro de Conjunto de Dados** para escolher uma tabela na lista de tabelas em uma exibição da fonte de dados. Em seguida, use a caixa de diálogo **Filtro** para criar condições que só se aplicam à tabela selecionada.  
  
 Depois de criar um conjunto de condições que se aplicam a uma única tabela, [!INCLUDE[clickOK](../includes/clickok-md.md)]. As alterações feitas na caixa de diálogo **Filtro** são adicionadas automaticamente à expressão de filtro na caixa de diálogo pai, **Filtro de Conjunto de Dados** ou **Filtro de Modelos**.  
  
 Se você aplicar o filtro ao novo conjunto de dados, o modelo de mineração de dados existente será usado para avaliar somente os casos do conjunto de dados que satisfaçam as condições. No entanto, se você aplicar o filtro ao próprio modelo de mineração, a precisão do modelo será avaliada apenas para os casos do modelo de mineração que satisfazem esses critérios.  
  
 **Para obter mais informações:**  [Teste e validação &#40;Mineração de dados&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opções  
 **Condições**  
 Uma grade que contém colunas nas quais são especificadas condições para as colunas da tabela selecionada na caixa de diálogo **Filtro de Conjunto de Dados** .  
  
|Valor|Description|  
|-----------|-----------------|  
|**E/Ou**|Clique para especificar se o operador AND ou OR deve ser aplicado à condição desta linha. Esses valores só ficam disponíveis depois que você seleciona uma coluna da lista **Coluna da Estrutura de Mineração** .|  
|**Coluna de estrutura de mineração**|Clique para selecionar uma coluna na lista de colunas contidas na tabela selecionada na fonte de dados na caixa de diálogo **Filtro de Conjunto de Dados** .|  
|**Operador**|Selecione um operador da lista. Os operadores que estão disponíveis dependem do tipo de dados da coluna.<br /><br /> Se a coluna contiver valores discretos, apenas os seguintes operadores estarão disponíveis:<br /><br /> = (igual a), <> (diferente de), IS NOT NULL, IS NULL.<br /><br /> Se a coluna contiver valores contínuos, os operadores para as operações maior que e menor que também serão suportados.|  
|**Value**|Digite um valor a ser usado como uma condição.|  
  
## <a name="see-also"></a>Consulte também  
 [Teste e validação de tarefas e instruções &#40;mineração de dados&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Designer do gráfico de precisão de mineração &#40;mineração de dados&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  