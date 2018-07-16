---
title: Consultar o painel (exibição de previsão do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.prediction.query.f1
ms.assetid: fdeec72e-d0bd-4453-9eaa-46436e4d6edc
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ede17228e9dc21a170815ecc46900fd38ab7d978
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211776"
---
# <a name="query-pane-mining-model-prediction-view"></a>Painel Consulta (Exibição da Previsão do Modelo de Mineração)
  O painel **Consulta** exibe as instruções DMX (extensões DMX) criadas pelo Construtor de Consultas de Previsão. Você pode modificar as instruções e, depois, clicar no botão **Alternar para a exibição de resultado da consulta** para retornar os resultados. Se você retornar à exibição de **Design** , quaisquer alterações efetuadas na instrução serão perdidas.  
  
 **Para obter mais informações:** [Instruções de manipulação de dados DMX &#40;extensões DMX&#41;](/sql/dmx/dmx-statements-data-manipulation), [Criar uma consulta DMX no SQL Server Management Studio](data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
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
  
  
