---
title: Painel de consulta (exibição de previsão do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.prediction.query.f1
ms.assetid: fdeec72e-d0bd-4453-9eaa-46436e4d6edc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6bfb0a0c4e8284173a102b034a8b19457340a286
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070522"
---
# <a name="query-pane-mining-model-prediction-view"></a>Painel Consulta (Exibição da Previsão do Modelo de Mineração)
  O painel **Consulta** exibe as instruções DMX (extensões DMX) criadas pelo Construtor de Consultas de Previsão. Você pode modificar as instruções e, depois, clicar no botão **Alternar para a exibição de resultado da consulta** para retornar os resultados. Se você retornar à exibição de **Design** , quaisquer alterações efetuadas na instrução serão perdidas.  
  
 **Para obter mais informações:** [extensões de Data Mining &#40;instruções de manipulação de dados do DMX&#41;](/sql/dmx/dmx-statements-data-manipulation), [crie uma consulta DMX no SQL Server Management Studio](data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
## <a name="options"></a>Opções  
 **Alternar para a exibição de resultado da consulta**  
 Clique para mudar entre os painéis **Design**, **Consulta**e **Resultado** . A consulta é executada ao alternar para o painel **Resultado** .  
  
 **Salvar o resultado da consulta**  
 Abre a caixa de diálogo **Salvar Resultado da Consulta de Mineração de Dados** .  
  
 **Consulta singleton**  
 Permite que você crie uma consulta singleton, na qual você fornecerá os dados de entrada diretamente na consulta em vez de fornecer uma referência para a tabela de valores de entrada. A tabela **Selecionar Tabela(s) de Entrada** será substituída por uma tabela **Entrada de Consultas Singleton** . A consulta de previsão atual será perdida se você alternar para uma consulta singleton.  
  
 **Atualizar resultados de consulta**  
 Processa novamente a consulta de previsão. Isso está habilitado apenas no painel **Resultado** .  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces de consulta de mineração de dados](data-mining/data-mining-query-tools.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](/sql/dmx/data-mining-extensions-dmx-statements)   
 [Construtor de Consultas de &#40;de mineração de dados de previsão&#41;](prediction-query-builder-data-mining.md)  
  
  
