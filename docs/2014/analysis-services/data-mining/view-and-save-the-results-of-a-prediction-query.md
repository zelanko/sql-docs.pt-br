---
title: Exibir e salvar os resultados de uma consulta de previsão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- prediction queries [Analysis Services]
- viewing prediction query results
- displaying prediction query results
- Mining Model Prediction [Analysis Services], viewing results
ms.assetid: abba4d24-3619-44c1-8279-88f27ad627d3
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3d7cfbd171ea3762dae468c9d418bbd9693dd6ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009254"
---
# <a name="view-and-save-the-results-of-a-prediction-query"></a>Exibir e salvar os resultados de uma consulta de previsão
  Após ter definido uma consulta no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o Construtor de Consulta de Previsão, você pode executar a consulta e visualizar os resultados alterando para a exibição de resultado de consulta.  
  
 Você pode salvar os resultados de uma consulta de previsão em uma tabela em qualquer fonte de dados que esteja definida em um projeto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você pode criar uma tabela nova ou pode salvar os resultados da consulta em uma tabela existente. Se você salvar os resultados em uma tabela existente, poderá decidir sobrescrever os dados que estão armazenados atualmente na tabela; caso contrário, os resultados de consulta serão anexados aos dados existentes na tabela.  
  
### <a name="run-a-query-and-view-the-results"></a>Executar uma consulta e exibir os resultados  
  
1.  Na barra de ferramentas da guia **Previsão de Modelo de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique em **Resultado** .  
  
     A exibição dos resultados da consulta é aberta e a consulta é executada. Os resultados são exibidos em uma grade no visualizador.  
  
### <a name="save-the-results-of-a-prediction-query-to-a-table"></a>Salvar os resultados de uma consulta de previsão em uma tabela  
  
1.  Na barra de ferramentas da guia **Previsão de Modelo de Mineração** do Designer de Mineração de Dados, clique em **Salvar resultado de consulta**.  
  
     A caixa de diálogo **Salvar Resultado da Consulta de Mineração de Dados** é exibida.  
  
2.  Selecione uma fonte de dados da lista **Fonte de Dados** ou clique em **Novo** para criar uma nova fonte de dados.  
  
3.  Na caixa **Nome da tabela** , digite o nome da tabela. Se a tabela já existir, selecione **Substituir se existir** para substituir o conteúdo da tabela com os resultados da consulta. Se você não desejar substituir o conteúdo da tabela, não selecione esta caixa de seleção. Os novos resultados da consulta serão anexados aos dados existentes na tabela.  
  
4.  Selecione uma exibição da fonte de dados de **Adicionar a DSV** caso queira adicionar a tabela à exibição da fonte de dados.  
  
5.  Clique em **Salvar**.  
  
    > [!WARNING]  
    >  Se o destino não der suporte a conjuntos de linhas hierárquicos, você poderá acrescentar a palavra-chave FALTTENED aos resultados para salvar como uma tabela plana.  
  
  