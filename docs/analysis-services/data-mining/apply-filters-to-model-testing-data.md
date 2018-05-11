---
title: Aplicar filtros de modelo de dados de teste | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 460bb381173e37c4cf4c31f358d89e915ea769bf
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="apply-filters-to-model-testing-data"></a>Aplicar filtros a dados de testes de modelo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando você especifica uma fonte de dados externa a ser usada para testar um modelo, pode opcionalmente aplicar um filtro para restringir os dados de entrada. Por exemplo, talvez queira testar o modelo especificamente para previsões sobre clientes com determinada faixa de renda.  
  
 Por exemplo, no cenário de email direcionado do Adventure Works, é possível criar uma expressão de filtro como esta em ProspectiveBuyer, que é a tabela contendo os dados de teste, bem como restringir casos de teste por faixa de renda:  
  
 `[YearlyIncome] = '50000'`  
  
 O comportamento de filtros é um pouco diferente, dependendo se você está filtrando dados de treinamento do modelo ou um conjunto de dados de teste:  
  
-   Quando você define um filtro em um conjunto de dados de teste, cria uma cláusula WHERE nos dados de entrada. Se estiver filtrando um conjunto de dados de entrada usado para avaliar um modelo, a expressão de filtro será convertida em uma instrução Transact-SQL e aplicada à tabela de entrada quando o gráfico for criado. Como resultado, o número de casos de teste pode ser reduzido consideravelmente.  
  
-   Quando você aplica um filtro a um modelo de mineração, a expressão de filtro que você cria é convertida em uma instrução DMX (extensões DMX), e aplicada ao modelo individual. Portanto, quando você aplica um filtro a um modelo, somente um subconjunto dos dados originais é usado para treinar o modelo. Isso pode gerar problemas quando você filtra o modelo de treinamento com um conjunto de critérios, de forma que o modelo seja ajustado a determinado conjunto de dados e, depois, testa o modelo com outro conjunto de critérios.  
  
-   Se você definiu um conjunto de dados de teste ao criar a estrutura, os casos do modelo usados para treinamento incluirão apenas os casos que constam no conjunto de treinamento da estrutura de mineração **e** que atendam as condições do filtro. Portanto, quando você está testando um modelo e seleciona a opção **Usar casos de teste do modelo de mineração**, os casos de testes incluem somente os casos que estão no conjunto de testes da estrutura de mineração e que atendem às condições do filtro. Entretanto, se você não definiu um conjunto de dados de validação, os casos do modelo usados para testes incluirão todos os casos do conjunto de dados que atendam às condições de filtro  
  
-   As condições de filtro que você aplica a um modelo também afetam as consultas de detalhamento nos casos do modelo.  
  
 Em suma, quando você testa vários modelos, mesmo que todos os modelos se baseiem na mesma estrutura de mineração, lembre-se de que os modelos potencialmente usam diferentes subconjuntos de dados para treinamentos e testes. Isso pode ter os seguintes efeitos em gráficos de precisão:  
  
-   O número total de casos nos conjuntos de testes varia entre os modelos testados.  
  
-   Os percentuais de cada modelo podem não estar alinhados no gráfico quando os modelos usam diferentes subconjuntos de dados de treinamento ou dados de teste.  
  
 Para determinar se um modelo contém um filtro predefinido que possa afetar os resultados, você pode procurar a propriedade **Filter** no painel **Propriedade** ou consultar o modelo usando os conjuntos de linhas do esquema de mineração de dados. Por exemplo, esta consulta retorna o texto de filtro para o modelo especificado:  
  
 `SELECT [FILTER] FROM $system.DMSCHEMA_MINING_MODELS WHERE MODEL_NAME = 'name of model’`  
  
> [!WARNING]  
>  Se desejar remover o filtro de um modelo de mineração existente ou alterar as condições do filtro, reprocesse o modelo de mineração.  
  
 Para obter mais informações sobre os tipos de filtros que você pode aplicar e como as expressões de filtro são avaliadas, consulte [Sintaxe de filtro de modelo e exemplos &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md).  
  
### <a name="create-a-filter-on-external-testing-data"></a>Criar um filtro em dados de testes externos  
  
1.  Clique duas vezes na estrutura de mineração que contém o modelo a ser testado, para abrir o Designer de Mineração de Dados.  
  
2.  Selecione a guia **Gráfico de Precisão da Mineração** e, em seguida, selecione a guia **Seleção de Entrada** .  
  
3.  Na guia **Seleção de Entrada** , em **Selecionar conjunto de dados a ser usado para Gráfico de Precisão**, selecione a opção **Especificar um conjunto de dados diferente**.  
  
4.  Clique no botão Procurar **(…)** para abrir uma caixa de diálogo e escolha o conjunto de dados externo.  
  
5.  Escolha a tabela de caso e adicione uma tabela aninhada, caso necessário. Mapeie colunas no modelo para colunas no conjunto de dados externo, caso necessário. Feche a caixa de diálogo **Especificar Mapeamento de Coluna** para salvar a definição de tabela de origem.  
  
6.  Clique em **Abrir Editor de Filtro** para definir um filtro para o conjunto de dados.  
  
     A caixa de diálogo **Filtro do Conjunto de Dados** se abre. Se a estrutura contiver uma tabela aninhada, você poderá criar um filtro em duas partes. Primeiro, defina as condições na tabela de casos, utilizando a caixa de diálogo **Filtro do Conjunto de Dados** e, em seguida, defina as condições nas linhas aninhadas utilizando a caixa de diálogo **Filtrar** .  
  
7.  Na caixa de diálogo **Filtro do Conjunto de Dados** , clique na linha superior da grade, em **Coluna da Estrutura de Mineração**, e selecione uma tabela ou coluna da lista.  
  
     Se a exibição da fonte de dados contiver várias tabelas ou uma tabela aninhada, selecione o nome da tabela primeiro. Caso contrário, você pode selecionar colunas diretamente na tabela de casos.  
  
     Adicione uma linha nova para cada coluna que você deseja filtrar.  
  
8.  Use **Operador**e as colunas **Valor** para definir como a coluna é filtrada.  
  
     **Nota** Digite os valores sem usar aspa.  
  
9. Clique na caixa de texto **E/Ou** e selecione um operador lógico para definir como combinar várias condições.  
  
10. Se desejar, clique no botão Procurar **(…)** à direita da caixa de texto **Valor** para abrir a caixa de diálogo **Filtrar** e defina as condições na tabela aninhada ou nas colunas da tabela de casos individuais.  
  
11. Verifique se as condições de filtro atendidas estão corretas exibindo o texto no painel **Expressão** .  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     A condição de filtro é aplicada à fonte de dados quando você cria o gráfico de precisão.  
  
## <a name="see-also"></a>Consulte também  
 [Escolher e mapear dados de testes modelo](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [Usando dados tabela aninhada como entrada para um gráfico de precisão](../../analysis-services/data-mining/using-nested-table-data-as-an-input-for-an-accuracy-chart.md)   
 [Escolha um tipo de gráfico de precisão e definir opções de gráfico](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
