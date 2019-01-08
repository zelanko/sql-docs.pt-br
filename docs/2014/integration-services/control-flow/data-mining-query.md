---
title: Consulta de Mineração de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquery.f1
ms.assetid: 948e358a-6245-429f-82c7-4cedc5e048fd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 95ce2aa24b844c77406b5286eac31b75cdb6fd35
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771128"
---
# <a name="data-mining-query"></a>Consulta de mineração de dados
  O painel de design contém o construtor de consultas de previsão de mineração de dados, que pode ser usado para construir consultas de previsão de mineração de dados. Você pode criar tanto consultas de previsão baseadas em tabelas de entrada como consultas de previsão singleton. Alterne para a exibição de resultados para executar a consulta e exibir os resultados. A exibição de consulta exibe a consulta DMX (Data Mining Extensions) criada pelo construtor de consultas de previsão.  
  
## <a name="options"></a>Opções  
 Botão para alternar a exibição  
 Clique em um ícone para alternar entre o painel de design e o painel de consulta. Por padrão, é aberto o painel de design.  
  
 Para mudar para o painel de design, clique no ícone ![ícone Design](../media/ssis-designicon.gif "ícone Design").  
  
 Para mudar para o painel de consulta, clique no ícone ![ícone SQL](../media/ssis-queryicon.gif "ícone SQL").  
  
 **Modelo de mineração**  
 Exibe o modelo de mineração selecionado no qual você deseja basear as previsões.  
  
 **Selecionar Modelo**  
 Abre a caixa de diálogo **Selecionar Modelo de Mineração** .  
  
 **Colunas de Entrada**  
 Exibe as colunas de entrada selecionadas usadas para gerar as previsões.  
  
 **Origem**  
 Selecione a origem que contém o campo a ser usado para a coluna da lista suspensa. Você pode usar o modelo de mineração selecionado na tabela **Modelo de Mineração** , a tabela de entrada selecionada na tabela **Selecionar Tabela(s) de Entrada** , uma função de previsão ou uma expressão personalizada.  
  
 As colunas podem ser arrastadas das tabelas que contêm o modelo de mineração e colunas de entrada para a célula.  
  
 **Campo**  
 Selecione uma coluna na lista de colunas derivada da tabela de origem. Se você selecionou **Função de Previsão** em **Origem**, esta célula conterá uma lista suspensa das funções de previsão disponíveis para o modelo de mineração selecionado.  
  
 **Alias**  
 Nome da coluna retornado pelo servidor.  
  
 **Mostrar**  
 Selecione para retornar a coluna ou para usar só a coluna na cláusula WHERE.  
  
 **Agrupar**  
 Use com a coluna **E/ou** para agrupar expressões. Por exemplo, (expr1 OU expr2) E expr3.  
  
 **E/ou**  
 Use para criar uma consulta lógica. Por exemplo, (expr1 OU expr2) E expr3.  
  
 **Critérios/Argumento**  
 Especifique uma condição ou expressão de usuário que se aplica à coluna. As colunas podem ser arrastadas das tabelas que contêm o modelo de mineração e colunas de entrada para a célula.  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de consulta de mineração de dados](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](/sql/dmx/data-mining-extensions-dmx-statements)  
  
  
