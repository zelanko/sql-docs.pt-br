---
title: Editar manualmente uma consulta de previsão | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying prediction queries
- Mining Model Prediction [Analysis Services], modifying prediction queries
- manual prediction query modification [Analysis Services]
ms.assetid: 9f6a9298-49d5-4675-ad49-977a47dff5a6
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3fac2127ebab9e06a043d11f1b901a29f3a46ad9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="manually-edit-a-prediction-query"></a>Editar manualmente uma consulta de previsão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="see-also"></a>Consulte também  
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)   
 [Construtor de consultas de previsão & #40; mineração de dados & #41;](http://msdn.microsoft.com/library/12900d49-db88-48bb-a5f4-0a9a172bc126)   
 [Lição 6: Criando e trabalhando com previsões & #40; Tutorial de mineração de dados básicos & #41;](http://msdn.microsoft.com/library/b213cb58-2c40-4c89-b08b-d3c36a4afad3)  
  
  
