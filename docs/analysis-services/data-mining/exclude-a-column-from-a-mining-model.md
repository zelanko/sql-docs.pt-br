---
title: Excluir uma coluna de um modelo de mineração | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 937a28d77b8398855773cb1c11799de6112a04fa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="exclude-a-column-from-a-mining-model"></a>Excluir uma coluna de um modelo de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ao criar um novo modelo de mineração, talvez você não queira usar todas as colunas existentes na estrutura de mineração em que o modelo é baseado. Por exemplo, talvez você tenha adicionado uma coluna de nome de cliente para detalhamento, mas não deseje usá-la para modelagem. Ou você pode decidir criar várias cópias de uma coluna com discretizações diferentes e usar apenas uma das cópias em cada modelo, ignorando as demais. Você também pode adicionar seletivamente colunas de entrada em vários modelos diferentes para ver como a variável adicionada afeta a coluna de saída.  
  
 Você não precisa criar uma nova estrutura de mineração para cada combinação de colunas; basta sinalizar uma coluna como não sendo usado em um modelo específico.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>Para excluir uma coluna de um modelo de mineração  
  
1.  Na guia **Modelos de Mineração** no Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione a célula que corresponde à coluna que deseja excluir no modelo de mineração apropriado.  
  
2.  Selecione **Ignorar** na caixa de listagem suspensa.  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais e tarefas do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
