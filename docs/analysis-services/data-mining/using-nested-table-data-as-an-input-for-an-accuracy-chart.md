---
title: Usando dados de tabela aninhada como entrada para um gráfico de precisão | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d4217962e6bb899cbf2a838c5214eb35bb576be0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209568"
---
# <a name="using-nested-table-data-as-an-input-for-an-accuracy-chart"></a>Usando dados de uma tabela aninhada como entrada para um gráfico de precisão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando você testar a precisão de um modelo de mineração usando dados externos, se o modelo de mineração contiver tabelas aninhadas, os dados externos também deverão contar uma tabela de casos e uma tabela aninhada associada.  
  
 Este tópico descreve como trabalhar com tabelas aninhadas usadas para testar modelos, como mapear tabelas de casos e aninhadas no modo e nos dados externos e como aplicar um filtro a uma tabela aninhada.  
  
 Ao trabalhar com tabelas aninhadas, lembre-se destas dicas:  
  
-   Se você selecionar a opção **Usar casos de teste do modelo de mineração** ou **Usar casos de teste da estrutura de mineração**, não será necessário especificar uma tabela de casos ou aninhada. Com essas opções, a definição dos dados de teste é armazenada na estrutura de mineração e os dados de teste serão selecionados automaticamente quando você criar o gráfico de precisão.  
  
-   Se já existir uma relação entre a tabela de caso e a tabela aninhada na fonte de dados, as colunas da estrutura de mineração serão mapeadas automaticamente para as colunas que têm o mesmo nome na tabela de entrada.  
  
-   Não será possível selecionar uma tabela aninhada até que você especifique a tabela de casos. Além disso, você não pode especificar uma tabela aninhada como uma entrada, a menos que o modelo de mineração também use uma estrutura de tabela de casos e tabela aninhada.  
  
### <a name="use-a-nested-table-as-input-to-an-accuracy-chart"></a>Usar uma tabela aninhada como entrada para um gráfico de precisão  
  
1.  Clique duas vezes na estrutura de mineração para abri-la no Designer de Mineração de Dados.  
  
2.  Selecione a guia **Gráfico de Precisão da Mineração** e, em seguida, selecione a guia **Seleção de Entrada** .  
  
3.  Em **Selecionar conjunto de dados a ser usado para o Gráfico de Precisão**, selecione a opção **Especificar um conjunto de dados diferente**.  
  
4.  Clique no botão Procurar **(...)**  para escolher o conjunto de dados externos de uma lista de exibições da fonte de dados no servidor atual.  
  
5.  Clique em **Selecionar Tabela de Casos**. Na caixa de diálogo **Selecionar Tabela** , escolha a tabela na exibição da fonte de dados que contém os dados do caso e, em seguida, clique em **OK**.  
  
6.  Clique em **Selecionar Tabela Aninhada**. Na caixa de diálogo **Selecionar Tabela** , selecione a tabela que contém os dados aninhados e, em seguida, clique em **OK**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Se você precisar modificar a relação entre a tabela aninhada e a tabela de casos, clique em **Modificar Junção** para abrir a caixa de diálogo **Criar Relação** .  
  
## <a name="see-also"></a>Consulte também  
 [Escolher e mapear dados de testes modelo](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [Aplicar filtros a dados de testes de modelo](../../analysis-services/data-mining/apply-filters-to-model-testing-data.md)  
  
  
