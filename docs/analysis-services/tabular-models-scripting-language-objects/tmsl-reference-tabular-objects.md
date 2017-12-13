---
title: "Definições de objeto na tabela de modelo a linguagem de script (TMSL) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 486f0507-cec6-4672-b947-0bb61d1cbc46
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fcf8b3c47b7663e467ad421a3732f8663320f055
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="tmsl-reference---tabular-objects"></a>Referência TMSL - objetos de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Aplicativos que criam, consumir ou administrar bancos de dados tabulares ou que se conectam a uma instância do SQL Server 2016 Analysis Services no modo de tabela, pode usar o modelo de script TMSL (linguagem tabela) para comandos e representações de objeto no formato JSON.  
  
 Este artigo documenta os principais objetos do esquema TMSL usado em scripts gerados pelo SQL Server Management Studio, o SQL Server Data Tools (SSDT) e o PowerShell do AMO.  
  
 Definições de objeto em JSON e usados em TMSL comandos como Create, Alter e exclusão. Consulte [comandos na tabela de linguagem de scripts &#40; modelo TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) para obter uma lista de comandos.  
  
## <a name="main-objects"></a>Objeto principal  
 A tabela a seguir é uma lista dos objetos mais usados no script TMSL.  
  
|||  
|-|-|  
|[Objeto de banco de dados &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|Define um banco de dados Tabular no nível de compatibilidade 1200 ou superior, com base em um modelo do mesmo nível.|  
|[Objeto de modelo &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|Define um modelo de tabela no nível de compatibilidade 1200 ou superior.|  
|[Objeto de fonte de dados &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|Define uma conexão com uma fonte de dados usada durante a importação para carregar o modelo, ou para consultas de passagem quando o modelo estiver no modo DirectQuery.|  
|[Objeto Tables &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|Especifica as tabelas do modelo.|  
|[Objeto de partições &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|Define o armazenamento de conjuntos de linhas de tabela, incluindo tabelas calculadas.|  
|[Objeto de relações &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|Define as relações entre tabelas.|  
|[Objeto de funções &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|Define permissões, associação e os filtros de segurança que controlam o acesso a dados e operações.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
