---
title: "Criar uma dimensão de mineração de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], dimensions
ms.assetid: 9f0c39e5-3516-43ab-b203-f3f6dbcff89a
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 238af959c27daaf75415cf913fddb823f6927c85
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-data-mining-dimension"></a>Criar uma dimensão de mineração de dados
  Se a sua estrutura de mineração é baseada em um cubo OLAP, você pode criar uma dimensão que possua o conteúdo do modelo de mineração. É possível incorporar a dimensão de volta no cubo de origem.  
  
 Você também pode procurar a dimensão, usá-la para explorar os resultados do modelo, ou consultar a dimensão usando MDX.  
  
### <a name="to-create-a-data-mining-dimension"></a>Para criar uma dimensão de mineração de dados  
  
1.  No Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], selecione a guia **Estrutura de Mineração** ou a guia **Modelos de Mineração** .  
  
2.  No menu **Modelo de Mineração** , selecione **Criar uma Dimensão de Mineração de Dados**.  
  
     A caixa de diálogo **Criar Dimensão de Mineração de Dados** é exibida.  
  
3.  Na lista **Nome do modelo** da caixa de diálogo **Criar Dimensão de Mineração de Dados** , selecione um modelo de mineração OLAP.  
  
4.  Na caixa **Nome da dimensão** , digite um nome para a nova dimensão de mineração de dados.  
  
5.  Se você quiser criar um cubo que inclua a nova dimensão de mineração de dados, selecione **Criar cubo**. Após selecionar **Criar cubo**, você pode digitar um nome novo para o cubo.  
  
6.  Clique em **OK**.  
  
     A dimensão de mineração de dados é criada e adicionada à pasta **Dimensões** no Gerenciador de Soluções. Se você selecionou **Criar cubo**, um cubo novo também será criado e adicionado à pasta **Cubos** .  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções da estrutura de mineração](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
