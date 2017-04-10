---
title: "Editar manualmente uma consulta de previs&#227;o | Microsoft Docs"
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
  - "modificando consultas de previsão"
  - "Previsão do modelo de mineração [Analysis Services], modificando consultas de previsão"
  - "modificação manual da consulta de previsão [Analysis Services]"
ms.assetid: 9f6a9298-49d5-4675-ad49-977a47dff5a6
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 17
---
# Editar manualmente uma consulta de previs&#227;o
  Depois de ter criado uma consulta usando o Construtor de Consultas de Previsão, você pode modificar a consulta alternando para a exibição Texto de Consulta na guia **Previsão de Modelo de Mineração** do Designer de Mineração de Dados. Um editor de texto aparece na parte inferior da tela para exibir a consulta criada pelo construtor de consultas.  
  
 Alternar para a exibição de Texto da Consulta é útil para fazer adições à consulta. Por exemplo, você pode adicionar uma cláusula WHERE ou ORDER BY.  
  
 Use a grade no Construtor de Consultas de Previsão para inserir os nomes de objetos e colunas, e configurar a sintaxe para funções de previsão individuais e, em seguida, alterne para o modo de edição manual para alterar os valores dos parâmetros.  
  
> [!NOTE]  
>  Se você retornar ao modo de exibição de **Design** por meio da exibição **Texto de Consulta**, quaisquer alterações efetuadas na exibição **Texto de Consulta** serão perdidas.  
  
### Modificar uma consulta  
  
1.  Na guia **Previsão de Modelo de Mineração** no Designer de Mineração de Dados do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique em **SQL**.  
  
     A grade na parte inferior da tela é substituída por um editor de texto que contém a consulta. Digite as alterações feitas na consulta neste editor.  
  
2.  Para executar a consulta, no menu **Modelo de Mineração**, selecione **Resultado** ou clique no botão para exibir os resultados da consulta.  
  
    > [!NOTE]  
    >  Se a consulta criada for inválida, a janela Resultados não exibirá um erro e não exibirá nenhum resultado. Clique no botão **Design** ou selecione **Design** ou **Consulta** no menu **Modelo de Mineração** para corrigir o problema e executar a consulta novamente.  
  
## Consulte também  
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)   
 [Construtor de Consultas de previsão &#40;Mineração de Dados&#41;](../Topic/Prediction%20Query%20Builder%20\(Data%20Mining\).md)   
 [Lição 6: Criando e trabalhando com previsões &#40;Tutorial de mineração de dados básico&#41;](../Topic/Lesson%206:%20Creating%20and%20Working%20with%20Predictions%20\(Basic%20Data%20Mining%20Tutorial\).md)  
  
  