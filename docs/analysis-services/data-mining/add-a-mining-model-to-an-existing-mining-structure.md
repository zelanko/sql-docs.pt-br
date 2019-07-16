---
title: Adicionar um modelo de mineração a uma estrutura de mineração existente | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f8b995a5b3fb89956e690598c786dc0a09474021
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210222"
---
# <a name="add-a-mining-model-to-an-existing-mining-structure"></a>Adicionar um modelo de mineração a uma estrutura de mineração existente
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  É possível adicionar mais modelos de mineração a uma estrutura de mineração, após adicionar o modelo inicial. Cada modelo deve conter colunas que existam na estrutura, mas você pode definir de forma diferente o uso das colunas para cada modelo de mineração. Para obter mais informações sobre como definir colunas de modelos de mineração, consulte [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md).  
  
### <a name="to-add-a-mining-model-to-the-structure"></a>Para adicionar um modelo de mineração à estrutura  
  
1.  No item de menu **Modelo de Mineração** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione **Novo Modelo de Mineração**.  
  
     A caixa de diálogo **Novo Modelo de Mineração** é exibida.  
  
2.  Em **Nome do modelo**, digite um nome para o modelo de mineração novo.  
  
3.  Em **Nome do algoritmo**, selecione o algoritmo por meio do qual o modelo de mineração será construído.  
  
4.  Clique em **OK**.  
  
 Um modelo de mineração novo é exibido na guia **Modelos de Mineração** . O modelo usa as colunas padrão que existem na estrutura. Para obter mais informações sobre como modificar as colunas, consulte [Alterar as propriedades de um modelo de mineração](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
