---
title: Importar de uma fonte de dados Multidimensional (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f0793ea-a4c7-42e9-b722-2164a454ebca
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4aaa43e745c86cd493279fe8bd875d376f8185c0
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="import-data---multidimensional-data-source"></a>Importar dados - fonte de dados Multidimensional
  Você pode usar um banco de dados de cubo do Analysis Services como uma fonte de dados para um modelo tabular. Para importar dados de um cubo do Analysis Services, você deve definir uma Consulta MDX para selecionar dados para importar.  
  
 Quaisquer dados contidos em um banco de dados do SQL Server Analysis Services pode ser importado para um modelo. É possível extrair total ou parcialmente uma dimensão, ou obter fatias e agregações do cubo, como soma das vendas, mês a mês, durante o ano atual, etc. Porém, você deveria se lembrar de que todos os dados que você importa de um cubo são bidimensionais. Portanto, se você definir uma consulta que recupera medidas ao longo de várias dimensões, os dados serão importados com cada dimensão em uma coluna separada.  
  
 Os cubos do Analysis Services devem ter a versão do SQL Server 2005, SQL Server 2008, SQL Server 2008 R2, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
### <a name="to-import-data-from-an-analysis-services-cube"></a>Para importar dados de um cubo do Analysis Services  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**.  
  
2.  Na página **Conectar com uma Fonte de Dados** , selecione **Microsoft Analysis Services**e clique em **Avançar**.  
  
3.  Siga as etapas no Assistente de Importação de Tabela. Você poderá especificar uma consulta MDX na página **Especificar uma Consulta MDX** . Para usar o Designer de Consulta MDX, na página Especificar uma Consulta MDX, clique em **Design**.  
  
## <a name="see-also"></a>Consulte também  
 [Importar dados &#40;SSAS de Tabela&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Fontes de dados com suporte &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
