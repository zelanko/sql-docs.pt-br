---
title: Altere o valor de tempo limite para consultas de mineração de dados | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e6286a931c0e1ad27a99462853c3b8dfe6de36bc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>Alterar o valor do tempo limite de consultas de mineração de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Às vezes, quando é criado um gráfico de comparação de precisão ou é executada uma consulta de previsão, a geração de todos os dados necessários para a previsão pode demorar. Para evitar que o tempo limite da consulta seja ultrapassado, você pode alterar o valor que controla o tempo em que o servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permanecerá em espera para concluir uma consulta.  
  
 O valor padrão é 15, porém se seus modelos são complexos ou se a fonte de dados for muito grande, este valor poderá ser insuficiente. Se necessário, você pode aumentar o valor o bastante para permitir tempo suficiente para o processamento. Por exemplo, se você definir o **Tempo Limite da Consulta** como 600, a consulta poderá continuar em execução por até 10 minutos.  
  
 Para obter mais informações sobre consultas de previsão, consulte [Tarefas e instruções de consulta de Data Mining](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md).  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>Configure o valor do tempo limite de consultas de mineração de dados  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no menu **Ferramentas** , selecione **Opções**.  
  
2.  No painel **Opções** , abra **Designers do Business Intelligence**.  
  
3.  Clique na caixa de texto **Tempo Limite da Consulta** e digite um valor para a quantidade de segundos.  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais e tarefas de consulta de mineração de dados](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
