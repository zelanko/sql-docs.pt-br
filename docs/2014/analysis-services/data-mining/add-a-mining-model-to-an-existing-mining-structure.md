---
title: Adicionar um modelo de mineração a uma estrutura de mineração existente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], adding
- mining structures [Analysis Services], mining models
- adding mining models
ms.assetid: fcf72300-0674-4e73-a826-9b8eeffefbb5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b550291b06918cce7adb430b0b05d1f37018fd78
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086377"
---
# <a name="add-a-mining-model-to-an-existing-mining-structure"></a>Adicionar um modelo de mineração a uma estrutura de mineração existente
  É possível adicionar mais modelos de mineração a uma estrutura de mineração, após adicionar o modelo inicial. Cada modelo deve conter colunas que existam na estrutura, mas você pode definir de forma diferente o uso das colunas para cada modelo de mineração. Para obter mais informações sobre como definir colunas de modelos de mineração, consulte [Colunas do modelo de mineração](mining-model-columns.md).  
  
### <a name="to-add-a-mining-model-to-the-structure"></a>Para adicionar um modelo de mineração à estrutura  
  
1.  No item de menu **Modelo de Mineração** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione **Novo Modelo de Mineração**.  
  
     A caixa de diálogo **Novo Modelo de Mineração** é exibida.  
  
2.  Em **Nome do modelo**, digite um nome para o modelo de mineração novo.  
  
3.  Em **Nome do algoritmo**, selecione o algoritmo por meio do qual o modelo de mineração será construído.  
  
4.  Clique em **OK**.  
  
 Um novo modelo de mineração é exibido na guia **modelos de mineração** . O modelo usa as colunas padrão que existem na estrutura. Para obter mais informações sobre como modificar as colunas, consulte [Alterar as propriedades de um modelo de mineração](change-the-properties-of-a-mining-model.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções do modelo de mineração](mining-model-tasks-and-how-tos.md)  
  
  
