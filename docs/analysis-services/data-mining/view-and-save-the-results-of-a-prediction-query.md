---
title: Exibir e salvar os resultados de uma consulta de previsão | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f34e2dbdfea2f803672fda7b55f92b62e08c6df
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="view-and-save-the-results-of-a-prediction-query"></a>Exibir e salvar os resultados de uma consulta de previsão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
  
