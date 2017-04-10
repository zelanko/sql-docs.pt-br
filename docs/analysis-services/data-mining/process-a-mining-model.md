---
title: "Processar um modelo de minera&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modelos de mineração [Analysis Services], processando"
ms.assetid: c2204472-c500-47a5-9afa-7ce2ca78b233
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 32
---
# Processar um modelo de minera&#231;&#227;o
  Na guia Modelos de Mineração do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode processar um modelo de mineração específico que está associado a uma estrutura de mineração ou processar todos os modelos que estão associados com a estrutura.  
  
 É possível processar um modelo de mineração usando as seguintes ferramentas:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 Você também pode usar um comando do processo XMLA. Para obter mais informações, consulte [Ferramentas e abordagens para processamento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
### Processar um único modelo de mineração usando as Ferramentas de Dados do SQL Server  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados, selecione um modelo de mineração de uma ou mais colunas de modelos na grade.  
  
2.  No menu **Modelo de Mineração** , selecione **Processar Modelo**.  
  
     Caso faça uma alteração na estrutura de mineração, você receberá uma solicitação para implantar a estrutura novamente antes de processar o modelo. Clique em **Sim**.  
  
3.  Na caixa de diálogo **Processando Modelo de Mineração – \<modelo>**, clique em **Executar**.  
  
     A caixa de diálogo **Andamento do Processo** é aberta e exibe os detalhes sobre o processamento do modelo.  
  
4.  Clique em **Fechar** na caixa de diálogo **Andamento do Processo** , após o modelo completar seu processamento.  
  
5.  Clique em **Fechar** na caixa de diálogo **Processando Modelo de Mineração – \<modelo>**.  
  
 Só foram processados a estrutura de mineração e o modelo de mineração selecionado.  
  
### Processar todos os modelos de mineração que estão associados com uma estrutura de mineração  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados, selecione **Processar Estrutura de Mineração e Todos os Modelos** a partir do menu **Modelo de Mineração** .  
  
2.  Caso faça alterações na estrutura de mineração, você receberá uma solicitação para implantar a estrutura novamente antes de processar os modelos. Clique em **Sim**.  
  
3.  Na caixa de diálogo **Processando Estrutura de Mineração – \<estrutura>**, clique em **Executar**.  
  
4.  A caixa de diálogo **Andamento do Processo** é aberta e exibe os detalhes sobre o processamento do modelo.  
  
5.  Clique em **Fechar** na caixa de diálogo **Andamento do Processo** , após os modelos completarem seu processamento.  
  
6.  Clique em **Fechar** na caixa de diálogo **Processando \<modelo>**.  
  
 A estrutura de mineração e todos os modelos de mineração associados foram processados.  
  
## Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  