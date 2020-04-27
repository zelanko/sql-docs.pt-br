---
title: Processar uma estrutura de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], processing
ms.assetid: 4162f33e-c23f-4293-8905-271781e45fa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92793adcf2fd04b1dac0c26933c1d5969a31f1a5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66083109"
---
# <a name="process-a-mining-structure"></a>Processar uma estrutura de mineração
  Para poder procurar ou trabalhar com modelos de mineração que são associados a uma estrutura de mineração, você deve implantar o projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e processar a estrutura de mineração e os modelos de mineração. Além disso, se fizer uma alteração na estrutura de mineração ou nos modelos de mineração, você será solicitado a reimplantá-los e processá-los. Processar a estrutura na guia de **Estrutura de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , processa todos os modelos associados.  
  
 É possível processar uma estrutura de mineração usando essas ferramentas:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA: comando Process  
  
 Para obter informações sobre como processar modelos individuais, consulte [Processar um modelo de mineração](process-a-mining-model.md).  
  
### <a name="to-process-a-mining-structure-and-all-associated-mining-models-using-sql-server-data-tools"></a>Para processar uma estrutura de mineração e todos os modelos de mineração associados usando as Ferramentas de Dados do SQL Server  
  
1.  Selecione **Estrutura de Mineração do Processo e Todos os Modelos** no item de menu **Modelo de Mineração** no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
     Caso faça alterações na estrutura, você receberá uma solicitação para implantar a estrutura novamente antes de processar os modelos. Clique em **Sim**.  
  
2.  Clique em **executar** na caixa de diálogo **processando estrutura de mineração \<– estrutura>** .  
  
     A caixa de diálogo **Andamento do Processo** é aberta para exibir os detalhes sobre o processamento do modelo.  
  
3.  Clique em **Fechar** na caixa de diálogo **Andamento do Processo** após os modelos completarem seu processamento.  
  
4.  Clique em **fechar** na caixa de diálogo **processando estrutura de mineração \<– estrutura>** .  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções da estrutura de mineração](mining-structure-tasks-and-how-tos.md)  
  
  
