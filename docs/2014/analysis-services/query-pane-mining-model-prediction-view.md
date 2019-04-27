---
title: Consultar o painel (exibição de previsão do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.prediction.query.f1
ms.assetid: fdeec72e-d0bd-4453-9eaa-46436e4d6edc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 316b82f15c28a13a2a04bdd81683d2fdf83707bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748368"
---
# <a name="query-pane-mining-model-prediction-view"></a>Painel Consulta (Exibição da Previsão do Modelo de Mineração)
  O painel **Consulta** exibe as instruções DMX (extensões DMX) criadas pelo Construtor de Consultas de Previsão. Você pode modificar as instruções e, depois, clicar no botão **Alternar para a exibição de resultado da consulta** para retornar os resultados. Se você retornar à exibição de **Design** , quaisquer alterações efetuadas na instrução serão perdidas.  
  
 **Para obter mais informações:** [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](/sql/dmx/dmx-statements-data-manipulation), [criar uma consulta DMX no SQL Server Management Studio](data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
## <a name="options"></a>Opções  
 **Alterne para a exibição de resultado de consulta**  
 Clique para mudar entre os painéis **Design**, **Consulta**e **Resultado** . A consulta é executada ao alternar para o painel **Resultado** .  
  
 **Salvar o resultado da consulta**  
 Abre a caixa de diálogo **Salvar Resultado da Consulta de Mineração de Dados** .  
  
 **Consulta singleton**  
 Permite que você crie uma consulta singleton, na qual você fornecerá os dados de entrada diretamente na consulta em vez de fornecer uma referência para a tabela de valores de entrada. A tabela **Selecionar Tabela(s) de Entrada** será substituída por uma tabela **Entrada de Consultas Singleton** . A consulta de previsão atual será perdida se você alternar para uma consulta singleton.  
  
 **Atualizar resultados de consulta**  
 Processa novamente a consulta de previsão. Isso está habilitado apenas no painel **Resultado** .  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de consulta de mineração de dados](data-mining/data-mining-query-tools.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](/sql/dmx/data-mining-extensions-dmx-statements)   
 [Construtor de consultas de previsão &#40;mineração de dados&#41;](prediction-query-builder-data-mining.md)  
  
  
