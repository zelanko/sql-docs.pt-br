---
title: Editar manualmente uma consulta de previsão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying prediction queries
- Mining Model Prediction [Analysis Services], modifying prediction queries
- manual prediction query modification [Analysis Services]
ms.assetid: 9f6a9298-49d5-4675-ad49-977a47dff5a6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce2086e998704e893beaa92aabd2e51129a0450f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084206"
---
# <a name="manually-edit-a-prediction-query"></a>Editar manualmente uma consulta de previsão
  Depois de ter criado uma consulta usando o Construtor de Consultas de Previsão, você pode modificar a consulta alternando para a exibição Texto de Consulta na guia **Previsão de Modelo de Mineração** do Designer de Mineração de Dados. Um editor de texto aparece na parte inferior da tela para exibir a consulta criada pelo construtor de consultas.  
  
 Alternar para a exibição de Texto da Consulta é útil para fazer adições à consulta. Por exemplo, você pode adicionar uma cláusula WHERE ou ORDER BY.  
  
 Use a grade no Construtor de Consultas de Previsão para inserir os nomes de objetos e colunas, e configurar a sintaxe para funções de previsão individuais e, em seguida, alterne para o modo de edição manual para alterar os valores dos parâmetros.  
  
> [!NOTE]  
>  Se você retornar ao modo de exibição de **Design** por meio da exibição **Texto de Consulta** , quaisquer alterações efetuadas na exibição **Texto de Consulta** serão perdidas.  
  
### <a name="modify-a-query"></a>Modificar uma consulta  
  
1.  Na guia **Previsão de Modelo de Mineração** no Designer de Mineração de Dados do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique em **SQL**.  
  
     A grade na parte inferior da tela é substituída por um editor de texto que contém a consulta. Digite as alterações feitas na consulta neste editor.  
  
2.  Para executar a consulta, no menu **Modelo de Mineração** , selecione **Resultado**ou clique no botão para exibir os resultados da consulta.  
  
    > [!NOTE]  
    >  Se a consulta criada for inválida, a janela Resultados não exibirá um erro e não exibirá nenhum resultado. Clique no botão **Design** ou selecione **Design** ou **Consulta** no menu **Modelo de Mineração** para corrigir o problema e executar a consulta novamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Consultas de mineração de dados](data-mining-queries.md)   
 [Construtor de Consultas de &#40;de mineração de dados de previsão&#41;](../prediction-query-builder-data-mining.md)   
 [Lição 6: Criando e trabalhando com previsões &#40;Tutorial de mineração de dados básico&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
  
