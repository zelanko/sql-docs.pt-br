---
title: Guia de seleção (exibição de gráfico de precisão de mineração) de entrada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.columnmapping.f1
ms.assetid: f8b1193c-5c86-4c7e-8e35-158d293184fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3fb4771c7345eb270e91a377d2755a25606f9a93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080420"
---
# <a name="input-selection-tab-mining-accuracy-chart-view"></a>Guia de seleção de entrada (exibição de gráfico de precisão de mineração)
  Use a guia **Seleção de Entrada** do designer **Gráfico de Precisão de Mineração** para especificar a fonte dos dados que são usados para testar o modelo e criar o gráfico de precisão.  
  
 **Para obter mais informações, consulte:** [Teste e validação &#40;Mineração de dados&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opções  
 **Sincronizar Colunas**  **e Valores de Previsão**  
 Selecione para coordenar os atributos previsíveis na grade de forma que, mesmo que eles tenham um nome diferente, serão derivados da mesma coluna previsível de estrutura de mineração durante o treinamento do modelo.  
  
 **Observação** Esta opção é selecionada por padrão. Você só deve desmarcar esta caixa para os casos nos quais você sabe que as duas colunas da estrutura de mineração derivam da mesma fonte relacional ou multidimensional subjacente e que estas colunas contêm os mesmos estados ou foram tornadas discretas da mesma maneira.  
  
 **Selecione as colunas do modelo de mineração previsíveis para mostrar no gráfico de comparação**  
 Uma grade que contém colunas para controlar que modelos são incluídos no gráfico de comparação de precisão e como eles são usados neste gráfico.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Mostrar**|Selecione no modelo de mineração a caixa próxima ao nome de cada coluna previsível que você deseja exibir no gráfico.<br /><br /> Se o gráfico é muito complexo para ser visualizado facilmente, desmarque a caixa próxima de uma ou mais colunas para simplificar o gráfico.<br /><br /> Observação: Você não pode criar um gráfico de precisão, a menos que pelo menos uma coluna está selecionada.|  
|**Modelo de mineração**|Lista os modelos de mineração que estão contidos na estrutura de mineração.|  
|**Nome da coluna previsível**|Selecione uma coluna previsível que esteja contida nos modelos de mineração que são usados para criar o gráfico de comparação de precisão.|  
|**Prever valor**|Selecione um valor para a coluna previsível. Se você deixar em branco, o gráfico de comparação de precisão prevê o melhor desempenho do modelo para todos os estados da coluna previsível.|  
  
 **Selecione o conjunto de dados a ser usado para gráfico de precisão**  
 Um grupo de opção que contém três opções para especificar dados de teste de exatidão.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Usar casos de teste do modelo de mineração**|Use o conjunto de teste que estava criado quando você dividiu a estrutura de mineração e aplique o filtro que esta definido no modelo. Para obter informações sobre filtros de modelo, consulte [Filters for Mining Models &#40;Analysis Services - Data Mining&#41;](data-mining/mining-models-analysis-services-data-mining.md)|  
|**Usar casos de teste da estrutura de mineração**|Use o conjunto de teste que foi criado quando você dividiu a estrutura de mineração.|  
|**Especificar um conjunto de dados diferente**|Especifique uma tabela de uma exibição da fonte de dados existente para usar como conjunto de dados de teste.|  
  
## <a name="filtering-options"></a>Filtrar opções  
 Se você selecionar a opção **Especificar um conjunto de dados diferente**, poderá definir uma exibição de fonte de dados e criar filtros para aplicar aos dados. Ao criar um filtro, você está criando uma cláusula WHERE na consulta que retorna os dados de teste da exibição de fonte de dados.  
  
 **Observação** Você não pode especificar um filtro no modelo de mineração usando a guia **Seleção de Entrada** . Para criar um filtro de modelo, clique na guia **Modelos de Mineração** e edite as propriedades do modelo.  
  
 Se você não criou um conjunto de controle para teste quando criou a estrutura de mineração, você pode selecionar esta opção e então especificar a exibição de fonte de dados original como um conjunto de teste. Usando esta solução alternativa, você também pode definir filtros no conjunto de dados original.  
  
 **Especificar Mapeamento de coluna**  
 Abre a caixa de diálogo **Especificar Mapeamento de Coluna** em que você seleciona a fonte de dados, especifica caso e tabelas aninhadas e associa colunas de dados externos às colunas da estrutura de mineração.  
  
 Para obter mais informações, consulte [Caixa de diálogo Especificar Mapeamento de Coluna &#40;gráfico de precisão de mineração&#41;](specify-column-mapping-dialog-box-mining-accuracy-chart.md).  
  
 **Expressão de filtro**  
 Exibe a condição do filtro que você construiu usando os editores de filtro.  
  
 **Abrir Editor de filtro**  
 Abra a caixa de diálogo **Filtro de Conjunto de Dados** que permite selecionar tabelas externas e definir condições nas colunas de tabela de caso e, a caixa de diálogo **Filtro** que o ajuda a criar condições que se aplicam para determinadas colunas na tabela selecionada ou para colunas em tabelas aninhadas.  
  
## <a name="see-also"></a>Consulte também  
 [Teste e validação de tarefas e instruções &#40;mineração de dados&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Designer do gráfico de precisão de mineração &#40;mineração de dados&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [Aplicar um filtro a um modelo de mineração](data-mining/apply-a-filter-to-a-mining-model.md)   
 [Filtros para modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](data-mining/mining-models-analysis-services-data-mining.md)  
  
  
