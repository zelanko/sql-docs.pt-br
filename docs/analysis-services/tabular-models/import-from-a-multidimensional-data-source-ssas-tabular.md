---
title: "Importar de uma fonte de dados multidimensional (SSAS tabular) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7f0793ea-a4c7-42e9-b722-2164a454ebca
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Importar de uma fonte de dados multidimensional (SSAS tabular)
  Você pode usar um banco de dados de cubo do Analysis Services como uma fonte de dados para um modelo tabular. Para importar dados de um cubo do Analysis Services, você deve definir uma Consulta MDX para selecionar dados para importar.  
  
 Quaisquer dados contidos em um banco de dados do SQL Server Analysis Services pode ser importado para um modelo. É possível extrair total ou parcialmente uma dimensão, ou obter fatias e agregações do cubo, como soma das vendas, mês a mês, durante o ano atual, etc. Porém, você deveria se lembrar de que todos os dados que você importa de um cubo são bidimensionais. Portanto, se você definir uma consulta que recupera medidas ao longo de várias dimensões, os dados serão importados com cada dimensão em uma coluna separada.  
  
 Os cubos do Analysis Services devem ter a versão do SQL Server 2005, SQL Server 2008, SQL Server 2008 R2, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
### Para importar dados de um cubo do Analysis Services  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**.  
  
2.  Na página **Conectar com uma Fonte de Dados** , selecione **Microsoft Analysis Services**e clique em **Avançar**.  
  
3.  Siga as etapas no Assistente de Importação de Tabela. Você poderá especificar uma consulta MDX na página **Especificar uma Consulta MDX** . Para usar o Designer de Consulta MDX, na página Especificar uma Consulta MDX, clique em **Design**.  
  
## Consulte também  
 [Importar dados &#40;SSAS de Tabela&#41;](../Topic/Import%20Data%20\(SSAS%20Tabular\).md)   
 [Fontes de dados com suporte &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  