---
title: Especifique a caixa de diálogo (gráfico de precisão de mineração) de mapeamento de coluna | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.coltotablecolmapping.f1
ms.assetid: 68e9e2d2-173f-4363-a515-fc60bfee3af0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0d0cfd668ae945cd54df11fe6110ce59d088980
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62746209"
---
# <a name="specify-column-mapping-dialog-box-mining-accuracy-chart"></a>Caixa de diálogo Especificar Mapeamento de Coluna (gráfico de precisão de mineração)
  Use a guia **Especificar Mapeamento de Coluna** para selecionar tabelas de uma fonte de dados externa e mapear as colunas para um modelo de mineração de dados. É possível usar os dados externos para testar a precisão de um modelo de mineração e mostrar os resultados no gráfico de precisão.  
  
 **Para obter mais informações, consulte:** [Teste e validação &#40;Mineração de dados&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opções  
 **Estrutura de mineração**  
 Exibe a estrutura de mineração selecionada que contém o modelo que será testado.  
  
 **Selecionar estrutura**  
 Clique para abrir a caixa de diálogo **Selecionar Estrutura de Mineração** e selecione uma estrutura de mineração diferente.  
  
 **Selecione a tabela de entrada**  
 Exibe as tabelas de entrada selecionadas que são usadas para gerar o gráfico de comparação de precisão. Selecione a tabela que contém os dados de teste que você deseja usar para testar a precisão dos modelos.  
  
> [!NOTE]  
>  Se o painel não contiver nenhuma tabela, clique em **Selecionar Tabela de Casos** para adicionar tabelas de uma exibição da fonte de dados.  
  
 **Remover tabela**  
 Remove a tabela selecionada. Este botão será desabilitado se nenhuma tabela tiver sido selecionada ou se nenhuma tabela for exibida na lista **Selecionar Tabelas de Entrada** .  
  
 **Selecionar tabela de casos**  
 Clique para abrir a caixa de diálogo **Selecionar Tabela** e selecione uma exibição da fonte de dados.  
  
 **Observação** Esse botão só será exibido se uma tabela de casos não tiver sido selecionada. Para habilitar o botão de modo que você possa selecionar uma tabela de casos diferente, limpe a lista selecionando todas as tabelas existentes e clicando em **Remover Tabela**.  
  
 **Selecionar tabela aninhada**  
 Abre a caixa de diálogo **Selecionar Tabela** . Esse botão só será exibido se uma tabela do casos tiver sido selecionada. Se a estrutura de mineração associada não contiver uma tabela aninhada, esse botão será desabilitado.  
  
 **Modificar junção**  
 Abre a caixa de diálogo **Especificar Junção Aninhada** . Esse botão só será ativado se a tabela aninhada for selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Teste e validação de tarefas e instruções &#40;mineração de dados&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Designer do gráfico de precisão de mineração &#40;mineração de dados&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  
