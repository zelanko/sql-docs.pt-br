---
title: Filtro de conjunto de dados ou a caixa de diálogo de filtro de modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a9602174-b7e2-4e16-8ded-dfd8eb9264d7
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 85986f7f73a96ce0fc2286ad8f9377df1d53845c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008301"
---
# <a name="data-set-filter-or-model-filter-dialog-box"></a>Caixa de Diálogo Filtro de Conjunto de Dados ou Filtro de Modelo
  Esta caixa de diálogo o ajuda a construir os filtros que você pode aplicar a um conjunto de dados.  O conjunto de dados pode ser um conjunto externo usado para teste ou os dados do caso para um modelo de mineração. O nome da caixa de diálogo irá mudar dependendo se o filtro for para um conjunto de dados externo ou para um modelo de mineração.  
  
 Se você aplica o filtro para um novo conjunto de dados, o modelo de mineração de dados é avaliado usando somente aqueles casos no conjunto de dados que atendam as condições. Se você aplica o filtro para o próprio modelo de mineração, o modelo será treinado e testado usando somente os casos, no conjunto de dados de teste existente, que atendam os critérios do filtro.  
  
-   A caixa de diálogo **Filtro de Conjunto de Dados** está disponível na guia **Seleção de Entrada** do designer **Gráfico de Precisão de Mineração** .  
  
-   A caixa de diálogo **Filtrar Modelos** está disponível na guia **Modelos de Mineração** do Designer de Data Mining.  
  
-   A grade **Condições** contém colunas nas quais você pode especificar uma tabela ou nome de coluna, um operador e valores de destino. Usando esta grade você está essencialmente criando uma cláusula WHERE.  
  
> [!TIP]  
>  Para testar a precisão em um subconjunto dos dados originais de treinamento, é possível adicionar a exibição de fonte de dados que foi utilizada para definir o conjunto de treinamento como dados externos de teste e então adicionar as condições na grade **Filtro de Conjunto de Dados**.  
  
 **Para obter mais informações:**  [Teste e validação &#40;Mineração de dados&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opções  
 **Condições**  
 Exibe nomes de tabela, seguidos por nomes de coluna com condições.  
  
|Valor|Description|  
|-----------|-----------------|  
|**E/Ou**|Escolha um operador para unir múltiplas condições.|  
|**Coluna de estrutura de mineração**|Clique para selecionar uma fonte de dados e em seguida clique em linhas sucessivas na grade para adicionar colunas da fonte de dados.<br /><br /> A primeira linha na grade especifica a exibição da fonte de dados. Após você selecionar uma exibição de fonte de dados, a **Coluna de Estrutura de Mineração** exibirá um ícone de tabela e o campo **Valor** vai mostrar as combinações de todos os critérios que você definiu para esta fonte de dados.<br /><br /> Após você ter selecionado uma fonte de dados, a caixa **Coluna de Estrutura de Mineração** apresentará um lista suspensa com as colunas individuais da fonte.|  
|**Operador**|Selecione um operador da lista.|  
|**Value**|Para tabelas, o campo **Valor** exibe a combinação de todos os filtros aplicados à fonte de dados. É possível também clicar no botão **(…)** do lado direito da caixa de texto, para abrir a caixa de diálogo **Filtro** e criar uma condição.|  
  
 **Expression**  
 Exibe o conjunto de critérios que você criou usando a grade.  
  
 **Editar consulta**  
 Altera o modo de edição de filtro de forma que você pode digitar uma expressão de filtro diretamente na caixa de texto **Expressão** .  
  
> [!NOTE]  
>  Após você ter feito alterações manuais na expressão do filtro, não será possível retornar ao modo de edição de grade, mesmo após você salvar a expressão na caixa **Expressão do Filtro** na guia **Seleção de Entrada** . Se você deseja criar uma expressão usando a grade, deve excluir a expressão do filtro existente e reiniciar.  
  
 **Reverter edições de consulta**  
 Restaura a grade a seu estado anterior e cancela qualquer alteração que você fez à expressão do filtro.  
  
## <a name="see-also"></a>Consulte também  
 [Teste e validação de tarefas e instruções &#40;mineração de dados&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Designer do gráfico de precisão de mineração &#40;mineração de dados&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  