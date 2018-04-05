---
title: Altere o valor de tempo limite para consultas de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- time-out
ms.assetid: f1add4bc-e882-440a-a98b-333cfa274c3e
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cb73246a4187ff8b8360c4e2eb37f6eaacd44dd3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>Alterar o valor do tempo limite de consultas de mineração de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Quando você cria um gráfico de comparação de precisão ou executa uma consulta de previsão, às vezes, ele pode levar muito tempo para gerar todos os dados necessários para a previsão. Para evitar que o tempo limite da consulta seja ultrapassado, você pode alterar o valor que controla o tempo em que o servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permanecerá em espera para concluir uma consulta.  
  
 O valor padrão é 15, porém se seus modelos são complexos ou se a fonte de dados for muito grande, este valor poderá ser insuficiente. Se necessário, você pode aumentar o valor o bastante para permitir tempo suficiente para o processamento. Por exemplo, se você definir o **Tempo Limite da Consulta** como 600, a consulta poderá continuar em execução por até 10 minutos.  
  
 Para obter mais informações sobre consultas de previsão, consulte [Tarefas e instruções de consulta de Data Mining](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md).  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>Configure o valor do tempo limite de consultas de mineração de dados  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no menu **Ferramentas** , selecione **Opções**.  
  
2.  No painel **Opções** , abra **Designers do Business Intelligence**.  
  
3.  Clique na caixa de texto **Tempo Limite da Consulta** e digite um valor para a quantidade de segundos.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções de consulta de Data Mining](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
