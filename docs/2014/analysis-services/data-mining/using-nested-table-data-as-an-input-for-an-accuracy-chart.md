---
title: Usando dados de tabela aninhada como uma entrada para um gráfico de precisão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services], nested tables
- Mining Accuracy Chart [Analysis Services], input tables
- nested tables
- adding nested tables
ms.assetid: 162e0686-ada3-4dd3-9151-9589926e6613
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a6e6d0ade60dbb42fca9bda9ee78f4dbb50064a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082728"
---
# <a name="using-nested-table-data-as-an-input-for-an-accuracy-chart"></a>Usando dados de uma tabela aninhada como entrada para um gráfico de precisão
  Quando você testar a precisão de um modelo de mineração usando dados externos, se o modelo de mineração contiver tabelas aninhadas, os dados externos também deverão contar uma tabela de casos e uma tabela aninhada associada.  
  
 Este tópico descreve como trabalhar com tabelas aninhadas usadas para testar modelos, como mapear tabelas de casos e aninhadas no modo e nos dados externos e como aplicar um filtro a uma tabela aninhada.  
  
 Ao trabalhar com tabelas aninhadas, lembre-se destas dicas:  
  
-   Se você selecionar a opção **Usar casos de teste do modelo de mineração** ou **Usar casos de teste da estrutura de mineração**, não será necessário especificar uma tabela de casos ou aninhada. Com essas opções, a definição dos dados de teste é armazenada na estrutura de mineração e os dados de teste serão selecionados automaticamente quando você criar o gráfico de precisão.  
  
-   Se já existir uma relação entre a tabela de caso e a tabela aninhada na fonte de dados, as colunas da estrutura de mineração serão mapeadas automaticamente para as colunas que têm o mesmo nome na tabela de entrada.  
  
-   Não será possível selecionar uma tabela aninhada até que você especifique a tabela de casos. Além disso, você não pode especificar uma tabela aninhada como uma entrada, a menos que o modelo de mineração também use uma estrutura de tabela de casos e tabela aninhada.  
  
### <a name="use-a-nested-table-as-input-to-an-accuracy-chart"></a>Usar uma tabela aninhada como entrada para um gráfico de precisão  
  
1.  Clique duas vezes na estrutura de mineração para abri-la no Designer de Mineração de Dados.  
  
2.  Selecione a guia **Gráfico de Precisão da Mineração** e, em seguida, selecione a guia **Seleção de Entrada** .  
  
3.  Em **selecionar conjunto de dados a ser usado para o gráfico de precisão**, selecione a opção **especificar um conjunto de dados diferente**.  
  
4.  Clique no botão procurar **(...)** para escolher o conjunto de dados externos em uma lista de exibições da fonte de dados no servidor atual.  
  
5.  Clique em **Selecionar Tabela de Casos**. Na caixa de diálogo **Selecionar Tabela** , escolha a tabela na exibição da fonte de dados que contém os dados do caso e, em seguida, clique em **OK**.  
  
6.  Clique em **Selecionar Tabela Aninhada**. Na caixa de diálogo **Selecionar Tabela** , selecione a tabela que contém os dados aninhados e, em seguida, clique em **OK**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Se você precisar modificar a relação entre a tabela aninhada e a tabela de casos, clique em **Modificar Junção** para abrir a caixa de diálogo **Criar Relação** .  
  
## <a name="see-also"></a>Consulte Também  
 [Escolher e mapear dados de teste de modelo](choose-and-map-model-testing-data.md)   
 [Aplicar filtros a dados de testes de modelo](apply-filters-to-model-testing-data.md)  
  
  
