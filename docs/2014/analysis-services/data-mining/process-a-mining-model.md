---
title: Processar um modelo de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], processing
ms.assetid: c2204472-c500-47a5-9afa-7ce2ca78b233
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 649aa722e67e8cfaf9986c003a965c5aaf564684
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163467"
---
# <a name="process-a-mining-model"></a>Processar um modelo de mineração
  Na guia Modelos de Mineração do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode processar um modelo de mineração específico que está associado a uma estrutura de mineração ou processar todos os modelos que estão associados com a estrutura.  
  
 É possível processar um modelo de mineração usando as seguintes ferramentas:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 Você também pode usar um comando do processo XMLA. Para obter mais informações, consulte [Ferramentas e abordagens para processamento &#40;Analysis Services&#41;](../multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
### <a name="process-a-single-mining-model-using-sql-server-data-tools"></a>Processar um único modelo de mineração usando as Ferramentas de Dados do SQL Server  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados, selecione um modelo de mineração de uma ou mais colunas de modelos na grade.  
  
2.  No menu **Modelo de Mineração** , selecione **Processar Modelo**.  
  
     Caso faça uma alteração na estrutura de mineração, você receberá uma solicitação para implantar a estrutura novamente antes de processar o modelo. Clique em **Sim**.  
  
3.  No **processando modelo de mineração - \<modelo >** caixa de diálogo, clique em **executar**.  
  
     A caixa de diálogo **Andamento do Processo** é aberta e exibe os detalhes sobre o processamento do modelo.  
  
4.  Clique em **Fechar** na caixa de diálogo **Andamento do Processo** , após o modelo completar seu processamento.  
  
5.  Clique em **feche** na **processando modelo de mineração - \<modelo >** caixa de diálogo.  
  
 Só foram processados a estrutura de mineração e o modelo de mineração selecionado.  
  
### <a name="process-all-mining-models-that-are-associated-with-a-mining-structure"></a>Processar todos os modelos de mineração que estão associados com uma estrutura de mineração  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados, selecione **Processar Estrutura de Mineração e Todos os Modelos** a partir do menu **Modelo de Mineração** .  
  
2.  Caso faça alterações na estrutura de mineração, você receberá uma solicitação para implantar a estrutura novamente antes de processar os modelos. Clique em **Sim**.  
  
3.  No **processando estrutura de mineração - \<estrutura >** caixa de diálogo, clique em **executar**.  
  
4.  A caixa de diálogo **Andamento do Processo** é aberta e exibe os detalhes sobre o processamento do modelo.  
  
5.  Clique em **Fechar** na caixa de diálogo **Andamento do Processo** , após os modelos completarem seu processamento.  
  
6.  Clique em **feche** na **processamento \<modelo >** caixa de diálogo.  
  
 A estrutura de mineração e todos os modelos de mineração associados foram processados.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do modelo de mineração](mining-model-tasks-and-how-tos.md)  
  
  
